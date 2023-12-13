# Configuration File

{% hint style="info" %}
[Stackmate Cloud](https://stackmate.io/cloud/) replaces the configuration file and command line with a simple to use interface and automatic deployments. We offer a **trial of 7 days** and **no credit card** is required.
{% endhint %}

Stackmate uses a really simple configuration file that describes your infrastructure and resides in your application's directory.  It is advised to store it along with your application's code and commit it in source control so that you can track your infrastructure's changes consistently.

The configuration file can be either a YAML or JSON file and examples are provided in the stackmate repository under the [examples](https://github.com/stackmate-io/stackmate/blob/main/examples) directory.

### Options

The stackmate configuration file is designed to be as simple and straight-forward as it gets. The following list summarizes the configuration attributes that you can apply and you can find more details in the corresponding sections.

* [`state`](../configuration/state.md) - _Required_ - The state storage configuration. _Applies to all environments_
* [`environments`](../configuration/environments.md) - _Required_ - The environments and list of services that are available
* [`provider`](../configuration/provider.md) - _Optional_ - The default cloud provider for the services deployed (by default we're using `aws`)
* [`region`](../configuration/region.md) - _Optional_ - The default region to deploy the services within (by default we're using `eu-central-1`)

### Configuration example

The following configuration file, will deploy two environments, `production` and `staging` and each will hold two AWS-managed services:&#x20;

* A MySQL database on RDS instance of `db.t3.medium` size and
* A Redis cache of `cache.t3.medium` size

The services will be provisioned with sane defaults and will be within the free tier

{% code title=".stackmate/config.yaml" %}
```yaml
provider: aws
region: eu-central-1

state:
  bucket: stackmate-sample-app-state-files

# It is implied that secrets are stored in AWS Secrets Manager
# since we're using AWS as our provider
environments:
  production:
    database:
      type: mysql
      size: db.t3.large
      storage: 30

    cache:
      type: redis
      size: cache.t3.large

  staging:
    database:
      type: mysql
      size: db.t3.micro
      storage: 10

    cache:
      type: redis
      size: cache.t3.micro
```
{% endcode %}
