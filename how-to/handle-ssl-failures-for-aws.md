# Handle SSL failures for AWS

As described on the [Application service](../configuration/application-services.md#what-you-get-when-introducing-this-service-to-your-configuration) configuration section, stackmate will add an SSL certificate for your environment, that will handle the domain names you specified in your project.&#x20;

### Using email validation

Stackmate will instruct AWS to try and validate the certificate using `email` by default, where you will get prompted to approve the validation request or not. What you need to know beforehand is the following:

* AWS will email the `administrator`, `hostmaster`, `postmaster`, `webmaster` and `admin`  inboxes at your domain so it's necessary to have at least one of these inboxes available, or a catch-all inbox at hand.
* The approval should be done within 5 minutes after you get the email, otherwise the deployment will fail
* There have to be a few CAA DNS records in your domain name so that AWS can issue the certificate for you as described in [this document](https://docs.aws.amazon.com/acm/latest/userguide/setup-caa.html). Our experience shows that just setting a CAA record for `amazon.com` will work, but we can't guarantee that.

### Using DNS validation

Alternatively, you can also use DNS validation for your SSL certificates but the domain needs to be active and the name servers for it need to already be pointing to AWS. What you need to do is the following:

* Create a Hosted Zone for your domain name (eg. stackmate.io) on Route53 as described in [this document](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/CreatingHostedZone.html).
* Get the NS records and set them as your nameservers on your domain registrar.

Stackmate will then attempt to validate whether the DNS records are active and use that as the validation method so that no manual action will be required

