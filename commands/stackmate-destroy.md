# stackmate destroy

{% hint style="danger" %}
**WARNING!** This will tear down your entire infrastructure **without any confirmation**, use when you're completely sure about what you're doing!
{% endhint %}

The `stackmate destroy` command applies **completely destroys your entire infrastructure**.

### Usage

```
stackmate destroy <environment> [-c configuration.yml -d working-directory]
```

### Arguments

* `<environment>` The environment to destroy

### Options

* `--configuration <file>, -c <file>` the configuration file to be used for this operation. By default `.stackmate/config.yml` is used
* `--directory <dir>, -d <dir>` the directory to use as a working one, where the [output-files.md](../guides/output-files.md "mention") will be generated&#x20;
