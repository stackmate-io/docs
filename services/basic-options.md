# Basic Options

Every service on a stackmate configuration, should have a unique name and can be described with the following attributes:

* `type` - **required** - The service's type. It should be one of the services available
* `region` - the region to deploy the service. If not provided, the default configuration for the project's [`region`](../configuration/region.md) is used.
* `links` - A list of services that are inter-connected. For example a `mysql` service could be linked to the `application` service in order to allow incoming connections from the `application` service.
* `profile` - A pre-made profile to use for the service. If not specified, the `default` profile is used for the service. You need to refer to every service separately in order to view the corresponding options available.
* `overrides` - An object with attributes to override the default profile with. Each service has its own profile and own overrides. You need to refer to every service separately in order to view the corresponding options available.

These configuration options are available across all services on stackmate, and each service may or may not provide additional attributes to be configured by.

### Services Available

Stackmate supports the following services:

* Database Services
  * [MariaDB](database-services/mariadb.md)
  * [MySQL](database-services/mysql.md)&#x20;
  * [PostgreSQL](database-services/postgresql.md)
* Cache Services
  * [Memcache](cache-services/memcache.md)
  * [Redis](cache-services/redis.md)

You can find all the available options for every service on corresponding service page
