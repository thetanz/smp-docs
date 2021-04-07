# Stripe Lifecycles

## Subscription
| Status | Description | Action Required (as applicable) | Subscription Management Behaviour
| - | - | - |
active | The subscription is in good standing and the most recent payment was successful. It’s safe to provision your product for your customer. |  | |
trialing | The subscription is currently in a trial period and it’s safe to provision your product for your customer. The subscription transitions automatically to active when the first payment is made. |  | |
past_due | Payment on the latest invoice either failed or wasn’t attempted. | Notify the customer, Collect new payment information  and create a new payment method, Attach the payment method to the customer, Update the default payment method, Pay the invoice using the new payment method. | SM will continue to respond as active. Notification will be raised every 7 days to inform the user to update the payment method to complete the payment and make the subscription active.
incomplete | Payment failed when the subscription was created. A successful payment needs to be made within 23 hours to activate the subscription. See the payments section for details on resolving subscriptions with this status | Notify the customer, Collect new payment information  and create a new payment method, Attach the payment method to the customer, Update the default payment method, Pay the invoice using the new payment method. | SM will continue to respond as active. Notification will be raised to inform the user to update the payment method to complete the payment and make the subscription active. The customer cannot change the plan.
incomplete_expired | The initial payment on the subscription failed and no successful payment was made within 23 hours of creating the subscription. These subscriptions do not bill customers. This status exists so you can track customers that failed to activate their subscriptions. | Notify the customer, Collect new payment information  and create a new payment method, Attach the payment method to the customer, Update the default payment method, Pay the invoice using the new payment method. | SM will continue to respond as active. Notification will be raised to inform the user to update the payment method to complete the payment and make the subscription active. The customer cannot change the plan.
cancelled | The subscription has been cancelled. During cancellation  automatic collection for all unpaid invoices is disabled (auto_advance=false). | | | 
unpaid | The latest invoice hasn’t been paid but the subscription remains in place. The latest invoice remains open and invoices continue to be generated but payments aren’t attempted. | | | 

## See Also
- [SubscriptionMgt_SM_TSL Reference](SubscriptionMgt.md)
- [Stripe Schema](StripeSchema.md)

![Analytics](https://ga-beacon.appspot.com/G-P2LEDQJP25/smp/References/StripeLifecycles?pixel)