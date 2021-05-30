# Getting Started
This guide shows how easy it is to get started with Subscription Management. Follow all the steps or jump to where you are in the process.
## 1. Connect your Stripe Account
<img align="right" src="https://www.belcar.fi/wp-content/uploads/2020/10/Stripe-wordmark-slate_sm-2.png" />

Subscription Management uses your Stripe account as a backend for all data. All your products as well as future customers and subscriptions will be stored and handled directly within Stripe.

<!-- theme: warning -->
> The Subscription Management app will have full access to your Stripe account. If you already have a Stripe account then we recommended you create a separate account solely for this purpose.

<a href="https://smp.365extensions.com/forms/account" style="border-bottom-style:none;padding:10px 90px;background-image:url('https://dabuttonfactory.com/button.png?t=Connect+with+Stripe&f=Open+Sans-Bold&ts=14&tc=fff&hp=23&vp=14&w=180&h=38&c=4&bgt=unicolored&bgc=635bff')"></a>
## 2. Setup Stripe Product & Price
Subscription Management uses [Stripe Product](https://stripe.com/docs/billing/prices-guide) to represent Publisher's proposition to customers. Please follow [documentation from Stripe](https://support.stripe.com/questions/how-to-create-products-and-prices) to set it up. As for now Subscription Management supports [Standard](https://stripe.com/docs/billing/subscriptions/model#package-standard-pricing), [Package](https://stripe.com/docs/billing/subscriptions/model#package-standard-pricing) and [Graduated](https://stripe.com/docs/billing/subscriptions/model#tiered-billing) pricing models. [Volume ("metered")](https://stripe.com/docs/billing/subscriptions/model#licensed-and-metered) one is in a [pipeline](https://github.com/thetanz/smp-docs/issues/14). 

> To extend your product pricing options (by currencies and billing intervals), just add a new price with the same name. Please check our [Stripe Schema](StripeSchema.md#product) documentation to get more information about how to set up the Stripe configuration implemented in Subscription Management. 

## 3. Installing dependencies
<img align="right" src="https://www.plantuml.com/plantuml/png/SoWkIImgAStDuOgEp2yjKd2jA4dDAyxCpujLqDMrKuWEBaqgJYxAB2W12lccbyHoEQJcfG2L0m00" />
Subscription Management is a separate extension which you use as a dependency app for each extension you would like to monetize.

1. [Install Subscription Management](https://businesscentral.dynamics.com/?filter=%27ID%27%20IS%20%276717135a-d80c-4a63-8a3a-5ded6717135a%27&page=2503) extension into your cloud development environment.
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
Use [TryAddProduct API](References/SubscriptionMgt.md#tryaddproduct-method) to enable Subscription Management to handle your extension monetization. We recommend executing it during installation and upgrade of your extension to the tenant. Example: 
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

> To block your customers from using your application without an account you can use a combination of [IsActive](References/SubscriptionMgt.md#isactive-method)/[ShowNotification](References/SubscriptionMgt.md#shownotification-method) within your application UX entry points or use them to control extension-specific ApplicaitonArea if such has been defined. 

## See Also
- [SubscriptionMgt_SM_TSL Reference](References/SubscriptionMgt.md)
- [Security & Privacy](Overview/Security&Privacy.md)
- [FAQ](FAQ.md)
