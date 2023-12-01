# Basic Options

Every service on a stackmate configuration, should have a unique name and can be described with the following attributes:

#### Required attributes

* `type` - The service's type. It should be one of the services available

#### Optional attributes

* `region` - the region to deploy the service. If not provided, the default configuration for the project's [`region`](../configuration/region.md) is used.
* `links` - A list of services that are inter-connected. For example a `mysql` service could be linked to the `application` service in order to allow incoming connections from the `application` service.
* `externalLinks` - A list of IPs of resources not deployed by Stackmate, to allow outside connections from
* `profile` - A pre-made profile to use for the service. If not specified, the `default` profile is used for the service. You need to refer to every service separately in order to view the corresponding options available. You can browse the profiles available in our [repository](https://github.com/stackmate-io/stackmate/tree/main/src/services/providers/aws/profiles).
* `overrides` - An object with attributes to override the default profile with. Each service has its own profile and own overrides. You need to refer to every service separately in order to view the corresponding options available.

These configuration options are available across all services on stackmate, and each service may or may not provide additional attributes to be configured by.
