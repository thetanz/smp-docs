---
sidebar_position: 2
---
# Stripe Schema
Subscription Management uses Stripe to manage different plans and payments processing. Below you will find details of different entities of Stripe that have been utilized and integrated within Subscription Management.
## Account
### Name
The customer gets to see this name as publisher name throughout Business Central. Preferably Name should be similar to your AppSource publisher name.
#### Setup in Stripe UI
1. Go to [Stripe account details](https://dashboard.stripe.com/settings/account)
2. Fill in the Account name under the account settings section and save.
![](./../images/StripeSchema_AccountName.png)
#### Where used in Subscription Management 
It is used in multiple places through the assisted setup and notifications.
### Support Email
This email will be used by customers for contacting the publisher. 
#### Setup in Stripe UI
1. Go to [Stripe account details](https://dashboard.stripe.com/settings/account)
2. Fill in the support email under the "Pubic business information" section and save.
![](./../images/StripeSchema_SupportEmail.png)
#### Where used in SM
Available as "Contact Us" button on all the sign-up "Assisted Setup" pages. 
![](./../images/StripeSchema_SupportEmail_ContactUs.png)

![](./../images/StripeSchema_SupportEmail_Email.png)
## Product
### ID
Unique identifier for the product in Stripe. Automatically generated by Stripe when a new product is added.
#### Setup in Stripe UI
Go to the products list page and click on the desired product to view the ID.
![](./../images/StripeSchema_Product_ID_StripeUI.png)
#### Where used in SM
Used by "Subscription Management" to uniquely identify the product in Stripe during API calls.
### Name
"Name" represents the name of the publisher's app in Stripe and Business Central. Subscription Management uses this "Name" to refer to the publisher's app.
#### Setup in Stripe UI
1. Go to Stripe dashboard and products section then click on "Add products"
![](./../images/StripeSchema_ProductName_SM_AddProducts.png)

2. Fill in the Account name under the account settings section and save.
![](./../images/StripeSchema_ProductName.png)
#### Where used in SM
It is used in multiple places through the assisted setup and notifications to identify the App.
![](./../images/StripeSchema_ProductName_SM1.png)

![](./../images/StripeSchema_Product_Name_SM_Name.png)
### Unit
Unit of measure for your product. Defines how you sell your product. e.g. (per) tenant, user or usage etc.
#### Setup in Stripe UI
Under "Product information" and "Additional options" section
![](./../images/StripeSchema_ProductUnit.png)
#### Where used in Subscription Management 
It is used on the assisted setup page.
![](./../images/StripeSchema_Product_Unit_SM.png)
## Price
### Name
Unique identifier for the Price in Stripe.
#### Setup in Stripe UI
Defined as "Price Description" when setting up a new price in Stripe.
![](./../images/StripeSchema_Price_Name_StripeUI.png)
#### Where used in SM
Equivalent to Plan in Assisted Setup
![](./../images/StripeSchema_Price_Name_StripeUI_ChoosePlan.png)

![](./../images/StripeSchema_Price_Name_StripeUI_SelectPlan.png)
### Description
A brief information about the product. 
#### Setup in Stripe UI
Setup from "Edit metadata" action from "Product" details page. Default metadata for Description is "description" (lower case). Multiple languages are supported. Please suffix "description" with _LocaleCode for other languages.
![](./../images/StripeSchema_Product_MetadataEdit_StripeUI.png)

![](./../images/StripeSchema_Product_Description_StripeUI.png)

#### Where used in SM
Reflects under Value field on "Assisted Setup", "Select a product plan" step. 
![](./../images/StripeSchema_Product_Description_SM.png)
### Currency
Represents currency associated with the price plan. Currently "Subscription Management" supports NZD, USD, AUD, GBP and EUR currencies.
#### Setup in Stripe UI
Defined as "Currency" when setting up a new price in Stripe.
![](./../images/StripeSchema_Price_Currency_StripeUI.png)
#### Where used in SM
When signing up for the "Subscription Management", the user is provided with a list of currencies that are supported. The user needs to select a currency from the list of supported currencies. The selected currency is used to filter plans as per matching 'currency code" from account information.
![](./../images/StripeSchema_Price_Currency_SM_Signup.png)

![](./../images/StripeSchema_Price_Currency_SM_Filter.png)
### Billing Period
Represents length of time between two billing cycle. Currently "Subscription Management" supports "Monthly" and "Yearly". We will be happy to support more on publishers' request.
#### Setup in Stripe UI
Defined as "Billing Period" when setting up a new price in Stripe.
![](./../images/StripeSchema_Product_BillingPeriod_StripeUI.png)
#### Where used in Subscription Management 
It appears on "Select a product plan" as "Payment Interval" during sign-up process.
![](./../images/StripeSchema_Product_BillingPeriod_SM.png)
### Trial Period
Specifies the free number of days a customer have. AppSource requires a minimum of 30 days trial period. Subscription Management maintains the remaining trial period days for the customer. It starts notifying 7 days, 3 days and 1 day before the trial expires and asks for payment method details. If payment method details are not entered before the trial period has expired then the subscription is marked as "Passed due" and the subscription will not be active.
#### Setup in Stripe UI
Defined as "Trial period" when setting up a new price in Stripe.
![](./../images/StripeSchema_Product_TrialPeriod_StripeUI.png)
#### Where used in Subscription Management 
Used to track "Plan Details" and "Next Payment" details.
![](./../images/StripeSchema_Product_TrialPeriod_SM.png)
## Tax Rate
Defines how customers from different regions should be taxed.
### Region
"Subscription Management" checks the tax rates you have defined in Stripe for different regions; and then compares it with the region of the customer during the sign-up process.
#### Setup in Stripe UI
Setup under Tax rates section.
![](./../images/StripeSchema_TaxRate_StripeUI.png)
#### Where used in Subscription Management 
If a tax rate exists for the customer's region then he/she must provide his "Tax Registration No." during sign-up and is charged tax accordingly.
![](./../images/StripeSchema_TaxRate_UserRegion_SM.png)

![](./../images/StripeSchema_TaxRate_SM.png)