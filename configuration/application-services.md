# Application Services

Stackmate supports Docker container images deployment on managed container services, like [AWS ECS](https://aws.amazon.com/ecs/)

### What you get when introducing this service to your configuration

* A managed container service running the container `image` specified with the `cpu` and `memory` restrictions you've applied. The service will run on the `port` specified in the configuration
* A DNS record to the value set as your `domain` in the configuration
* A load balancer routing HTTP and HTTPS traffic to the container
* An SSL certificate for the domain name(s) specified

### Required attributes

* `type` - **string** - It should be set to `application`
* `image` - **string** - The docker image to run, for example `stackmate/sample-nodejs-app:latest`. It should be anything that Docker can pull from (for example a public DockerHub repository)
* `port` - **number / Optional for non-web services** - The port that your web application runs on. If your application doesn't expose a port (for example it's a backend worker or something similar), feel free to leave this empty

### Optional attributes

* `cpu` - **number** - The vCPU units that your container runs on. Acceptable values are: `0.25`, `0.5`, `1`, `2`, `4`, `8` and `16`.
* `memory` - **number** - The GB of memory available that the container runs on. You can use `0.5` and any integer value between `1` and `120` but please keep in mind that cloud providers might introduce some restrictions:
  * Available AWS [CPU and Memory combinations](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/fargate-tasks-services.html#fargate-tasks-size)
* `domain` - **string** - The domain name to use for your service. It can be both top-level domains (eg. stackmate.io) or subdomains (eg. app.stackmate.io)
* `www` - **boolean** - Whether to add another DNS record that starts with`www` (eg. www.stackmate.io). Please note: This only applies when using a top-level domain name as `domain` (like eg. stackmate.io)

### Example configuration for an application container on AWS ECS

{% code title=".stackmate/config.yml" %}
```yaml
---
state:
  bucket: ...
  lockTable: ...

environments:
  production:
    nodejs-app:
      type: application
      image: stackmate/sample-nodejs-app:latest
      cpu: 0.5
      memory: 1
      port: 3000
      domain: stackmate.io
      # provider: aws # implied, since aws is the default provider
```
{% endcode %}

The example above will run a container of `0.5` vCPU, `1` GB of memory, that will expose port `3000` on AWS ECS Fargate. It will also create an application load balancer that will forward traffic to the container, using an auto-generated SSL certificate via ACM for `stackmate.io`. Finally, there will be a DNS record on Route53 with `stackmate.io` as the domain name, targeting the load balancer.
