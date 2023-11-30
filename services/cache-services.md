# Cache Services

Stackmate offers infrastructure deployment for major cache services, the following configuration is supported:

### Required attributes

* `type` - **string** - It should be either `redis` or `memcached`

### Optional attributes

* `size` - **string** - The instance size. Should be one of the instances the provider has available
* `version` - **string** - The cache version to use. These are dictated by the cloud provider (eg. AWS) and it's one of the versions they currently support.
* `storage` - **number** - The size of the storage space in Gigabytes
* `port` - **number** - The port to use. By default, `6379` is assigned to `redis` and `11211` is assigned to `memcached`
* `monitoring` - **object** - Any monitoring options available for the service. Example configuration is shown below

The typical [basic-options.md](basic-options.md "mention") apply here too.

### Example configuration

```yaml
# ... the rest of the configuration ...
environments:
  production:
    # ... more services ...
    my-cache:
      type: redis
      provider: aws         # optional when your provider's set to aws
      region: eu-central-1  # optional if you have a region set for the project
      size: cache.t3.micro
      storage: 30
      version: 7.0
      monitoring:
        urls:
          - https://a-webhook-to-get-alerted-by.com
        emails:
          - cache-alerts@mywebsite.com
```

