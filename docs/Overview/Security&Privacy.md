# Security & Privacy
Subscription Management takes on the responsibility of connecting your application with your end-users. We've taken a number of steps to ensure the confidentiality of your data whilst it's entrusted with us.

We work in close collaboration with our [Security Team](https://theta.co.nz/cyber) to ensure our design and architecture meets and exceeds industry standards, with regular penetration tests validating our controls.

## Keeping your Stripe account safe
We use your [Stripe Secret Key](https://stripe.com/docs/keys#safe-keys) to authenticate to your Stripe Account and leverage this connection to facilitate  operations performed within Subscription Management.

This key provides full access to your Stripe account and can broker access to your customer data as well as any billing transactions. For these reasons, we recommend you follow the below safeguards:
1. Keep your Stripe Secret Key in a robust location such as [Azure's Key Vault](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-app-key-vault)) 
2. Mark any methods that work with secrets as [NonDebuggable](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods/devenv-nondebuggable-attribute)
3. Mark any object instances that works with secrets as accessible only within the application. Single instance codeunits may be used only if its **methods** are marked with [internal access modifier](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-using-access-modifiers) - the `internalsVisibleTo` setting declared within the applications JSON File should be blank to disallow **ANY** apps from accessing it.

**Subscription Management** keeps your Stripe Secret Key strongly encrypted through the use of server side encryption mechanisms, leveraging TLS 1.2 to ensure robust, encrypted transport to external parties.
## Keeping your and your customer data safe
Subscription Management (SM) collects and stores information from you and your customer. We classify this information into categories listed bellow and depends on each of this categories we applying a different storage and usage requirements:

Category | Description | Entered | Stored | Used 
-------- | ----------- | ------- | ------ | ----
**Publisher's Authentication Information** | Publisher's Stripe API Keys | By publisher using Subscription Mgt. API | Encrypted within Subscription Mgt. | By Subscription Mgt. to authorize your app with your Stripe account
**Publisher's Information** | Publisher's Stripe ID, name, support email, Stripe TAX ID, links to TOC and privacy policy | By publisher using Stripe UI | Public within Subscription Mgt. | By Subscription Mgt. to operate
**Customer's User Authentication Information** | Customer's user SIDs | By user using Subscription Mgt. Assisted Setup | Public within Subscription Mgt. | By Subscription Mgt. to authorize customer access to customer's account information
**Customer's User Information** | Customer's user email, first/last name | By user using Subscription Mgt. Assisted Setup | Private within Publisher's Stripe Account | By publisher for service availability notifications
**Customer's Authentication Information** | Customer's ID | By user using Subscription Mgt. Assisted Setup | Public within Subscription Mgt. | By Subscription Mgt. to authorize customer access to customer's account information
**Customer's Environment Information** | Customer's tenant ID and environment identifier | By user using Subscription Mgt. Assisted Setup | Private within Publisher's Stripe Account | By Subscription Mgt. to operate
**Customer's Billing Information** | Customer's billing address, email and payment method | By user using Subscription Mgt. Assisted Setup and Stripe Elements only for paid subscribers | Private within Publisher's Stripe Account | By Stripe to billing purposes
