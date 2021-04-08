# Getting Started
This is a simple guide to get started with Subscription Management. Follow all the steps or jump to where you are in the process.
## 1. Connect your Stripe Account
<img align="right" src="https://www.belcar.fi/wp-content/uploads/2020/10/Stripe-wordmark-slate_sm-2.png" />

Subscription Management uses your Stripe account as a backend for all data. All your products as well as future customers and subscriptions will be stored and handled within Stripe.

<!-- theme: warning -->
> Subscription Management will have full access to your Stripe account. Due to this, we recommended a separate account is provisioned solely for this purpose.

<a href="https://dashboard.stripe.com/oauth/authorize?response_type=code&client_id=ca_IP9AidZcFWmxKgnfQwKQri4paRKxNATO&scope=read_write" style="border-bottom-style:none;padding:10px 90px;background-image:url('https://dabuttonfactory.com/button.png?t=Connect+with+Stripe&f=Open+Sans-Bold&ts=14&tc=fff&hp=23&vp=14&w=180&h=38&c=4&bgt=unicolored&bgc=635bff')"></a>
## 2. Setup Stripe Product & Price
> This process still to be documented. Please contact [Product Team](mailto:volodymyr.leonov@theta.co.nz?subject=%5BSM%5D) for assistance.
## 3. Installing dependencies
<img align="right" src="https://www.plantuml.com/plantuml/png/SoWkIImgAStDuOgEp2yjKd2jA4dDAyxCpujLqDMrKuWEBaqgJYxAB2W12lccbyHoEQJcfG2L0m00" />
Subscription Management is a separate extension which you use as a dependency for each extension you would like to monetize.

1. [Install Subscription Management](https://share.hsforms.com/1jnXDTuDCR7CCWyzDoGl9jw5n4ae) extension into your development environment.
2. Add a dependency to your extension's `app.json`.
```json
"dependencies": [
   ...
   {
      "id": "6717135a-d80c-4a63-8a3a-5ded6717135a",
      "publisher": "Theta Systems Limited",
      "name": "SubscriptionMgt",
      "version": "1.0.0.0"
    }
]
```
## 4. Basic Integration
> This process still to be documented. Please contact [Product Team](mailto:volodymyr.leonov@theta.co.nz?subject=%5BSM%5D) for assistance.

## See Also
- [SubscriptionMgt_SM_TSL Reference](References/SubscriptionMgt.md)
- [Security & Privacy](Overview/Security&Privacy.md)
- [FAQ](FAQ.md)