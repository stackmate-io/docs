# state

The `state` configuration option, is an `Object` which defines where the [Terraform State](https://www.terraform.io/language/state) should be stored after each deployment.&#x20;

### Accepted values

#### AWS S3 Bucket

For storing the state on an AWS S3 bucket, you need to specify an object containing the following attributes:

* `bucket` - The name for the bucket to use. It should comply with the guidelines that AWS provides for naming a bucket.
* `lockTable` - The DynamoDB table to use for state locking. If you don't want to use state locking, feel free to leave this option out.
* `statePath` - _Optional_ - The name of the Terraform state file to use. By default it's `stackmate.tfstate` and it should always end in `.tfstate`
* `provider` - _Optional_ - It should be set to `aws`. _You don't have to specify this value if the root configuration option for `provider` is set to `aws`._

### Examples

#### Storing your state on a private, encrypted AWS S3 bucket with state locking

```yaml
...
state:
  bucket: my-awesome-project-state-bucket
  lockTable: stackmate-state-lock
  statePath: my-cool-project.tfstate
  provider: aws # you don't have to specify this if the default provider is set to "aws"
```
