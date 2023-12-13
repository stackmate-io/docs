# Getting started

### Deploy MySQL and Redis on AWS in just a moment

Follow this simple guide to deploy a MySQL and a Redis instance on **your** AWS account. By the end of this guide, you'll have a MySQL instance running on RDS and a Redis cluster on Elasticache.What you'll need:

* An [AWS account](https://docs.aws.amazon.com/SetUp/latest/UserGuide/setup-AWSsignup.html) with the credentials stored in your local machine. You could create an AWS profile that uses those credentials and would make things easier. More details on the [official AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html). If you already have an AWS account profile set up locally, you can skip this.
* [Terraform](https://www.terraform.io/) installed locally. You can follow the [official Terraform documentation](https://developer.hashicorp.com/terraform/install) to do that, or if you already have Terraform installed, feel free to skip this part.
* [NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) to help us install stackmate.
* Your favorite text editor, terminal and a working internet connection.

Here's what you'll get after you've finished this guide:

* A MySQL database instance on RDS, within the AWS free tier to help run in sane costs
* A Redis instance on Elasticache, within the AWS free tier
* A VPC and Internet Gateway to keep your database instances isolated and secure
* Your credentials securely stored on AWS Secrets Manager

{% hint style="info" %}
This guide is meant for the Community Edition of Stackmate which is free and open-source.\
\
We also offer a [Cloud edition](https://stackmate.io/cloud/) that sets up your AWS account for you and deploys every time you push a new commit. We offer a **trial of 7 days** and **no credit card** is required
{% endhint %}

### 1. Create a configuration file

First, we need to create a configuration file for stackmate, under its default location which is `.stackmate/config.yml`. You can start by copying the code specified in this [example file](https://github.com/stackmate-io/stackmate/blob/main/examples/db-redis.yml) on the [stackmate repository](https://github.com/stackmate-io/stackmate). Our configuration file would then look something like this:

```yaml
---
# Optional - by default stackmate uses AWS
# provider: aws

# Optional - by default stackmate deploys to eu-central-1
# region: eu-central-1

state:
  # 👇 This will store the state file in our local machine
  # and should be OUTSIDE your source code repository,
  # so that you make sure it NEVER GETS COMMITTED to git
  #
  # Alternatively, you can use an S3 bucket to store the state
  # you can find more information by the end of this guide
  workspaceDir: /Users/<myusername>/.stackmate-states/my-cool-project

environments:
  production:
    mysql-database:
      type: mysql
      # Note: Use the externalLinks attribute to allow a resource
      # that's not deployed by stackmate to access the database
      # externalLinks:
      #  - 1.2.3.4
    redis-cache:
      type: redis

```

**Quick note**: By default your resources are deployed in a [VPC,](https://aws.amazon.com/vpc/) meaning that they're isolated from the outside world but all resources deployed by Stackmate, can connect with each other. If you need to allow connections from a resource that's not deployed by Stackmate, consider adding the `externalLinks` attribute to the service as documented in [basic-options.md](configuration/basic-options.md "mention").

### 2. Create the directory to store the Terraform state in

Terraform requires a [state](https://developer.hashicorp.com/terraform/language/state) file to be present, so that it knows what the desired state of your infrastructure will be every time. For the sake of this guide, we will be storing our state files locally, but at the end of this guide, we'll see how we can use an AWS S3 bucket to securely store our states in.

Please note that as described in [#should-i-commit-the-files-that-are-generated-by-stackmate](appendix/output-files.md#should-i-commit-the-files-that-are-generated-by-stackmate "mention"), we should **NEVER** commit our state to version control and this is why the directory is set outside our repository. Now let's go ahead and create the directory:

```bash
$ mkdir -p ~/.stackmate-states/my-cool-project
```

### 3. Pick an AWS profile to use

Use your favorite editor to view an existing, or add a new AWS profile on your AWS configuration. As an example, we'll be using an AWS profile named `stackmate-user`. More details on the [official AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html).

### 4. Run the deployment!

Let's now prefix the AWS profile to the [stackmate-deploy.md](commands/stackmate-deploy.md "mention") command and we're ready to go!

```
AWS_PROFILE=stackmate-user npx @stackmate/stackmate deploy production
```

This will do the following:

* Install stackmate cli locally (if it's not available already)
* Load the AWS profile specified
* Set up our infrastructure on the AWS account specified.

You'll be getting output on your terminal regarding the progress and once it's done, you'll get the endpoints you can connect to. For example:

```bash
# ... more output here ...
Apply complete! Resources: 4 added, 0 changed, 0 destroyed.

Outputs:
aws_redis_eu_central_1_1_endpoint = "redis-cache-production.abcdefg.0001.euc1.cache.amazonaws.com"
aws_mysql_eu_central_1_1_endpoint = "mysql-database-production.abcdefg.eu-central-1.rds.amazonaws.com:3306"
```

Your infrastructure is now deployed and ready to be used!

### 5. Bonus points: Use an S3 bucket to store the state

Deploying your state on an S3 bucket, allows your team to access it centrally, makes sure it's always available and handles versioning and locking. The benefits and the process Terraform uses is described in this [documentation page](https://developer.hashicorp.com/terraform/language/settings/backends/s3).

To be able to use an S3 bucket in our stackmate configuration with locking, the following needs to exist in advance:

* An [S3 bucket](https://aws.amazon.com/s3/) with versioning and no public access
* A [DynamoDB](https://aws.amazon.com/dynamodb/) table to be used for locking

You can create these resources manually, as described in numerous tutorials (for example [this](https://dev.to/aws-builders/configure-a-remote-backend-with-aws-s3-and-dynamodb-state-locking-in-terraform-3jne) one) but if you're already familiar with Terraform, we have prepared a [terraform script](https://github.com/stackmate-io/stackmate/blob/main/utilities/create-s3-state/main.tf) for you that you can use to create the resources described above. Here's how:

```bash
# create a working directory
mkdir ~/stackmate-state-preparation
cd ~/stackmate-state-preparation

# download the script from GitHub
curl -O https://raw.githubusercontent.com/stackmate-io/stackmate/main/utilities/create-s3-state/main.tf

# Initialize terraform
terraform init

# Apply changes using your AWS profile
AWS_PROFILE=stackmate-user terraform apply

# You'll get prompts similar to the following ones, you can 
# var.aws_dynamodb_lock_table_name
#   Enter a value: stackmate-state-locking

# var.aws_s3_bucket_name
#  Enter a value: stackmate-terraform-states

# var.infrastructure_region
#  Enter a value: eu-central-1

# Do you want to perform these actions?
#  Terraform will perform the actions described above.
#  Only 'yes' will be accepted to approve.
#  Enter a value: yes

# Ouptut would look something like this:
# aws_dynamodb_table.terraform_state_lock: Creating...
# aws_s3_bucket.terraform_state: Creating...
# aws_s3_bucket.terraform_state: Creation complete after 3s [id=stackmate-terraform-states]
# aws_s3_bucket_versioning.terraform_state: Creating...
# aws_s3_bucket_versioning.terraform_state: Creation complete after 2s [id=stackmate-terraform-states]
# aws_dynamodb_table.terraform_state_lock: Creation complete after 8s [id=stackmate-state-locking]

# Apply complete! Resources: 3 added, 0 changed, 0 destroyed.

# Outputs:

# state_bucket = "stackmate-terraform-states"
# lock_table = "stackmate-state-locking"

```

The directory we used and its contents should now be safe to delete

You can use the value in the "Outputs" sections above to configure stackmate:

```yaml
---
state:
  # Copy the values from the outputs above
  bucket: stackmate-terraform-states
  lockTable: stackmate-state-locking

environments:
  production:
    # ... the rest of our configuration ...

```

Our next deployments will store the state in S3 and the state will be locked in DynamoDB

{% hint style="info" %}
[Stackmate Cloud](https://stackmate.io/cloud/) creates the state bucket and lock table for you and handles AWS profiles automatically, once it securely access your AWS account. We offer a **trial of 7 days** and **no credit card** is required.
{% endhint %}

Next steps

* You can check out the additional configuration in [Database services configuration page](configuration/database-services.md) or [Cache services configuration page](configuration/cache-services.md) and update the service section on `.stackmate/config.yml` accordingly
* You can add more [services](broken-reference) to your configuration
* You can add more [environments](configuration/configuration-file/environments.md) to your project, for example a `staging` environment
* [Install](appendix/installation.md) `stackmate` globally to avoid using `npx @stackmate/stackmate`
* Tweet about [@stackmate](https://twitter.com/stackmate), raise an [issue](https://github.com/stackmate-io/stackmate/issues), or view our [roadmap](https://github.com/stackmate-io/stackmate/projects).
