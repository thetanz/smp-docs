# Security & Privacy
Subscription Management takes on the responsibility of connecting your application with your end-users. We've taken a number of steps to ensure the confidentiality of your data whilst it's entrusted with us.

We work in close collaboration with our [Security Team](https://theta.co.nz/cyber) to ensure our design and architecture meets and exceeds industry standards, with regular penetration tests validating our controls.

## Keeping your Stripe account safe
We use your [Stripe Secret Key](https://stripe.com/docs/keys#safe-keys) to authenticate to your Stripe Account and leverage this connection to facilitate  operations performed within Subscription Management.

This key provides full access to your Stripe account and can broker access to your customer data as well as any billing transactions. For these reasons, we recommend you follow the below safeguards:
1. Keep your Stripe Secret Key in a robust location such as [Azure's Key Vault](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-app-key-vault)) 
2. Mark any methods that work with Secrets as [NonDebuggable](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods/devenv-nondebuggable-attribute)
3. Mark any object instances that works with Secrets as accessible only within the application. Single instance codeunits may be used only if its **methods** are marked with [internal access modifier](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-using-access-modifiers) - the `internalsVisibleTo` setting declared within the applications JSON File should be blank to disallow **ANY** apps from accessing it.

**Subscription Management** keeps your Stripe Secret Key strongly encrypted through the use of server side encryption mechanisms, leveraging TLS 1.2 to ensure robust, encrypted transport to external parties.
## Keeping your and your customer data safe

Subscription Management (SM) collects and stores information from you and your customer. We classify this information into the categories listed below and depending on the category, we apply different storage and usage requirements:

Category | Description | Entered | Stored | Used 
-------- | ----------- | ------- | ------ | ----
**Publisher's Auth Info** | Publisher's Stripe API keys | By publisher using SM API | Encrypted within SM | By SM to authorize your app with your Stripe account
**Publisher's Info** | Publisher's Stripe ID, name, support email, Stripe TAX ID, links to TOC and privacy policy | By publisher using Stripe UI | Public within SM | By SM to operate
**Customer's User Auth Info** | Customer's user SIDs | By user using SM Assisted Setup | Public within SM | By SM to authorize customer access to customer's account information
**Customer's User Info** | Customer's user email, first/last name | By user using SM Assisted Setup | Private within Publisher's Stripe Account | By publisher for service availability notifications
**Customer's Auth Info** | Customer's ID | By user using SM Assisted Setup | Public within SM | By SM to authorize customer access to customer's account information
**Customer's Environment Info** | Customer's tenant ID and environment identifier | By user using SM Assisted Setup | Private within Publisher's Stripe Account | By SM to operate
**Customer's Billing Info** | Customer's billing address, email and payment method | By user using SM Assisted Setup and Stripe Elements only for paid subscribers | Private within Publisher's Stripe Account | By Stripe to billing purposes

Please check a complete [Terms and Conditions](https://www.theta.co.nz/media/3805/terms-and-conditions-for-appsource-apps-for-business-central.pdf) and [Privacy Policy](https://www.theta.co.nz/contact-us/privacy-policy/) for a more detailes.

## See Also
- [Getting Started](../GettingStarted.md)
- [FAQ](../FAQ.md)

![Analytics](https://ga-beacon.appspot.com/G-P2LEDQJP25/smp/Overview/SecurityPrivacy?pixel)