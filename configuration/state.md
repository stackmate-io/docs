# state

The `state` configuration option, is an `Object` which defines where the [Terraform State](https://www.terraform.io/language/state) should be stored after each deployment.&#x20;

### Accepted values

#### AWS S3 Bucket

For storing the state on an AWS S3 bucket, you need to specify an object containing the following attributes:

* `bucket` - The name for the bucket to use. It should comply with the guidelines that AWS provides for naming a bucket.
* `provider` - It should be set to `aws`. _You don't have to specify this value if the root configuration option for `provider` is set to `aws`._

### Examples

#### Storing your state on a private, encrypted AWS S3 bucket

```yaml
...
state:
  bucket: my-awesome-project-state-bucket
  provider: aws # you don't have to specify this if the provider is set to "aws"yaml
```
