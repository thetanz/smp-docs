---
sidebar_position: 5
---
# FAQ
## How to start using Subscription Management? 
Subscription Management is a separate extension which you use as a dependency app for each extension you would like to monetize. During the publisher onboarding process, we will provide a development version to set up your integration. When the integration is defined, we will provide an AppSource version dependency reference that needs to be used for your AppSource publication.
## Which versions of Dynamics NAV/Business Central are supported by Subscription Management? 
Version 15 is currently the lowest supported version. There are no plans to support any lower version. 
## How to enable sales through partners? 
Currently, we offer the ability to track a partner reference within Subscription Management. We are planning to support automatic partner billing in future releases. We are collecting requirements to make sure that partner engagement scenarios are sufficiently covered. 
## Which Stripe pricing models are possible to use with Subscription Management? 
Fixed price and per-seat (per UOM) pricing are supported (https://stripe.com/docs/billing/subscriptions/model#common-models). Any metered models are currently not supported, but it is on our roadmap. 
## What customer information is collected by Subscription Management? 
There are three types of information collected: 
1.	**User Identity**: User SID, User Email, User First/Last Name. This information is used by Subscription Management for authorization purposes. It can only be used by a publisher for service availability notifications. 
2.	**Environment Info**: Tenant ID, Instance Name. This information is used by Subscription Management for environment usage control. It should not be used by the publisher for any purposes. 
3.	**Billing Info**: Billing Address, Billing Email, Payment Method. This information is used by Stripe for billing purposes. It should not be used by the publisher for any other purposes than billing. This information will be collected only for paid subscribers.
## Is it possible to block a customer from using an app if invoice payment is overdue? 
Subscription Management regularly synchronizes the customer’s subscription status with Stripe. Your app will be able to get this status through the API, which you can use to block users access if desired. 
## Is it possible to use Subscription Management for on-premise installations? 
Yes, Subscription Management is available in any environment with Internet connectivity.