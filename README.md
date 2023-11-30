# Introduction

### What is Stackmate?

Stackmate is a free, open source tool that helps busy professionals deploy their cloud infrastructure without doing much. It abstracts and simplifies resource creation, modification and destruction in an intuitive way.

The reasoning behind Stackmate is that most of the times, all developers want is to simply deploy their database, cache or object storage services, without having to read the manual or go through complex DevOps processes.

### Who is Stackmate for?

Stackmate was built with the busy developer in mind. People who want to deploy an average traffic website that depends on a database and a few complementary services, without getting lost in their cloud provider's console or documentation.

### How does it work?

Stackmate uses an extremely simple configuration file either in JSON or YAML format. Before you read on, let us re-assure you that we are fully aware that people hate YAML with a burning passion. That's why we do two things with said file:

* Stackmate **generates it automatically** for you and
* We kept it very very **very** simple.

After you generate (and modify, if necessary) the configuration file, you may use the `deploy` command to provision your cloud resources on the provider of choice. The deployment process works as follows:

* Stackmate will build the [Terraform](https://www.terraform.io/) configuration for the selected stage (eg. `production`)
* The generated [Terraform](https://www.terraform.io/) configuration will be stored in the project's folder by default, or any other folder you decide to specify
* It will ask you to provide the credentials or stored cloud provider profile, for example, an [AWS profile](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html) stored on your `~/.aws/config` file
* Stackmate will use your system's Terraform executable to provision your cloud resources and store
* It will store the [Terraform State](https://www.terraform.io/language/state/remote) to a secure location (either AWS S3, Terraform Cloud or any remote which is considered safe)
* It will store random generated secrets to a secure remote location (for example AWS Secrets Manager) so that you can securely view and rotate them.

Once your stack has successfully been deployed, any modifications you make on the configuration file, will be reflected on your cloud infrastructure the next time you re-run the `deploy` command and any resource deleted from the configuration, will also be destroyed once you re-deploy.

### An important note regarding manual modification

Same as Terraform (which is used under the hood), any manual modification on your Stackmate-managed resources, will be lost when you next deploy. For example, if your Stackmate configuration file declares a MySQL database which is deployed on AWS and has a size of `db.t3.micro` and you modify it to eg. `db.t3.large`, that modification will be lost when you next deploy, due to Terraform's declarative nature.
