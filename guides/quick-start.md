---
description: >-
  This is the TL;DR version of our usage guide and deploys MySQL on AWS RDS and
  Redis on AWS Elasticache as an example
---

# Quick Start

### Deploy MySQL and Redis on AWS in just a moment

As a quick start, we'll deploy a MySQL and a Redis database on AWS, you may follow along with your favorite text editor and command line to replicate this example.

{% hint style="info" %}
If you find this guide too cumbersome, perhaps you could find our [Cloud](https://stackmate.io/cloud/) version more interesting and easier to use. We offer a **trial of 7 days** and **no credit card** is required.
{% endhint %}

### 1. Create a configuration file

First, we need to create a configuration file (the default location would be `.stackmate/config.yml`). You can start by copying the code specified in this [example file](https://github.com/stackmate-io/stackmate/blob/main/examples/db-redis.yml) on the [stackmate repository](https://github.com/stackmate-io/stackmate). Our configuration file would then look something like this:

```yaml
---
# Optional - by default stackmate uses AWS
# provider: aws

# Optional - by default stackmate deploys to eu-central-1
# region: eu-central-1

state:
  # 👇 these need to exist on AWS prior to the deployment, we'll get there in a minute
  bucket: my-stackmate-state-bucket
  lockTable: stackmate-terraform-state-lock

environments:
  production:
    mysql-database:
      type: mysql
    redis-cache:
      type: redis

```

### 2. Create the state bucket and DynamoDB lock table

All you need to do before hand is to create an S3 bucket that will store the Terraform state and a DynamoDB table to use for state locking, so that deployments are atomic and nobody in your team deploys a conflicting version. You can follow our super easy [guide](https://app.gitbook.com/o/1hvtqlSFUrlyNGJZFoLw/s/-MZRy1bgyIc6l7rYOrXd/\~/changes/61/appendix/preparing-for-deployment) to create your bucket and DynamoDB table.&#x20;

Note: you can also use an existing bucket by specifying a different key as described in our [state configuration](../configuration/state.md) guide.

### 3. Run the deployment

You are now ready to deploy your infrastructure! All you need to do is run:

```
npx @stackmate/cli deploy production
```

If your configuration file is stored in a location other than `.stackmate/config.yml`, you can specify the configuration file by running

```
npx @stackmate/cli deploy production -c <my-configuration.yml>
```

### What you get after the deployment

* A MySQL database instance on RDS, within the AWS free tier to help run in sane costs
* A Redis instance on Elasticache, within the AWS free tier
* A VPC and Internet Gateway to keep your database instances isolated and secure
* Terraform state, securely stored in a private, encrypted S3 Bucket
* Your username and password securely stored on AWS Secrets Manager

#### Next steps

* You can check out the additional configuration in [MySQL service's configuration page](https://docs.stackmate.io/services/mysql) and update the service section on `.stackmate/config.yml` accordingly
* You can add more services to your configuration
* You can add more environments to your project, for example a `staging` environment
* Install `stackmate` globally to avoid using `npx @stackmate/cli`
* Tweet about [@stackmate](https://twitter.com/stackmate), raise an [issue](https://github.com/stackmate-io/stackmate/issues), join the [discussion](https://github.com/stackmate-io/stackmate/discussions), or view our [roadmap](https://github.com/stackmate-io/stackmate/projects).

### Committing to source control

Stackmate and its generated files are populated in a way which allows you to commit all the files created to source control (eg. Git)
