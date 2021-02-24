# SubscriptionMgt_SM_TSL (Codeunit)
SubscriptionMgt_SM_TSL codeunit contains all the code blocks for the integration aspect of Subscription Management product. It comprises of multiple functions as described below. 
## Common Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | It's your [Stripe Secret Key](https://stripe.com/docs/keys#obtain-api-keys) which allows any API request to your Stripe account without restriction. It **should be kept confidential** preferably in [secure vault](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-app-key-vault-overview). |
| PublishableKey | Text | It's your [Stripe Publishable Key](https://stripe.com/docs/keys#obtain-api-keys) which allows identify your Stripe account when using Stripe.js controls. They aren't secret and can safely published in code. |
| ProductID | Text\[100\] | It's [Stripe product](https://dashboard.stripe.com/products) identifier of the product that assosiated with your extension. |
<!-- theme: info -->
> _SecretKey_, _PublishableKey_ and _ProductID_ parameter values is differ whereware you using Stripe in test or live mode. Use test values during development/testing and make sure you use live one in production ready package. Easiest way to do it is by replacing [keyVaultUrls](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-app-key-vault#specify-the-azure-key-vault-in-extensions) during your continuous integration process.

## Integration API
### TryAddProduct (Method)
Requests SM to start handling your extension. It's recomended to call it with `OnInstallAppPerDatabase` and `OnUpgradePerDatabase` events.
#### TryAddProduct(Text,Text,ModuleInfo,Text[100])
![](https://img.shields.io/badge/version-v1.0.0.0-blue)
```sql
[NonDebuggable]
TryAddProduct(SecretKey:Text;PublishableKey:Text;Info:ModuleInfo;ProductID:Text[100]):Boolean
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | [Stripe Secret Key](#common-parameters) |
| PublishableKey | Text | [Stripe Publishable Key](#common-parameters) |
| Info | ModuleInfo | It's your extension [module info](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/moduleinfo) object instance. It can be retrieved by using `NavApp.GetCurrentModuleInfo(Info)` function. |
| ProductID | Text\[100\] | [Stripe Product ID](#common-parameters) |
##### Returns
| Type | Description |
| - | - |
| Boolean | Indicating whether operation completed with success |
##### Examples
<!--
type: tab
title: InstallExt.Codeunit.al
-->
```sql
codeunit 50000 InstallExt
{
    Subtype = Install;

    [NonDebuggable]
    trigger OnInstallAppPerDatabase()
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        Info: ModuleInfo;
        SecretKey: Text;
        PublishableKey: Text;
        ProductID: Text[100];
    begin
        if NavApp.GetCurrentModuleInfo(Info) then
            if SecretProvider.TryInitializeFromCurrentApp() then
                if SecretProvider.GetSecret('SecretKey', SecretKey) and
                   SecretProvider.GetSecret('PublishableKey', PublishableKey) and
                   SecretProvider.GetSecret('MyAppProductID', ProductID)
                then
                    SubscriptionMgt.TryAddProduct(
                        SecretKey,
                        PublishableKey,
                        Info,
                        ProductID);
    end;
}
```
<!--
type: tab
title: UpgradeExt.Codeunit.al
-->
```sql
codeunit 50001 UpgradeExt
{
    Subtype = Upgrade;

    [NonDebuggable]
    trigger OnUpgradePerDatabase()
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        Info: ModuleInfo;
        SecretKey: Text;
        PublishableKey: Text;
        ProductID: Text[100];
    begin
        if NavApp.GetCurrentModuleInfo(Info) then
            if SecretProvider.TryInitializeFromCurrentApp() then
                if SecretProvider.GetSecret('SecretKey', SecretKey) and
                   SecretProvider.GetSecret('PublishableKey', PublishableKey) and
                   SecretProvider.GetSecret('MyAppProductID', ProductID)
                then
                    SubscriptionMgt.TryAddProduct(
                        SecretKey,
                        PublishableKey,
                        Info,
                        ProductID);
    end;
}
```
<!-- type: tab-end -->
#### TryAddProduct(Text,Text,Guid,Text[100])
![](https://img.shields.io/badge/version-v1.0.0.0-blue)
```sql
[NonDebuggable]
TryAddProduct(SecretKey:Text;PublishableKey:Text;AppID:Guid;ProductID:Text[100]):Boolean
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | [Stripe Secret Key](#common-parameters) |
| PublishableKey | Text | [Stripe Publishable Key](#common-parameters) |
| AppID | Guid | It's [unique ID of your extension](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/devenv-json-files#Appjson). You can retrieve it from [current module info](https://docs.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/moduleinfo/moduleinfo-id-method). |
| ProductID | Text\[100\] | [Stripe Product ID](#common-parameters) |
##### Returns
| Type | Description |
| - | - |
| Boolean | Indicating whether operation completed with success |
##### Examples
<!--
type: tab
title: InstallExt.Codeunit.al
-->
```sql
codeunit 50000 InstallExt
{
    Subtype = Install;

    [NonDebuggable]
    trigger OnInstallAppPerDatabase()
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        Info: ModuleInfo;
        SecretKey: Text;
        PublishableKey: Text;
        ProductID: Text[100];
    begin
        if NavApp.GetCurrentModuleInfo(Info) then
            if SecretProvider.TryInitializeFromCurrentApp() then
                if SecretProvider.GetSecret('SecretKey', SecretKey) and
                   SecretProvider.GetSecret('PublishableKey', PublishableKey) and
                   SecretProvider.GetSecret('MyAppProductID', ProductID)
                then
                    SubscriptionMgt.TryAddProduct(
                        SecretKey,
                        PublishableKey,
                        Info.Id(),
                        ProductID);
    end;
}
```
<!--
type: tab
title: UpgradeExt.Codeunit.al
-->
```sql
codeunit 50001 UpgradeExt
{
    Subtype = Upgrade;

    [NonDebuggable]
    trigger OnUpgradePerDatabase()
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        Info: ModuleInfo;
        SecretKey: Text;
        PublishableKey: Text;
        ProductID: Text[100];
    begin
        if NavApp.GetCurrentModuleInfo(Info) then
            if SecretProvider.TryInitializeFromCurrentApp() then
                if SecretProvider.GetSecret('SecretKey', SecretKey) and
                   SecretProvider.GetSecret('PublishableKey', PublishableKey) and
                   SecretProvider.GetSecret('MyAppProductID', ProductID)
                then
                    SubscriptionMgt.TryAddProduct(
                        SecretKey,
                        PublishableKey,
                        Info.Id(),
                        ProductID);
    end;
}
```
<!-- type: tab-end -->

### IsActive (Method)
Checks whether product subscription is in one of the active states (active or trialing).
#### IsActive(Text,Text[100])
![](https://img.shields.io/badge/version-v1.0.0.0-blue)
```sql
[NonDebuggable]
IsActive(SecretKey:Text;ProductID:Text[100]):Boolean
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | [Stripe Secret Key](#common-parameters) |
| ProductID | Text\[100\] | [Stripe Product ID](#common-parameters) |
##### Returns
| Type | Description |
| - | - |
| Boolean | Indicates whether product subscription is in one of the active states (active or trialing) |
##### Examples
```sql
pageextension 50000 MyExtension extends "Customer Card"
{
    trigger OnOpenPage()
    begin
        CurrPage.Editable := IsActive()
    end;

    [NonDebuggable]
    procedure IsActive(): Boolean
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        SecretKey: Text;
        ProductID: Text[100];
    begin
        if SecretProvider.TryInitializeFromCurrentApp() then
            if SecretProvider.GetSecret('SecretKey', SecretKey) and
               SecretProvider.GetSecret('MyAppProductID', ProductID)
            then
                exit(SubscriptionMgt.IsActive(SecretKey, ProductID));
    end;
}
```
### IsTrialing (Method)
Returns whether a subscription is under a trial period currently.
#### IsTrialing(Text,Text[100])
![](https://img.shields.io/badge/version-v1.0.0.0-blue)
```sql
[NonDebuggable]
IsTrialing(SecretKey:Text;ProductID:Text[100]):Boolean
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | [Stripe Secret Key](#common-parameters) |
| ProductID | Text\[100\] | [Stripe Product ID](#common-parameters) |
##### Returns
| Type | Description |
| - | - |
| Boolean | Indicates whether a subscription is under a trial period currently. |
##### Examples
```sql
TBD
```
### GetPriceName (Method)
Returns name of the user selected plan. Returns `''` if no plan selected.
#### GetPriceName(Text,Text[100])
<a href="../References/Changelog.md#1040-2020-12-13" style="border-bottom-width:0px;background:transparent;padding:0px;">![](https://img.shields.io/badge/version-v1.0.4.0-blue)</a>
```sql
[NonDebuggable]
GetPriceName(SecretKey:Text;ProductID:Text[100]):Text
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | [Stripe Secret Key](#common-parameters) |
| ProductID | Text\[100\] | [Stripe Product ID](#common-parameters) |
##### Returns
| Type | Description |
| - | - |
| Text | TBD |
##### Examples
```sql
TBD
```
### SetQuantity (Method)
Sets the current quantity for the specified product. Returns `true` if the update process is successful, otherwise returns `false`.
#### SetQuantity(Text,Text[100],BigInteger)
![](https://img.shields.io/badge/version-Unreleased-blue)
```sql
[NonDebuggable]
GetQuantity(SecretKey:Text;ProductID:Text[100];Quantity:BigInteger):Boolean
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | [Stripe Secret Key](#common-parameters) |
| ProductID | Text\[100\] | [Stripe Product ID](#common-parameters) |
| Quantity | BigInteger | Quantity of the product |
##### Returns
| Type | Description |
| - | - |
| Boolean | `true` if the update process completed with success, otherwise returns `false` |
##### Examples
```sql
page 50000 "My Product Page"
{

    Caption = 'My Product Page';
    PageType = List;
    SourceTable = "My Account Product";

    layout
    {
        area(content)
        {
            repeater(General)
            {
                field(ProductName; ProductName)
                {
                    Caption = 'Product Name';
                    ApplicationArea = All;
                    Editable = false;
                }
                field(ProductUnit; ProductUnit)
                {
                    Caption = 'Product Unit';
                    ApplicationArea = All;
                    Editable = false;
                }
                field(Quantity; Quantity)
                {
                    Caption = 'Quantity';
                    ApplicationArea = All;

                    trigger OnValidate()
                    begin
                        if SetQuantity(Quantity) then
                            Message(MsgTxt_Lbl);
                    end;
                }
            }
        }
    }

    [NonDebuggable]
    procedure SetQuantity(Qty: BigInteger): Boolean
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        SecretKey: Text;
        ProductID: Text[100];
    begin
        if SecretProvider.TryInitializeFromCurrentApp() then
            if SecretProvider.GetSecret('SecretKey', SecretKey) and
               SecretProvider.GetSecret('MyAppProductID', ProductID)
            then
                exit(SubscriptionMgt.SetQuantity(SecretKey, ProductID, Qty));
    end;

    var
        Quantity: BigInteger;
        MsgTxt_Lbl: Label 'Quantity value is succesfully updated'.
}
```
#### SetQuantity(Text,Text[100],BigInteger,Boolean)
![](https://img.shields.io/badge/version-Unreleased-blue)
```sql
[NonDebuggable]
GetQuantity(SecretKey:Text;ProductID:Text[100];Quantity:BigInteger;ResetBillingCycle:Boolean):Boolean
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | [Stripe Secret Key](#common-parameters) |
| ProductID | Text\[100\] | [Stripe Product ID](#common-parameters) |
| Quantity | BigInteger | Quantity of the product |
| ResetBillingCycle | Boolean | if `true`, it resets the subscription’s billing cycle anchor to the current time. If `false`, the quantity changes will be applied to a next invoice date. |
##### Returns
| Type | Description |
| - | - |
| Boolean | `true` if the update process completed with success, otherwise returns `false` |
##### Examples
```sql
page 50000 "My Product Page"
{

    Caption = 'My Product Page';
    PageType = List;
    SourceTable = "My Account Product";

    layout
    {
        area(content)
        {
            repeater(General)
            {
                field(ProductName; ProductName)
                {
                    Caption = 'Product Name';
                    ApplicationArea = All;
                    Editable = false;
                }
                field(ProductUnit; ProductUnit)
                {
                    Caption = 'Product Unit';
                    ApplicationArea = All;
                    Editable = false;
                }
                field(ResetBillingCycle; ResetBillingCycle)
                {
                    Caption = 'Reset Billing Cycle';
                    ApplicationArea = All;
                }
                field(Quantity; Quantity)
                {
                    Caption = 'Quantity';
                    ApplicationArea = All;

                    trigger OnValidate()
                    begin
                        if SetQuantity(Quantity, ResetBillingCycle) then
                            Message(MsgTxt_Lbl);
                    end;
                }
            }
        }
    }

    [NonDebuggable]
    procedure SetQuantity(Qty: BigInteger; ResetBillingCycle: Boolean): Boolean
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        SecretKey: Text;
        ProductID: Text[100];
    begin
        if SecretProvider.TryInitializeFromCurrentApp() then
            if SecretProvider.GetSecret('SecretKey', SecretKey) and
               SecretProvider.GetSecret('MyAppProductID', ProductID)
            then
                exit(SubscriptionMgt.SetQuantity(SecretKey, ProductID, Qty, ResetBillingCycle));
    end;

    var
        Quantity: BigInteger;
        MsgTxt_Lbl: Label 'Quantity value is succesfully updated.';
}
```
#### SetQuantity(Text,Text[100],BigInteger,Boolean,Boolean)
![](https://img.shields.io/badge/version-Unreleased-blue)
```sql
[NonDebuggable]
GetQuantity(SecretKey:Text;ProductID:Text[100];Quantity:BigInteger;ResetBillingCycle:Boolean;ShowConfirmation:Boolean):Boolean
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | [Stripe Secret Key](#common-parameters) |
| ProductID | Text\[100\] | [Stripe Product ID](#common-parameters) |
| Quantity | BigInteger | Quantity of the product |
| ResetBillingCycle | Boolean | if `true`, it resets the subscription’s billing cycle anchor to the current time. If `false`, the quantity changes will be applied to a next invoice date. |
| ShowConfirmation | Boolean | If `true`, the confirmation dialog pops up with an upcoming invoice information where there will be an information about what next payment will look like and question to proceed. |
##### Returns
| Type | Description |
| - | - |
| Boolean | `true` if the update process completed with success, otherwise returns `false` |
##### Examples
```sql
page 50000 "My Product Page_SM_TSL"
{

    Caption = 'My Product Page';
    PageType = List;
    SourceTable = "My Account Product";

    layout
    {
        area(content)
        {
            repeater(General)
            {
                field(ProductName; ProductName)
                {
                    Caption = 'Product Name';
                    ApplicationArea = All;
                    Editable = false;
                }
                field(ProductUnit; ProductUnit)
                {
                    Caption = 'Product Unit';
                    ApplicationArea = All;
                    Editable = false;
                }
                field(ResetBillingCycle; ResetBillingCycle)
                {
                    Caption = 'Reset Billing Cycle';
                    ApplicationArea = All;
                }
                field(ShowConfirmation; ShowConfirmation)
                {
                    Caption = 'Show Confirmation';
                    ApplicationArea = All;
                }
                field(Quantity; Quantity)
                {
                    Caption = 'Quantity';
                    ApplicationArea = All;

                    trigger OnValidate()
                    begin
                        if SetQuantity(Quantity, ResetBillingCycle, ShowConfirmation) then
                            Message(MsgTxt_Lbl);
                    end;
                }
            }
        }
    }

    [NonDebuggable]
    procedure SetQuantity(Qty: BigInteger; ResetBillingCycle: Boolean; ShowConfirmation: Boolean): Boolean
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        SecretKey: Text;
        ProductID: Text[100];
    begin
        if SecretProvider.TryInitializeFromCurrentApp() then
            if SecretProvider.GetSecret('SecretKey', SecretKey) and
               SecretProvider.GetSecret('MyAppProductID', ProductID)
            then
                exit(SubscriptionMgt.SetQuantity(SecretKey, ProductID, Qty, ResetBillingCycle, ShowConfirmation));
    end;

    var
        Quantity: BigInteger;
        MsgTxt_Lbl: Label 'Quantity value is succesfully updated.';
}
```
### ShowNotification (Method)
Force SM to show a notification to user to act on subscription. It will return false if there are nothing to show.
#### ShowNotification(Text,Text[100])
<a href="../References/Changelog.md#1040-2020-12-13" style="border-bottom-width:0px;background:transparent;padding:0px;">![](https://img.shields.io/badge/version-v1.0.4.0-blue)</a>
```sql
[NonDebuggable]
ShowNotification(SecretKey:Text;ProductID:Text[100]):Boolean
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| SecretKey | Text | [Stripe Secret Key](#common-parameters) |
| ProductID | Text\[100\] | [Stripe Product ID](#common-parameters) |
##### Returns
| Type | Description |
| - | - |
| Boolean | Indicates if any notification shows |
##### Examples
```sql
pageextension 50000 MyExtension extends "Customer Card"
{
    trigger OnOpenPage()
    begin
        CurrPage.Editable := IsActive()
    end;

    [NonDebuggable]
    procedure IsActive(): Boolean
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        SecretKey: Text;
        ProductID: Text[100];
    begin
        if SecretProvider.TryInitializeFromCurrentApp() then
            if SecretProvider.GetSecret('SecretKey', SecretKey) and
               SecretProvider.GetSecret('MyAppProductID', ProductID)
            then
                if SubscriptionMgt.IsActive(SecretKey, ProductID) then
                  exit(true)
                else
                  SubscriptionMgt.ShowNotification(SecretKey, ProductID);
    end;
}
```
## Mocking API
### RequestMocking (Method)
Request service mocking by key provided.
#### RequestMocking(Text)
<a href="../References/Changelog.md#1040-2020-12-13" style="border-bottom-width:0px;background:transparent;padding:0px;">![](https://img.shields.io/badge/version-v1.0.4.0-blue)</a>
```sql
[NonDebuggable]
RequestMocking(PrivateKey:Text)
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| PrivateKey | Text | Private key used to authorize mocking |
##### Examples
```sql
codeunit 50002 "MyExtensionTest"
{
    Subtype = Test;

    [Test]
    procedure TestMyExtension();
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        MockAuthKey: Text;
    begin
        // [Scenario] Check if customer card is editbale when subscription is active
        // [Given] my extension is installed and subscription is active
        SecretProvider.TryInitializeFromCurrentApp();
        SecretProvider.GetSecret('MockAuthKey', MockAuthKey);
        SubscriptionMgt.RequestMocking(MockAuthKey);
        SubscriptionMgt.SetMock(false, true, 'Business');
        // [When] user opens a customer card 
        ...
        // [Then] castomer card page is editable
        ...
    end;
}
```
### AuthorizeMocking (Method)
Allows further calls to the service to be mocked using provided private key.
#### AuthorizeMocking(Text)
<a href="../References/Changelog.md#1040-2020-12-13" style="border-bottom-width:0px;background:transparent;padding:0px;">![](https://img.shields.io/badge/version-v1.0.4.0-blue)</a>
```sql
[NonDebuggable]
AuthorizeMocking(PrivateKey:Text)
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| PrivateKey | Text | Private key used to authorize mocking |
##### Examples
```sql
pageextension 50000 MyExtension extends "Customer Card"
{
    trigger OnOpenPage()
    begin
        CurrPage.Editable := IsActive()
    end;

    [NonDebuggable]
    procedure IsActive(): Boolean
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        SecretKey: Text;
        ProductID: Text[100];
        MockAuthKey: Text;
    begin
        if SecretProvider.TryInitializeFromCurrentApp() then
            if SecretProvider.GetSecret('SecretKey', SecretKey) and
               SecretProvider.GetSecret('MyAppProductID', ProductID) and
               SecretProvider.GetSecret('MockAuthKey', MockAuthKey)
            then begin
                SubscriptionMgt.AuthorizeMocking(MockAuthKey);
                exit(SubscriptionMgt.IsActive(SecretKey, ProductID));
            end
    end;
}
```
### SetMock (Method)
Sets response which `SubscriptionMgt_SM_TSL` will reply during test execution.
#### SetMock(Boolean,Boolean,Text)
![](https://img.shields.io/badge/version-v1.0.0.0-blue)
```sql
[NonDebuggable]
SetMock(IsTrialing:Boolean;IsActive:Boolean;PriceName:Text)
```
##### Parameters
| Name | Type | Description |
| - | - | - |
| IsTrialing | Boolean | Defines response for `IsTrialing` method |
| IsActive | Boolean | Defines response for `IsActive` method |
| PriceName | Text | Defines response for `GetPriceName` method |
##### Examples
```sql
codeunit 50002 "MyExtensionTest"
{
    Subtype = Test;

    [Test]
    procedure TestMyExtension();
    var
        SecretProvider: Codeunit "App Key Vault Secret Provider";
        SubscriptionMgt: Codeunit SubscriptionMgt_SM_TSL;
        MockAuthKey: Text;
    begin
        // [Scenario] Check if customer card is editbale when subscription is active
        // [Given] my extension is installed and subscription is active
        SecretProvider.TryInitializeFromCurrentApp();
        SecretProvider.GetSecret('MockAuthKey', MockAuthKey);
        SubscriptionMgt.RequestMocking(MockAuthKey);
        SubscriptionMgt.SetMock(false, true, 'Business');
        // [When] user opens a customer card 
        ...
        // [Then] castomer card page is editable
        ...
    end;
}
```
