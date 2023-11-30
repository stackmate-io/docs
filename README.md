# Introduction

### What is Stackmate?

Stackmate is a free, open source tool that helps busy professionals deploy their cloud infrastructure without doing much. It abstracts and simplifies resource creation, modification and destruction in an intuitive way.

The reasoning behind Stackmate is that most of the times, all developers want is to simply deploy their database, cache or object storage services, without having to read the manual or go through complex DevOps processes.

### Who is Stackmate for?

Stackmate was built with the busy developer in mind. It's for people who want to deploy an average traffic website, that depends on a database and a few complementary services, without spending a lifetime in complex consoles or developer tools.

### How does it work?

Stackmate uses an extremely simple configuration file either in JSON or YAML format. Before you read on, let us re-assure you that we are fully aware that people hate YAML with a burning passion and that's why we kept it very very **very** simple, by providing sane defaults for the services deployed.

After you create the configuration file, you may use the `deploy` command to provision your cloud resources on the cloud provider of choice (\* we currently only support AWS but there's more to come):

* Stackmate will build the [Terraform](https://www.terraform.io/) configuration for the selected environment (eg. `production`).
* The generated [Terraform](https://www.terraform.io/) configuration will be stored in the project's folder (for example under `stacks/production/main.tf.json`).
* You don't need to provide your AWS credentials in your configuration, you can use environment variables or an [AWS profile](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html) stored on your `~/.aws/config` file.
* Stackmate will trigger CDKTF which will look for your system's Terraform executable to provision your cloud resources
* It will store the [Terraform State](https://www.terraform.io/language/state/remote) to the corresponding location as per your configuration.
* It will store random generated secrets to a secure remote location (for example AWS Secrets Manager) so that you can securely view and rotate them.

Once your stack has successfully been deployed, any modifications you make on the configuration file, will be reflected on your cloud infrastructure the next time you re-run the `deploy` command and any resource deleted from the configuration, will also be destroyed once you re-deploy.

### An important note regarding manual modification

Same as Terraform (which is used under the hood), any manual modification on your Stackmate-managed resources, will be lost when you next deploy. For example, if your Stackmate configuration file declares a MySQL database which is deployed on AWS and has a size of `db.t3.micro` and you modify it to eg. `db.t3.large`, that modification will be lost when you next deploy, due to Terraform's declarative nature.
