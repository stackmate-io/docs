# secrets

The `secrets` configuration option, is an `Object` which defines the storage option for your stack's secrets. The same storage is used for all stages available in the stack.

### Accepted values

#### AWS Secrets Manager

For storing your secrets on AWS Secrets manager, you need to specify an object containing the following attributes:

* `provider` - It should be set to `aws`

The entire `secrets` block can be skipped if the project-wide `provider` is set to `aws`.

### Examples

#### Storing your state on AWS Secrets Manager

```yaml
...
secrets:
  provider: aws # you don't have to specify this if the provider is set to "aws"yaml
```
