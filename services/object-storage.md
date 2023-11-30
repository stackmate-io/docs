# Object storage

Stackmate offers infrastructure deployment for object storage, the following configuration is supported:

### Required attributes

* `type` - **string** - It should be set to `objectstore`
* `buckets` - **array** - a list of objects with the following attributes:
  * `name` - **string, required** - the bucket's name
  * `versioning` - **boolean, optional** - whether to enable versioning for objects, `false` by default
  * `encrypted` - **boolean, optional** - whether objects are encrypted in the bucket, `false` by default
  * `publicRead` - **boolean, optional** - whether the objects are publicly available for reading, `false` by default

The typical [basic-options.md](basic-options.md "mention") apply here too.

### Accessing the bucket

{% hint style="info" %}
Please read the following if you plan to grant programmatic access to your buckets
{% endhint %}

Stackmate creates a user in your cloud that is able to access and manage objects in the newly created bucket and a policy is assigned to it. The user does not have any credentials assigned to it, so you should log in through your console and create them yourself.

### Example configuration

```yaml
# ... the rest of the configuration ...
environments:
  production:
    # ... more services ...
    my-storage:
      type: objectstore
      buckets:
        - name: my-super-bucket
          versioning: true
        - name: my-other-awesome-bucket
          encrypted: true
```

