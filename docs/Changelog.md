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

## 27.1.3.0 `2026-06-08`
### Changed
- **Media Preview is now disabled by default.** Previously, clicking a file in the Document Attachments FactBox would always attempt to open the in-browser previewer. This behaviour is now opt-in and can be enabled via the new **File Preview Settings** action, which appears on both the Document Attachment Details page and the Document Attachments FactBox. The setting can be managed globally (Super User required) or on a per-user basis, with per-user preferences always taking priority over the global setting.
- **File extension now takes priority over Tenant Media MIME type when selecting the viewer.** Previously, the MIME type stored against the Tenant Media record was used first to determine how to render a file. Where attachments were added programmatically, it was possible for that value to be set incorrectly or left as a generic type, causing files such as PDFs to be rendered incorrectly. The app now trusts the file extension to determine the appropriate viewer and only falls back to the Tenant Media MIME type when no extension is present.

## 27.1.2.0 `2026-05-25`
### Fixed
- Fixed customers with more than 10 subscriptions losing rows after sign-out/sign-in. SyncCustomerData was reading from the embedded `customer.subscriptions` list, which Stripe caps at 10 items. It now uses the paginated subscriptions endpoint, which returns all subscriptions regardless of count.

## 27.1.1.0 `2026-05-20`
### Changed
- Enforced minimum version of subscription management

## 27.1.0.0 `2026-05-19`
### Fixed

- Fixed Stripe subscription paging: increased limit to 100 and corrected last-item index for paginated responses
- Fixed SyncCustomerData incorrectly marking all Account Product records for deletion (now only marks non-app-registered rows)
- Fixed duplicate subscriptions not being resolved during sign-in, causing stale or conflicting subscription state
- Fixed subscription selection logic to prioritise active status over creation date
### Added

- Added FindAndUpdateExistingSubscriptionIDByProduct to detect and reuse existing Stripe subscriptions during assisted setup
- Added duplicate subscription resolution during sign-in (cancels trialling when non-trialling exists; never cancels active)
### Changed

- VIEW_SM_TSL now extends "System App - Basic" instead of "COMMON_CO_TSL"
- LoginCustomer now fetches Stripe subscriptions once per sign-in instead of once per product (performance improvement)


## 26.0.0.0 - `2025-10-20`

### Removed 
- Removed obsoleted methods in the common library extension.

## 25.1.4.0 - `2025-09-07`
### Changed
- The dependency for Open Feature has been removed.
- Handled breaking changes relating to Business Central 2025 Wave 2 (BC27)

## 25.0.0.0 - `2025-01-21`

### Fixed 
- When updating your subscription the following error would be raised on versions greater than 25.1: "Unsupported Media Type Status Code: 415"

## 1.4.10.0 - `2024-08-01`
### Changed
- Added support for archived prices on existing subscriptions

## 1.4.9.0 - `2024-07-11`
### Fixed
- Resolved an issue with the Azure Key Vault Initialisation - the issue was caused by 1.4.8.0.
## 1.4.8.0 - `2024-07-11`
### Changed
- Implemented session cache to reduce the number of API calls
- Allow using apps in a SaaS Sandbox without signing up for an account. Note: Some apps require minor refactoring to take advantage of this.

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
