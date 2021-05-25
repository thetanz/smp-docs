# Changelog
All notable changes to this project will be documented in this file.
<!-- theme: info -->
>The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Added
- SubscriptionMgt: SetQuantity

## [1.1.1.0] `(2021-05-13)`
### Added
- Connect: Platform connected version allows self-onboarding for publishers
- SubscriptionMgt: GetQuantity
- Payment Screen: Total Amount to Pay
- Subscription States: Pastdue, Incomplete, Incomplete_Expired, Unpaid, Canceled
- Environments\Tenant Limit: per customer
- Daily/Weekly: new payment intervals supported 
### Changed
- Intro Screen UX redesign and no "accept" condition required
- Notifications Action: "Skip for today" to "Remind me later"
- Customer ID moved to private storage
- Common v1.1.1.0: New version with better security features
### Fixed
- Version 17 Assisted Setup layout
- Assisted Setup sign-out message
- Prorated upcoming payment data & formats 
- Upcoming invoice data cache
- Ability to skip payment method setup
## [1.0.5.0] `(2021-01-13)`
### Added
- Support all [Stripe TaxID types](https://stripe.com/docs/billing/customer/tax-ids#supported-tax-id)
- Contact Us action
- Display Terms of Conditions & Privacy Policy only if publisher defined
- Moving to v14 (Part 1) (StripeAPI_SM_TSL, Subscriber_SM_TSL, Notifier_SM_TSL)
- Translations: cs-CZ
### Fixed
- Country Code is in ISO Format
- Move Organisation Name to a Account Info Screen
- Changes to using test API keys to access live mode objects in the Stripe API
## [1.0.4.0] `(2020-12-13)`
### Added
- "VAT Registration No." validation now on Billing Info screen
- Upgrade to Stripe API version 2020-08-27
- Automatic Pagination
### Changed
- Name: _Exclude_SubscriptionMgt to SubscriptionMgt
- SubscriptionMgt: RequestMockingByKey to RequestMocking
- SubscriptionMgt: AuthorizeMockingByKey to AuthorizeMocking
- SubscriptionMgt: GetCurrentPlanName to GetPriceName
- SubscriptionMgt: ShowProductNotification to ShowNotification
- SubscriptionMgt: Parameter: SetMock(...,ProductPlanName) to SetMock(...,PriceName)

## See Also
- [Getting Started](../GettingStarted.md)
- [Security & Privacy](../Overview/Security&Privacy.md)
- [Contribution](../Contributing.md)