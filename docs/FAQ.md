# FAQ

## How to start using Subscription Management? 
Subscription Mgt. (SM) is a separate extension which you use as a dependency for each extension you would like to monetize. During the publisher onboarding process, we will provide a development version to setup integration. When integration is defined, we will provide an AppSource version dependency references which should be used for your AppSource publication. [More info](./GettingStarted.md).
## Which versions of NAV/BC Subscription Management supports? 
Version 15 is currently the lowest supported version. We are planning to support version 14 within a publisher RC, this will be released in 2021 Q1. 
## How to enable sales though partners? 
Currently we offer the ability to track a partner reference within SM. We are planning to support automatic partner billing in future releases. Currently we are collecting requirements to make sure that partner engagement scenarios are sufficiently covered. 
## Which Stripe pricing models is possible to use with Subscription Mgt.? 
Fixed price and per-seat (per UOM) pricing is supported (https://stripe.com/docs/billing/subscriptions/model#common-models). Any metered models will be supported in 2021 Q1. 
## What customer information is collected by Subscription Mgt.? 
There are three types of information collected: 
1.	**User Identity**: User SID, User Email, User First/Last Name. This information is used by SM for authorization purposes. It can only be used by a publisher for service availability notifications. 
2.	**Environment Info**: Tenant ID, Instance Name. This information is used by SM for environment usage control. It should not be used by publisher for any purposes. 
3.	**Billing Info**: Billing Address, Billing Email, Payment Method. This information is used by Stripe for billing purposes. It should not be used by publisher for any other purposes then billing. This information will be collected only for paid subscribers.
## Is it possible to block a customer from using an app if an invoice payment overdue? 
SM regularly synchronizes customer’s subscription status with Stripe. Application will be able to get this status though API and block users access if necessary. 
## Is it possible to use Subscription Mgt. for on-prem installation? 
SM is available to be used with any environment with network connectivity.

