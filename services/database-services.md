# Database services

Stackmate offers infrastructure deployment for major managed database services (like AWS RDS for example)

### What you get when introducing this service to your configuration

* A managed database instance with sane defaults

### Required attributes

* `type` - **string** - It should be either `mysql`, `postgresql` or `mariadb`

### Optional attributes

* `provider` - **string** - by default is set to `aws`
* `size` - **string** - The instance size. Should be one of the instances the cloud provider has available
* `version` - **string** - The database version to use. These are dictated by the cloud provider (eg. AWS) and it's one of the versions they currently support.
* `storage` - **number** - The size of the storage space in Gigabytes
* `database` - **string** - The name of the database to deploy
* `port` - **number** - The port to use. By default, `3306` is assigned to `mysql` and `mariadb` and `5432` for `postgresql`
* `monitoring` - **object** - Any monitoring options available for the service. Example configuration is shown below

The typical [Common Service Options](../configuration/environments.md#common-service-options) apply here too.

### Credentials for the root user:

The password for the root user associated with the database, is stored as a secret on your provider, you can link directly to it through your provider's secret manager (eg. AWS secrets manager)

### Example configuration

```yaml
# ... the rest of the configuration ...
environments:
  production:
    # ... more services ...
    my-database:
      type: mysql
      provider: aws         # optional when your provider's set to aws
      region: eu-central-1  # optional if you have a region set for the project
      size: db.t2.micro
      storage: 30
      version: 8.0
      database: my-database
      profile: default      # this is the default
      monitoring:
        urls:
          - https://a-webhook-to-get-alerted-by.com
        emails:
          - database-alerts@mywebsite.com
```
