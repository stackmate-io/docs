# stackmate deploy

{% hint style="info" %}
If you're looking to deploy every time you push a new commit, perhaps you might want to check our [Cloud](https://stackmate.io/cloud/) version out. We offer a **trial of 7 days** and **no credit card** is required.
{% endhint %}

The `stackmate deploy` command applies changes to an environment specified. It is responsible for deploying and modifying your infrastructure.

### Usage

```
stackmate deploy <environment> [-c configuration.yml -d working-directory]
```

### Arguments

* `<environment>` The environment to deploy

### Options

* `--configuration <file>, -c <file>` the configuration file to be used for this operation. By default `.stackmate/config.yml` is used
* `--directory <dir>, -d <dir>` the directory to use as a working one, where the [output-files.md](../appendix/output-files.md "mention") will be generated&#x20;
