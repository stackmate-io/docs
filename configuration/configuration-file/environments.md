# environments

The `environments` configuration is the most important part of the stackmate configuration file, since it contains all of your environments and services that are related to it. The structure of the object is as follows:

```
environments:
  <stage name>:
    <service name>:
      ... service configuration ...
  <other stage name>:
    ....
```

As you can see, each environment is added as a key to the `environments` object and every service that should be deployed on every environment, should be a key to the corresponding environment.

### Common Service Options

Every service on a stackmate configuration, should have a unique name and can be described with the following attributes:

#### Required attributes

* `type` - The service's type. It should be one of the services available. Acceptable values are:&#x20;
  * `application`  - Configures an Application service, an application running on a container
  * `object-store` - Configures an [object store](../object-storage.md) service like AWS S3
  * `memcached` - Configures a managed [Memcached](../cache-services.md) cluster service (eg. AWS Elasticache)&#x20;
  * `mariadb` - Configures a managed [MariaDB](../database-services.md) instance (eg. MariaDB on AWS RDS)
  * `mysql` - Configures a managed MySQL instance (eg. MySQL on AWS RDS)
  * `postgresql` - Configures a managed PostgreSQL instance (eg. PostgreSQL on AWS RDS)
  * `redis` - Configures a managed Redis instance (eg. AWS Elasticache)

{% hint style="info" %}
You can find more information for each service-specific options, on the corresponding page
{% endhint %}

#### Optional attributes

* `region` - the region to deploy the service. If not provided, the default configuration for the project's [`region`](region.md) is used.
* `links` - A list of services that are inter-connected. For example a `mysql` service could be linked to the `application` service in order to allow incoming connections from the `application` service.
* `externalLinks` - A list of IPs of resources not deployed by Stackmate, to allow outside connections from
* `profile` - A pre-made profile to use for the service. If not specified, the `default` profile is used for the service. You need to refer to every service separately in order to view the corresponding options available. You can browse the profiles available in our [repository](https://github.com/stackmate-io/stackmate/tree/main/src/services/providers/aws/profiles).
* `overrides` - An object with attributes to override the default profile with. Each service has its own profile and own overrides. You need to refer to every service separately in order to view the corresponding options available.

These configuration options are available across all services on stackmate, and each service may or may not provide additional attributes to be configured by.

### Available services

Stackmate supports the following services that you can use in your environments configuration:

* [Database Services](../database-services.md)
* [Cache Services](../cache-services.md)
* [Object storage](https://app.gitbook.com/o/1hvtqlSFUrlyNGJZFoLw/s/-MZRy1bgyIc6l7rYOrXd/\~/changes/61/services/object-storage)

You can find all the available options for every service on the corresponding page

### Example

{% code title=".stackmate/config.yaml" %}
```yaml
provider: aws
region: eu-central-1
...
environments:
  production:    # the production stage
    mysqldb:        # a mysql database service
      type: mysql
      size: db.t3.2xlarge
      storage: 300
      # ....
    postgresqldb:   # a postgresql database service
      type: postgresql
      size: db.t3.2xlarge
      storage: 300
      # ...

  staging:        # the staging stage, copied from production but with lower specs
    mysqldb:
      type: mysql
      size: db.t3.micro
      storage: 10
      # ....
    postgresqldb:   # a postgresql database service
      type: postgresql
      size: db.t3.micro
      storage: 10
      # ...
```
{% endcode %}
