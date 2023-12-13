# Use your own VPC on AWS

Stackmate deploys a VPC for every environment it handles. For example, if you have two environments, `production` and `staging`, you'll get two different VPCs when finished deploying.

By default, AWS has a limit of 5 VPCs per account, which means that you should either be re-using a VPC you've already used elsewhere, or reach out to the AWS support to have them increase your VPC quota.

In our example, we'll create and use a VPC that we'll add to our stackmate configuration.

* First, let's create a VPC on AWS: We can create the VPC using the Console by following [this document](https://docs.aws.amazon.com/vpc/latest/userguide/create-vpc.html#create-vpc-only), or use the AWS CLI by following [this one](https://docs.aws.amazon.com/vpc/latest/userguide/create-vpc.html#create-vpc-cli) instead.&#x20;
* Next, we need to grab the VPC ID and the Root IP used to create the CIDR blocks on the VPC
* In our example, we assume that the VPC ID is `vpc-1234567` and the CIDR block will be `19.0.0.0/24` which means that our root IP address is `19.0.0.0`
* We need to add a `provider` service on our configuration as follows:

{% code title=".stackmate/config.yml" %}
```yaml
---
state:
  bucket: ...
  lockTable: ...
environments:
  production:
    aws:
      type: provider
      vpcId: "vpc-1234567"
      rootIp: "19.0.0.0"
    app:
      type: application
      # ... the rest of the configuration here ...
```
{% endcode %}

What stackmate will do next then, is to import the vpc specified, and use this as the reference VPC for your AWS services
