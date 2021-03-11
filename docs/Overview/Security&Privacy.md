# Security & Privacy
Subscription Management takes on the responsibility for connecting you with your app end-users. With this in mind we do our best to guarantee a keeping secrets private and ensure only confidential connection. We are working in close collaboration with our Security Team. Part of our security hardening processes is e.g. penetration testing to limit security vulnerabilities and risks in two attack surfaces: 
- **Within Platform**: Scenarios where person or service which has access to hosting platform would tries to gain access to your sensitive information or reuse your subscription on another environment.
- **Within Application**: Scenarios where another extension installed on a same environment tried gain access to your sensitive information.
## Keeping your Stripe account safe
Currently we are using your [Stripe Secret Key](https://stripe.com/docs/keys#safe-keys) as an authentication key to your Stripe Account as well as any operations that you can perform in Subscription Management. This key allows full access to your Stripe account including access to your customer data as well as your billing transactions. With this in mind, we list a set of requirements which should be applied to keep this key private:
1. **Publisher** should keep a Stripe Secret Key in secure location (for example in [Azure Key Vault](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-app-key-vault)) 
2. **Publisher** should mark all methods which works with secrets as [NonDebuggable](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods/devenv-nondebuggable-attribute)
3. **Publisher** should keep object instances which works with secrets accessible only within application. Single instance codeunits may be used only if its **methods** are marked with [internal access modifier](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-using-access-modifiers) and `internalsVisibleTo` setting in App JSON File should be blank to not allow **ANY** apps to access it.

**Subscription Management** keeps your Stripe Secret Key strongly encrypted in any environment using server side encryption mechanism. All communications with external services handled using TLS 1.2. 
## Keeping your and your customer data safe
Subscription Management (SM) collects and stores information from you and your customer. We classify this information into categories listed bellow and depends on each of this categories we applying a different storage and usage requirements:

Category | Description | Entered | Stored | Used 
-------- | ----------- | ------- | ------ | ----
**Publisher's Authentication Information** | Publisher's Stripe API Keys | By publisher using Subscription Mgt. API | Strongly encrypted within Subscription Mgt. | By Subscription Mgt. to authorize your app with your Stripe account
**Publisher's Information** | Publisher's Stripe ID, name, support email, Stripe TAX ID, links to TOC and privacy policy | By publisher using Stripe UI | Public within Subscription Mgt. | By Subscription Mgt. to operate
**Customer's User Authentication Information** | Customer's user SIDs | By user using Subscription Mgt. Assisted Setup | Public within Subscription Mgt. | By Subscription Mgt. to authorize customer access to customer's account information
**Customer's User Information** | Customer's user email, first/last name | By user using Subscription Mgt. Assisted Setup | Private within Publisher's Stripe Account | By publisher for service availability notifications
**Customer's Authentication Information** | Customer's ID | By user using Subscription Mgt. Assisted Setup | Public within Subscription Mgt. | By Subscription Mgt. to authorize customer access to customer's account information
**Customer's Environment Information** | Customer's tenant ID and environment identifier | By user using Subscription Mgt. Assisted Setup | Private within Publisher's Stripe Account | By Subscription Mgt. to operate
**Customer's Billing Information** | Customer's billing address, email and payment method | By user using Subscription Mgt. Assisted Setup and Stripe Elements only for paid subscribers | Private within Publisher's Stripe Account | By Stripe to billing purposes
