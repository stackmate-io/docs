# stackmate config

The `stackmate config` command retrieves or sets values in the application's preferences file which is located in your home directory

### Usage

#### Retrieving a value

```
stackmate config:get <option>
```

The command in the example above, will output the value for the default cloud provider that should be used in future project configurations

#### Setting a value

```
stackmate config:set <option> <value>
```

The command in the example above will set `aws` to be the default cloud provider for future project configurations, meaning that next time you don't specify a provider in `stackmate init` it will automatically assign `aws` as the provider

### Available options

* `default-provider` - The default provider to use for new project configuration files. Should be one of the cloud providers available in the system
* `default-region` - The default region to use for new project configuration files. Should be one of the regions available for the `default-provider`
* `terraform-path` - The path for the terraform executable
