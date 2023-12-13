# stackmate preview

The `stackmate preview` command shows the changes that will be applied to the stack after you've updated your configuration file

### Usage

```
stackmate preview <environment> [-c configuration.yml -d working-directory]
```

### Arguments

* `<environment>` The environment to preview the changes for

### Options

* `--configuration <file>, -c <file>` the configuration file to be used for this operation. By default `.stackmate/config.yml` is used
* `--directory <dir>, -d <dir>` the directory to use as a working one, where the [output-files.md](../guides/output-files.md "mention") will be generated&#x20;
