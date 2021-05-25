# Getting Started
This is a simple guide to get started with Subscription Management. Follow all the steps or jump to where you are in the process.
## 1. Connect your Stripe Account
<img align="right" src="https://www.belcar.fi/wp-content/uploads/2020/10/Stripe-wordmark-slate_sm-2.png" />

Subscription Management uses your Stripe account as a backend for all data. All your products as well as future customers and subscriptions will be stored and handled within Stripe.

<!-- theme: warning -->
> Subscription Management will have full access to your Stripe account. Due to this, we recommended a separate account is provisioned solely for this purpose.

<a href="https://smp.365extensions.com/forms/account" style="border-bottom-style:none;padding:10px 90px;background-image:url('https://dabuttonfactory.com/button.png?t=Connect+with+Stripe&f=Open+Sans-Bold&ts=14&tc=fff&hp=23&vp=14&w=180&h=38&c=4&bgt=unicolored&bgc=635bff')"></a>
## 2. Setup Stripe Product & Price
Subscription Management use [Stripe Product](https://stripe.com/docs/billing/prices-guide) to represent Publisher's proposition to customers. Please follow [documentation from Stripe](https://support.stripe.com/questions/how-to-create-products-and-prices) to set it up. As for now Subscription Management supports [Standard](https://stripe.com/docs/billing/subscriptions/model#package-standard-pricing), [Package](https://stripe.com/docs/billing/subscriptions/model#package-standard-pricing) and [Graduated](https://stripe.com/docs/billing/subscriptions/model#tiered-billing) pricing models. [Volume ("metered")](https://stripe.com/docs/billing/subscriptions/model#licensed-and-metered) one is in a [pipeline](https://github.com/thetanz/smp-docs/issues/14). 

> To extend your product pricing options (by currencies and billing intervals), just add a new price with a same name. Please check our [Stripe Schema](StripeSchema.md#product) documentation to get more information about how Stripe configuration implemented in Subscription Management. 

## 3. Installing dependencies
<img align="right" src="https://www.plantuml.com/plantuml/png/SoWkIImgAStDuOgEp2yjKd2jA4dDAyxCpujLqDMrKuWEBaqgJYxAB2W12lccbyHoEQJcfG2L0m00" />
Subscription Management is a separate extension which you use as a dependency for each extension you would like to monetize.

1. <a href="https://smp.365extensions.com/forms/install">Get Subscription Management</a> extension into your development environment.
2. Add a dependency to your extension's `app.json`.
```json
"dependencies": [
   ...
   {
      "id": "6717135a-d80c-4a63-8a3a-5ded6717135a",
      "publisher": "Theta Systems Limited",
      "name": "SubscriptionMgt",
      "version": "1.1.1.0"
    }
]
```
## 4. Basic Integration
For Subscription Management to be able to handle your extension monetization, it should be registered using [TryAddProduct API](References/SubscriptionMgt.md#tryaddproduct-method). We recommend to execute it during installation\upgrade of your extension. Example: 
<!--
type: tab
title: SubscriptionMgtProxy.Codeunit.al
-->
```sql
codeunit 50000 SubscriptionMgtProxy
{
    [NonDebuggable]
    internal procedure AddProduct()
    var
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        Info: ModuleInfo;
        TryAddProductErr: Label 'Failed to register product.';
    begin
        if NavApp.GetCurrentModuleInfo(Info) then
            if SubscriptionMgt.TryAddProduct(
                GetSecret('StripeSecretKey'),
                GetSecret('StripePublishableKey'),
                Info,
                GetSecret('StripeProductID'))
            then
                exit;
        LogError('SubscriptionMgtProxy-0001', TryAddProductErr)
    end;

    [NonDebuggable]
    local procedure GetSecret(Name: Text) Result: Text
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        GetSecretErr: Label 'Failed to get ''%1'' secret.', Comment = '%1 - Secret Name';
    begin
        // TODO: Can be replaced with your own secret provider
        if SecretProvider.TryInitializeFromCurrentApp() then
            if SecretProvider.GetSecret(Name, Result) then
                exit;
        LogError('SubscriptionMgtProxy-0002', GetSecretErr)
    end;

    local procedure LogError(EventId: Text; Message: Text)
    var
        CustDimension: Dictionary of [Text, Text];
    begin
        // TODO: Can be replaced with Error if installation error is acceptable.
        LogMessage(
            EventId,
            Message,
            Verbosity::Critical,
            DataClassification::EndUserPseudonymousIdentifiers,
            TelemetryScope::ExtensionPublisher,
            CustDimension)
    end;
}
```
<!--
type: tab
title: InstallExt.Codeunit.al
-->
```sql
codeunit 50001 InstallExt
{
    Subtype = Install;

    trigger OnInstallAppPerDatabase()
    var
        SubscriptionMgtProxy: Codeunit SubscriptionMgtProxy;
    begin
        SubscriptionMgtProxy.AddProduct()
    end;
}
```
<!--
type: tab
title: UpgradeExt.Codeunit.al
-->
```sql
codeunit 50002 UpgradeExt
{
    Subtype = Upgrade;

    trigger OnUpgradePerDatabase()
    var
        SubscriptionMgtProxy: Codeunit SubscriptionMgtProxy;
    begin
        SubscriptionMgtProxy.AddProduct()
    end;
}
```
<!-- type: tab-end -->

> To block your customers from using your application without an account you can use a combination of [IsActive](References/SubscriptionMgt.md#isactive-method)/[ShowNotification](References/SubscriptionMgt.md#shownotification-method) within your application UX entry points or use them to control extension specific ApplicaitonArea if such has been defined. 

## See Also
- [SubscriptionMgt_SM_TSL Reference](References/SubscriptionMgt.md)
- [Security & Privacy](Overview/Security&Privacy.md)
- [FAQ](FAQ.md)