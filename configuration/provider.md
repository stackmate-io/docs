# provider

The `provider` configuration option is the default cloud provider to use for services launched, state and secret storage unless specified otherwise. This practically means that the value you specify for the `provider` configuration option is the only one required across the configuration file, if you plan to use only one provider for everything: services, state and secrets storage.

### Accepted values

Accepted cloud providers are:

* `aws` - Allows use of the AWS (Amazon Web Services) provider

_Note: We plan to support more cloud providers in the near future._
