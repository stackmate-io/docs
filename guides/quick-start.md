---
description: >-
  This is the TL;DR version of our usage guide and deploys MySQL on AWS RDS as
  an example
---

# Quick Start

### Deploy MySQL on AWS with a single command

As a quick start, we'll deploy an MySQL database on AWS RDS, when no configuration file is available in the project

```
npx @stackmate/cli init --with mysql --deploy
```

Stackmate will then create a configuration file, ask you to provide your AWS credentials or profile, and use Terraform to deploy your resources on AWS

#### What you get after the deployment

* Automatically generated project configuration file to save you from creating it from scratch
* A MySQL database instance on RDS, within the AWS free tier to reduce costs
* A VPC and Internet Gateway to keep your database isolated and securepi
* Terraform state, securely stored in a private, encrypted S3 Bucket
* Your username and password securely stored on AWS Secrets Manager

#### Next steps

* You can check out the additional configuration in [MySQL service's configuration page](https://docs.stackmate.io/services/mysql) and update the service section on `.stackmate/config.yml` accordingly
* You can add more services to your configuration
* You can add more environments to your project, for example a `staging` environment
* Install `stackmate` globally to avoid using `npx @stackmate/cli`
* Tweet about [@stackmate](https://twitter.com/stackmate), raise an [issue](https://github.com/stackmate-io/stackmate/issues), join the [discussion](https://github.com/stackmate-io/stackmate/discussions), or view our [roadmap](https://github.com/stackmate-io/stackmate/projects).

### Committing to source control

Stackmate and its generated files are populated in a way which allows you to commit all the files created to source control (eg. Git). If you wish to skip some files however, feel free to take a look into our [Generated files section](https://docs.stackmate.io/general/generated-files).
