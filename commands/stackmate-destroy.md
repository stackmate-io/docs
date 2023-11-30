# stackmate copy

The `stackmate copy` command copies a stage and adds it to the configuration file.

### Usage

```
stackmate copy <source> <target> [...arguments]
```

### Arguments

* `<source>` - Which stage to copy. It should be one of the stages that are already available in your `.stackmate/config.yml` file
* `<target>` should be the name of the stage to add and it should not already be present on your `.stackmate/config.yml` files

### Options

* `--skip service1, service2` - Comma separated list of the services to skip when inheriting from the base stage. For example, you can base the new stage onto `production` but choose to skip the `cache` service
