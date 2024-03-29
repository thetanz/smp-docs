---
sidebar_position: 1
title: Product & Prices
hide_title: true
---
# Product & Prices
## Licensed and Metered Usage
The available subscription options are built on [**Usage
Types**](https://stripe.com/docs/billing/subscriptions/model#licensed-and-metered).
These usage types are **licensed** usage and **metered** usage, and they
determine how much a customer is charged for the recurring purchase of your
products.

If you choose the **licensed** usage option, you are requiring that the quantity
of a product is set when the subscription is created or updated. This means that
for every billing period, the subscription charges the quantity x price for the
product. For example, a customer with three users who subscribes to a 10 USD
per-user monthly service is charged 30 USD every month.

With the **metered** usage option your customer is charged for the amount of
your product they have consumed. At the end of the billing period, the total
usage x price is used to calculate how much the customer owes. For example, if a
broadband provider charges 0.50 USD per gigabyte (GB) used, and a customer uses
100 GBs, the customer is charged 50 USD.

When you create a new product, licensed usage is applied by default unless you
select the “**Usage is metered**” checkbox control.

![](./../images/9871628bd51fc5dce267c2f08e33079c.png)

Making this selection then opens a “**Charge for metered usage by**” dropdown
control, where you can select the option that best suits your billing strategy.

![](./../images/086f6b3e60b869e1b8e771bb6b1849a0.png)
:::caution
Important. A product has usage categorized as Licensed by default until the
“**Usage is metered**” checkbox control is selected, then the usage changes to
Metered.
:::
## Pricing Models
When you are planning how to configure the product subscription and depending on
how you want to price each product unit, you can choose between several pricing
models. The pricing models available are **Standard**, **Volume**, **Package**,
and **Graduated**.
Here is a comparison of each pricing model:

| Standard | Volume | Package | Graduated |
|----------|--------|---------|-----------|
| Select **standard** pricing if you charge the same price for each unit. | Select **volume** pricing if you charge the same for each unit based on the total number of units sold. For example, you might charge 10.00 USD per unit for 50 units, and 7.00 USD per unit when the 50+ units total is reached. | Select **package** pricing if you charge by a group of units or a package.  For example, if you charge 50.00 USD for every 5 units. Purchases are rounded up by default, so a customer buying 8 units would pay 100.00 USD. | Select **graduated** pricing if you use pricing tiers that may result in a different price for some units in an order. For example, you might charge 10.00 USD per unit for the first 100 units and then 5.00 USD per unit for the next 50.  |
## How the Usage Types correlate to the Pricing Models
Usage records provide **quantity** information that is used to track how many of
your products a customer is consuming.
With quantity information and the **pricing model** set up by the metered
billing plan, the invoices you send to your customers are accurate i.e. quantity
x price = invoiced amount.
## Configuring the Pricing for your Product
The product setup user interface is contextually driven and the options you are
presented with directly relate to your previous selections. Here is more
information on configuring each of the pricing options available.
### Standard Pricing 
There are two methods of configuring the standard pricing model. Option 1 is for
a one time purchase of your
product.

![](./../images/2502b6d534c72dbb602629d334d98de0.png)

Option 2 is for recurring purchases of your product

![](./../images/5e059e10b895169df50f1ca5e79899e1.png)

You can select the billing period you want, and choose to meter the
usage.

![](./../images/907a2104ba010837b0c513fda5d07192.png)
:::caution
Remember: metered billing lets you charge customers based on reported usage at
the end of each billing period.
:::
### Volume Pricing
The first unit and last unit columns are used to set prices based on the total
number of units sold. In the example below, the first 150 units are charged at
10.00 USD each, and when the 151 total is achieved, all units are charged at
7.00 USD each.

Additional tiers can be added by using the **Add another tier** control.
Hovering over the **Preview** control shows how your selections will impact the
pricing at the final price breakpoint.

![](./../images/4fe2422521ed4f389ed1b278885d2128.png)

As per Standard pricing, the billing period can be selected, and product usage metered.
### Package Pricing
There are two methods of configuring the package pricing model. Option 1 is for
a one time purchase of your product.      

![](./../images/80d036e1088147beba80fe9f5b5d4ca0.png)

Option 2 is for recurring purchases of your product

![](./../images/6527eb113932e234da6742fdf38cb686.png)

As per Standard pricing, the billing period can be selected, and product usage metered.
### Graduated Pricing
The first unit and last unit columns are used to set a different price for some
units in the order. In the example below, the first 100 units are charged at
10.00 USD each, the next 50 units are charged at 8.00 USD each, and units over
151 are charged at 6.00 USD each.
Additional tiers can be added by using the **Add another tier** control.
Hovering over the **Preview** control shows how your selections will impact the
pricing at the final price breakpoint.

![](./../images/3bb32b067ad376c4187d1419f04696de.png)
## One Product - Multiple Pricing Models, Billing Periods, & Currencies
As you create your products you can add multiple pricing models, billing periods,
and currencies to one product by selecting the **Add another price** button.
In this example, there is:
1.  a price per unit per month in USD
2.  a volume-based discount for 3 monthly purchases in USD, and
3.  a price per unit per week in EUR

![](./../images/1249ea853ffcf2193de4a4d3c7bf6e0a.png)
There is no limit to the multiples that can be added to one product, and you can
also add or edit the multiples later by accessing the product record and
selecting the controls:
1.  **Add another price**, or
2.  **…** (ellipses to open a sub-menu)

![](./../images/f62a01ef0bae9aa5e7b44d35f1b03d03.png)