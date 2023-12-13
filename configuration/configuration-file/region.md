# region

Same with the [`provider`](provider.md) configuration option, the `region` acts as a default for services to be launched with stackmate. Specifying a `region` means every service deployed with stackmate uses that region as a default, which basically means that you don't have to specify it in the services themselves

### Accepted values

The values accepted for the `region` configuration attribute, depend on the value you specified for the `provider` attribute, meaning that the `region` should be one of the regions that the cloud provider you specified in the `provider` uses.

For reference, you can check out the regions every cloud provider uses:

* For the `aws` provider: [https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)
