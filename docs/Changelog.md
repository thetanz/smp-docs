---
sidebar_position: 998
---
# Changelog
All notable changes to this project will be documented in this file.
:::info
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).
:::
## [Unreleased]
### Added
- SubscriptionMgt: GetProductLines
- SubscriptionMgt: SetProductLines
- SubscriptionMgt: OnLookupProductLines
### Changed
- SubscriptionMgt: GetQuantity to CountProductLines
### Fixed
- Notification for pastDue status [#21](https://github.com/thetanz/smp-docs/issues/21)
- System refresh trial with second product subscription created [#23](https://github.com/thetanz/smp-docs/issues/23)
- Clear Accountdata when Parent App is uninstalled
## 1.3.11.0 - `2023-05-02`
### Fixed
- Code Warnings
### Changed
- VIEW_SM_TSL now extends "System App - Basic" instead of "COMMON_CO_TSL"
### Deprecated
- "EXT SETUP TSL" User Group
## 1.3.9.0 - `2023-01-24`
### Changed
- Dependency to Common 1.5.2.0
### Fixed
- [Trial expiers before Payment](https://feedback.365extensions.com/bc/p/trial-expiers-before-payment)
## 1.3.8.0 - `2022-12-23`
### Fixed
- [Don't default Currency Code](https://feedback.365extensions.com/bc/p/dont-default-currency-code)
- [Trial notifications with payment method defined](https://365extensions.canny.io/bc/p/trial-notifications-with-payment-method-defined)
- German translation
- Language independent DateFormula for upcoming invoice handling
- [Subscription with failed payment won't retry on a new card](https://feedback.365extensions.com/bc/p/subscription-with-failed-payment-wont-retry-on-a-new-card)
## 1.3.7.0 - `2022-10-06`
### Fixed
- Account Product permission error
## 1.3.6.0 - `2022-07-07`
### Fixed
- Select a product plan sorting [#30](https://github.com/thetanz/smp-docs/issues/30)
## 1.3.1.0 - `2021-11-16`
### Added
- OAuth Fallback to "Tenant" Auth (Cloud-Only) [#17](https://github.com/thetanz/smp-docs/issues/17)
### Fixed
- IsActive is true when status in 'active', 'trialing', 'past_due', 'incomplete', 'incomplete_expired'
## 1.2.1.0 - `2021-10-08`
### Fixed
- Country Code depends on ISO Code
- FR-local: Integer evaluate issue
## 1.2.0.0 - `2021-09-13`
### Added
- New SETUP and VIEW permission sets
### Fixed
- Cannot finish with payment method exists [#22](https://github.com/thetanz/smp-docs/issues/22)
## 1.1.1.0 - `2021-05-13`
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
## 1.0.5.0 - `2021-01-13`
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
## 1.0.4.0 - `2020-12-13`
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
