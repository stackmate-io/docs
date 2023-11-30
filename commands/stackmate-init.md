# stackmate init

The `stackmate init` command initializes a stackmate configuration file inside a project directory

### Usage

```
stackmate init --with <service list> [...additional arguments]
```

The `--with` argument is required in order for stackmate to add some services to your configuration file.&#x20;

### Options

* `--with <service1, service2,...>` - **required** - Comma separated list of the services to add to the production environment. For a full list of the supported services, please check out the [stages configuration](../configuration/stages.md) for supported options.
* `--name <project-name>` - The name for the project. The default value is the name of the directory that the [`init`](stackmate-init.md) command is currently running in
* `--provider <provider>` - Should be one of the providers available, for example `aws`. For a full list of the providers we support, please check out the [provider configuration](../configuration/provider.md) for supported options.
* `--region <region>` - Correlates with the `--provider` flag, should be one of the regions that are available for the provider specified (or the default provider that is found in your preferences file if none is provided as a command flag). You can check out the [region configuration](../configuration/region.md) for supported options
* `--deploy <true | false>` - Boolean value, indicates whether we should deploy the `production` stage after the project's initialization.
* `--stages <production, staging...>` - Comma separated list of the stages to add. By default the `production` stage is added. In case you don't specify a `production` stage, the first on the list will become the main one. The rest of the stages will inherit from the `production` one. You can read more information in the [stages configuration](../configuration/stages.md) page.
* `--format <yaml | json>` - Can be one of `yaml`, `json` and specifies the file type of the configuration file.
