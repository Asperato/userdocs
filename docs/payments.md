---
id: payments
title: Payments
sidebar_label: Payments
---

## Collecting one-off payments
For simple one-off payments without an authorisation (that require payment details to be entered), simply create a payment record with the required amount, and select the payment route options you wish to allow on the payment page.
 
You can then access the payment page via one of two ways:
 
 - If the customer is providing you with payment details as you are in the org (such as over the phone), then hit the “Process payment” button on the top-right of the screen, then enter the required details into the form.
 - If you wish to provide the customer with a link to the payment page that they can complete at their own convenience, copy the “Ecommerce URL” field and supply this to the customer (this might be via email, IM, or any other means.)
 
## Manually collecting ad-hoc payments against an existing authorisation
 
Ad hoc payments can easily be taken where a related authorisation record is already set up.

1. Navigate to the authorisation record for which you wish to set up a payment. Under the payment related list for the authorisation, select `New`:
 
![New payment from auth](/userdocs/img/payments/payment_related_auth.png)
 
Note that the authorisation field will be pre-populated with the required authorisation record.

2. Enter the required amount, and then hit the "Process Payment" button. 
     1. This will create the payment record with the authorisation attached.
     2. The payment would be immediately processed.    
 
## Automatically collecting payments against an existing authorisation
 
Payments can be automatically collected against an existing authorisation by creating a payment record where the following conditions are true:
 - The payment record is set to “Awaiting submission”
 - The payment record is attached to an authorisation
 - The attached authorisation's status is either “In force” or “Pending”
 - The payment record has a "Due date" either today, or in the past
 - The field value for "Payment route selected" has a matching value on both records - the payment and attached authorisation (v2.14+).
 
An overnight batch job will run and attempt to collect any payments that fulfil these above criteria.
 
This payment record can be created manually as above. However, more commonly in practice, it can also be created automatically as part of a Lightning flow, Process, Apex trigger or any other method Salesforce provides for automation.

## Collecting a payment and an authorisation simultaneously

Many business cases require collecting an initial payment from a customer, and simultaneously collecting an authoristaion so future payments can be collected seamlessly.

To do this:

 - Create a new payment record with the amount of the initial payment
 - Create a new authorisation record
 - Set the "Authorisation" field on the payment record to the authorisation created in the previous step
 - Hit the "Process payment" button to process the payment and authorisation from within Salesforce, or distribute the link contained in the "Ecommerce URL" to the customer for processing.
 
When the payment page has been filled in and processed, both the payment and authorisation record will be populated with the result of the transaction. The authorisation record can then be used to process any future payments as and when required.

## Expiring a payment link

You may wish to expire the payment link so it can no longer be used to collect funds. To do this, simply set the "Payment stage" field to "Expired":

![Expired status](/userdocs/img/payments/expired.png)
 
## Required data
 
The required fields for a payment are: 

 - Available payment routes
 - Amount 
 - Currency (only if multi-currency payments are enabled for the Salesforce org.)
 
When creating a payment from an authorisation, the authorisation field will automatically be populated with the correct record ID.
 
## Statuses
Payment statuses are provided as follows:
 
<table>
<tr>
<th>Awaiting submission</th>
<td>The payment has not yet been processed or submitted to your payment service provider.</td>
</tr><tr>
<th>Submitted for collection</th>
<td>The payment has been submitted to your payment service provider, but the outcome of this transaction is not yet known. This is used for direct debit payments which will take a few days to clear.</td>
</tr><tr>
<th>Collected from Customer</th>
<td>The payment has been collected from the customer and has been confirmed.</td>
</tr><tr>
</tr><tr>
<th>Retry in progress</th>
<td>Status value introduced in package version 2.16. The payment collection attempt has failed and will be retried in a few days. Note that this status only applies to integrations with GoCardless Success+.</td>
</tr><tr>
<th>Failed</th>
<td>The payment failed to collect. There are a variety of reasons why this could happen, in this case there should be a reason documented in the “Status description” field. Note that if a payment fails, and that payment is attached to an authorisation, the authorisation status will be unaffected. The failure of a payment does not necessarily imply a failure of the underlying authorisation (for example, it could simply be that there are insufficient funds in the account at this time.)</td>
</tr>
</table>
 
## Cancellations / Refunds in Salesforce
If you wish to refund a payment, navigate to the payment record and press the “Refund” button. This will show as a standard button in classic, and a quick action in lightning:
 
![Refund button](/userdocs/img/payments/refund_button.png)
 
You’ll then see the refund dialog, where you can either choose to refund a specified amount (up to the original amount of the payment).
 
![Refund dialog](/userdocs/img/payments/refund_dialog.png)
 
Note that some payment service providers place restrictions on refunds. If this is the case, you will need to contact your payment service provider and ask them to enable refunds on your account.

## Payment outcomes
Not all payments will succeed - they may fail for a variety of reasons, such as insufficient funds, a billing address that doesn't match, the card has been blocked, etc. Asperato will sanitise all error responses across payment service providers to one of a set of values. This enables you to easily automate different flows off the back of specific failure reasons, rather than failures in general.

The sanitised responses we currently support are listed here:

<table class="sanitisedResponses">
<tr>
<th>NOT_COMPLETED</th>
<td>The payment gateway authorisation screen was not completed correctly.</td>
</tr>
<tr>
<th>DECLINED</th>
<td>Transaction declined, a reason was not given. Please try again. If no luck, try a different payment method.</td>
</tr>
<tr>
<th>DECLINED_AUTH_NOT_FOUND</th>
<td>A repeat payment was attempted using an authorisation, but the gateway did not have a record of this authorisation.</td>
</tr>
<tr>
<th>DECLINED_INVALID_NAME</th>
<td>Transaction declined, a valid name was not provided.</td>
</tr>
<tr>
<th>DECLINED_FRAUD</th>
<td>Transaction declined due to an unspecified issue. Please contact your bank for more details</td>
</tr>
<tr>
<th>DECLINED_AVS</th>
<td>Declined, billing address does not match the address held by the bank. Please check the address entered.</td>
</tr>
<tr>
<th>DECLINED_AVS_MISSING_INFO</th>
<td>Declined, required billing information not specified. Please check you have completed all required fields.</td>
</tr>
<tr>
<th>DECLINED_ABA</th>
<td>Declined, routing number was incorrect</td>
</tr>
<tr>
<th>DECLINED_CV2</th>
<td>Declined, card security code was incorrect. Please check the digits given on the reverse of card (or the front of the card for American Express) and try again.</td>
</tr>
<tr>
<th>DECLINED_CARD_DETAILS</th>
<td>Declined, card details were incorrect. Please check the card details entered. If the problem persists please contact your card issuer or try a different payment method.</td>
</tr>
<tr>
<th>DECLINED_WRONG_CARD_TYPE</th>
<td>Declined, the card type you specified does not match the card number. Please check the card details entered.</td>
</tr>
<tr>
<th>DECLINED_UNSUPPORTED_CARD_TYPE</th>
<td>Declined, the card you used isn't supported. Please try with a different card or contact the company you are trying to make payment to.</td>
</tr>
<tr>
<th>DECLINED_DUPLICATE</th>
<td>Declined, duplicate transaction. Please do not try again as payment has most likely already been collected. Please contact the company you are trying to make payment to.</td>
</tr>
<tr>
<th>DECLINED_ISSUE</th>
<td>Invalid issue number. Please check and try again. If the problem persists please contact your card issuer.</td>
</tr>
<tr>
<th>DECLINED_START_DATE</th>
<td>Declined, start date is in the future. Please enter a start date that is in the past.</td>
</tr>
<tr>
<th>DECLINED_EXPIRY_DATE</th>
<td>Declined, card expired. Please use a different card or contact your bank.</td>
</tr>
<tr>
<th>DECLINED_INVALID_EMAIL</th>
<td>Declined, the email address is mandatory and a valid one was not provided. Please try again and enter your email address.</td>
</tr>
<tr>
<th>DECLINED_UNSUPPORTED_CURRENCY_TYPE</th>
<td>Declined, the currency you used isn't supported.</td>
</tr>
<tr>
<th>DECLINED_UNSUPPORTED_CURRENCY_TYPE_ASP</th>
<td>Declined, no payment service provider has been set up for this currency.</td>
</tr>
<tr>
<th>DECLINED_INVALID_AMOUNT</th>
<td>Declined, invalid amount. Please check the amount and try again. If the problem persists, please contact the company you are trying to make payment to.</td>
</tr>
<tr>
<th>DECLINED_AMOUNT_TOO_LARGE</th>
<td>Declined, the amount is too large.</td>
</tr>
<tr>
<th>DECLINED_INSUFFICIENT_FUNDS</th>
<td>Declined, there are insufficient funds in this account.</td>
</tr>
<tr>
<th>DECLINED_PAYER_DECEASED</th>
<td>Declined, this account belongs to someone who is deceased.</td>
</tr>
<tr>
<th>DECLINED_AMOUNT_MISMATCH</th>
<td>Declined, the amount does not match the amount of the previous transaction
</td>
</tr>
<tr>
<th>DECLINED_ALREADY_SETTLED</th>
<td>Declined, this transaction has already been settled</td>
</tr>
<tr>
<th>DECLINED_REFERRED</th>
<td>Declined. Your bank has not authorised the transaction, Please contact your card issuing bank for more details and then try to process the transaction again</td>
</tr>
<tr>
<th>DECLINED_CREDIT_LIMIT_EXCEEDED</th>
<td>Declined, there are insufficient funds in the account. Please try with other card or payment method.</td>
</tr>
<tr>
<th>DECLINED_CARD_TYPE_NOT_PERMITTED</th>
<td>Declined, the card type presented is not accepted by the merchant. Please use a different card</td>
</tr>
<tr>
<th>DECLINED_ALREADY_REVERSED</th>
<td>Declined, this authorisation has already been reversed
</td>
</tr>
<tr>
<th>DECLINED_USAGE_LIMIT_EXCEEDED</th>
<td>Declined, the card has exceeded its usage limit - either the number of times used or the cumulative amount processed. Please use a different payment method</td>
</tr>
<tr>
<th>DECLINED_TRANSACTION_COMPLETED</th>
<td>Declined, the transaction being referenced has already been completed so this operation cannot be performed. Please try again and if this error persists, please contact the merchant</td>
</tr>
<tr>
<th>DECLINED_MISSING_FIELDS</th>
<td>Declined, some of the fields are missinging in the request. Please try again. If the problem persists contact your merchant.</td>
</tr>
<tr>
<th>DECLINED_INVALID_DATA</th>
<td>Declined, some of the fields contain invalid data in the request. Please try again. If the problem persists contact your merchant.</td>
</tr>
<tr>
<th>DECLINED_CARD_NOT_AUTHORISED_OR_INACTIVE</th>
<td>Declined, this card is not authorised for this transaction or has marked as inactive. Please contact your bank.</td>
</tr>
<tr>
<th>DECLINED_INVALID_CARD</th>
<td>The Card was declined by the issuer.</td>
</tr>
<tr>
<th>PAYMENT_RETRY_FAILED</th>
<td>Payment retry failed at Payment Gateway. Please contact Payment Gateway for more information.</td>
</tr>
<tr>
<th>DECLINED_GATEWAY_ERROR</th>
<td>Declined, the gateway encountered an error. Please try again in a few minutes. If the problem persists, please contact the company you are trying to make payment to.</td>
</tr>
<tr>
<th>DECLINED _WRONG AUTHENTICATION</th>
<td>Declined, the authentication entered is incorrect</td>
</tr>
<tr>
<th>DECLINED_SESSION EXPIRED</th>
<td>Declined, the 3D authentication was not entered and session expired.</td>
</tr>
<tr>
<th>AUTHENTICATION_REQUIRED</th>
<td>The Payment using this card requires authentication. Please authenticate the cardholder to continue with the transaction.</td>
</tr>
<tr>
<th>TRANSACTION_DECLINED_BY_ISSUER</th>
<td>Transaction was declined for this card/account. Please contact your bank.</td>
</tr>
<tr>
<th>DECLINED_INVALID_API_KEYS</th>
<td>The api keys used for connection are not valid. Please get the updated keys from gateway and correct the connection details in Asperato.</td>
</tr>
<tr>
<th>REFUND_DECLINED_BY_GATEWAY</th>
<td>Refund could not be processed by gateway. Either the Payment is not paid out or the number of refunds that can be collected against payment have exceeded.</td>
</tr>
<tr>
<th>DECLINED_PAYMENT_REFUNDED</th>
<td>A refund against the payment has already been issue.</td>
</tr>
<tr>
<th>DECLINED_MANDATE_ERROR</th>
<td>Mandate is either not setup, Inactive, failed, cancelled or expired</td>
</tr>
<tr>
<th>MANDATE_CANCELLATION_FAILED</th>
<td>Authorisation can not be cancelled as the related mandate could not be cancelled by PSP. Please try after sometime or check status in the PSP dashboard.</td>
</tr>
<tr>
<th>BANK_ACCOUNT_DISABLED</th>
<td>Process could not be established. Customer bank account is disabled or does not exist.</td>
</tr>
<tr>
<th>AUTHORISATION_ERROR</th>
<td>The Card/Bank details could not be authorised for some reason. Please try again with other account.</td>
</tr>
<tr>
<th>INVALID_BANK_ACCOUNT</th>
<td>The bank account details entered are invalid.</td>
</tr>
<tr>
<th>DECLINED_NOT_SUPPORTED</th>
<td>Declined, the requested operation is not supported by the merchant's payment facility. Please contact the merchant or try a different payment method</td>
</tr>
<tr>
<th>DECLINED_NO_USABLE_AUTH_FOUND</th>
<td>Declined, this authorisation being referenced has either already been captured or was previously declined. Please try a different payment method and if this error persists, please contact the merchant</td>
</tr>
<tr>
<th>AUTHORISATION_DISPUTED_CHARGEBACK_ISSUED</th>
<td>A chageback back was issued by customer's bank because either the mandate or the payment was not approved by the customer </td>
</tr>
<tr>
<th>MANDATE_CANCELLED_CHARGEBACK_ISSUED</th>
<td>This payment was charged back because the mandate was withdrawn by customer at their bank</td>
</tr>
<tr>
<th>CHARGEBACK_ISSUED</th>
<td>The payment was charged back.</td>
</tr>
<tr>
<th>AMOUNT_DISPUTED_CHARGEBACK_ISSUED</th>
<td>The customer has disputed that the amount taken differs from the amount they were notified of.</td>
</tr>
<tr>
<th>FRAUD_REPORTED_CHARGEBACK_ISSUED</th>
<td>The customer has disputed having been notified of this Direct Debit.</td>
</tr>
<tr>
<th>REFUND_REQUESTED_CHARGEBACK_ISSUED</th>
<td>A chargeback was issued against this payment, by the customer’s bank at the customer’s request within the 8 week cool-off period.</td>
</tr>
<tr>
<th>CHARGEBACK_ERROR</th>
<td>The chargeback for this transaction can not be issued. Please contact your Issuer/ bank.</td>
</tr>
<tr>
<th>BANK_SERVER_ERROR</th>
<td>Could not connect to bank because the bank server is either down or not responding</td>
</tr>
<tr>
<th>PSP_SERVER_ISSUE</th>
<td>Payment could not be processed by the Payment server or Payment Server is not running.</td>
</tr>
<tr>
<th>FEATURE_DISABLED_AT_GATEWAY</th>
<td>Transaction declined. Please contact the merchant or try a different payment method</td>
</tr>
</table>

## GoCardless Payments Reconcilliation (2.16+)
Whenever GoCardless will make a payout against the payments which were collected from customers, the value of "Payout Reference" field will be updated with the GoCardless "Payout Number". You can use this field to create reports for Payouts grouped by Payments for reconcilliation.

## Custom references (2.13+)

Some PSPs allow you to specify a custom reference attached to an payment. You can specify this by using the "Custom reference" field available on the payment object. 

However, note that not all PSPs or PSP account types support custom references, and some often have restrictions on the maximum length of a reference. You should check your PSPs documentation for any rules around specifying custom references. Note that setting a custom reference where they are not supported, or setting an invalid custom reference may cause a transaction to fail.

## Post transaction endpoints
After a user has loaded the paypage, they may exit the payment page in three different scenarios - having successfully completed the transaction, having unsuccessfully completed the transaction, and having cancelled (not attempted) the transaction. Asperato can send the user to different URLs for each of these three separate scenarios.

These URLs can be set by changing the value of fields on the payment/authorisation record - these fields are are `Success_Endpoint`, `Fail_endpoint`, and `Cancel_endpoint`, and control the URL where a user will be sent in these three scenarios. Note that the "cancel" link will only appear on the payment page if the `Cancel_endpoint` is set.

### Endpoint Considerations:
- Endpoints need to be set on individual payment/authorisation records. This can be done manually, or more likely, in practice, via a Salesforce Process Builder/Workflow. 
- Redirection to endpoints will apply when payment/authorisations are processed via the Ecommerce URL only, they do not apply when payments/authorisations are processed from within the Asperato application.
- It is possible to automatically advance straight to the endpoints without displaying the standard Asperato screens. Please contact the Asperato team to request this.
- Redirection to endpoints will not take effect when the Asperato paypage is iframed. Postmessages should be used with iframes.

## Notes for existing users upgrading to 2.16 package

If you upgrading to package 2.16 and are a GoCardless user then ask your salesforce admin to update the payment <a href="https://help.salesforce.com/articleView?id=sf.customize_layout.htm&type=5"> _page layout_</a> to include
+ Payment status "Retry in progress"
+ Field "payout reference"
+ Checkbox "suppress notification by psp"
