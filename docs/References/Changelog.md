# Changelog
All notable changes to this project will be documented in this file.
<!-- theme: info -->
>The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Added
- SubscriptionMgt: SetQuantity
- SubscriptionMgt: GetQuantity
- Payment Screen: Total Amount to Pay
- Handle Pastdue, Incomplete, Incomplete_Expired, Unpaid, Canceled
- Control Limits per Customer
### Fixed
- Version 17 Assisted Setup layout
- More informative Signout Message
- Prorated upcomming payment data fixed + formats 
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
