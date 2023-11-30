# Configuration

Stackmate uses a really simple configuration file that describes your infrastructure and resides in your application's directory.  It is advised to store it along with your application's code and commit it in source control so that you can track your infrastructure's changes consistently.

Here's everything you need to know in a gist:

### You don't have to write it yourself

We are fully aware of two things: a) It's really annoying when you need to quickly try a tool out and you have to go through long documentation documents just to get started and b) you probably don't really like YAML very much.

That's why we focused on automatically generating the configuration file and asking the developer to do as little as possible in order to get up and running. You can provide any number of services, stages and just be done with it. For example the following command:

```
stackmate init --with mysql,redis --stages production,staging
```

will generate a YAML configuration file that includes a MySQL and a Redis service and two deployment environments: `production` and `staging`.

### It can be a YAML or JSON file

For those who don't really like YAML, we decided to support JSON configuration files as well. You can create a JSON configuration file when initializing a project by specifying the `--format` flag:

```
stackmate init --with mysql --format json
```

You can find more information on the `init` command [page](../commands/stackmate-init.md).

### Options

The stackmate configuration file is designed to be as simple and straight-forward as it gets. The following list summarizes the configuration attributes that you can apply and you can find more details in the corresponding sections.

* [`name`](../configuration/name.md) - The project's url-friendly name
* [`provider`](../configuration/provider.md) - The default cloud provider for the services deployed
* [`region`](../configuration/region.md) - The default region to deploy the services within
* [`state`](../configuration/state.md) - The state storage configuration. _Applies to all environments_
* [`secrets`](../configuration/secrets.md) - _**Optional**_ - The secrets storage configuration. _Applies to all environments_
* [`stages`](../configuration/stages.md) - The stages and list of services that are available for each

### Configuration example

The following configuration file, will deploy two environments, `production` and `staging` and each will hold two AWS-managed services:&#x20;

* A MySQL database on RDS instance of `db.t3.medium` size and
* A Redis cache of `cache.t3.medium` size

The services will be provisioned with sane defaults and will be within the free tier

{% code title=".stackmate/config.yaml" %}
```yaml
name: sample-app
provider: aws
region: eu-central-1

state:
  bucket: stackmate-sample-app-state-files

# It is implied that secrets are stored in AWS Secrets Manager
# since we're using AWS as our provider

stages:
  production:
    database:
      type: mysql
      size: db.t3.medium
      storage: 30

    cache:
      type: redis
      size: cache.t3.medium

  # Environment overrides - staging
  staging:
    from: production
    skip:
      - cache
```
{% endcode %}
