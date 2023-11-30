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

### Service configuration

You can find more information on how to configure your services on the [available-services.md](../services/available-services.md "mention") configuration page, or by visiting each service's documentation page.

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
