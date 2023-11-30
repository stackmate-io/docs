# stackmate preview

The `stackmate service` command introduces a new service to the stack. By default the service is introduced to the `production` stage but you can choose otherwise.

### Usage

```
stackmate service <service type> [--stage production]
```

### Arguments

* `<service type>` The service to add to the stage. For a full list of the supported services, please check out the [stages configuration](../configuration/environments.md) for supported options.

### Options

* `--stage` should be one of the stages declared inside your `.stackmate/config.yml` file, for example `production` or `staging`. By default the `production` stage will be used
