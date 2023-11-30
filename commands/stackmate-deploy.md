# stackmate deploy

The `stackmate deploy` command applies changes to an environment specified. It is responsible for deploying and modifying your infrastructure.

### Usage

```
stackmate deploy <environment> [-c configuration.yml -d working-directory]
```

### Arguments

* `<environment>` The environment to deploy

### Options

* `--configuration <file>, -c <file>` the configuration file to be used for this operation. By default `.stackmate/config.yml` is used
* `--directory <dir>, -d <dir>` the directory to use as a working one, where the [output-files.md](../guides/output-files.md "mention") will be generated&#x20;
