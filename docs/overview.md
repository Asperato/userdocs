---
id: overview
title: Overview
sidebar_label: Overview
---

## Introduction

Asperato ONE allows Salesforce to control the collection of payments. It enables you to collect payments from many different providers such as Worldpay, GoCardless, Braintree, Stripe, Authorize.NET and more. It allows you to fully automate all your payment collection activities from the single control and view of Salesforce.

You can also securely save payment methods from your customers. We call them Authorisations. Authorisations can take the form of a tokenised credit/debit card, a direct debit mandate, or an eCheck authorisation. These Authorisations can be used to collect future one-off and repeat payments as required.

The solution is used by a variety of business models including: franchises (multi deposit accounts connected to a Single Salesforce Org), real estate (rental and deposit collection into escrow bank accounts), insurance (premium collections), non-profits (donations), membership organisations (membership dues), services and manufacturing (invoice dues), council and local government (service leveys and online payments) and many more.

## Installing & setting up Asperato

1. <a target="_blank" style="text-decoration: underline; font-weight: bold;" href="https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000EcrOnUAJ">Install the package from the AppExchange here.</a>
2. Ensure you're in <a target="_blank" href="https://help.salesforce.com/articleView?id=lex_enable_turn_on.htm&type=5">lightning experience</a> and you have <a href="https://help.salesforce.com/articleView?id=domain_name_overview.htm&type=5" target="_blank">My Domain setup and deployed.</a> (Asperato ONE can be used in classic, but has to be setup in lightning experience.)
3. Navigate to the "Asperato Setup" page on the Asperato ONE app.
4. Click the "Setup Configuration" button.

You should now be connected to an Asperato test account, setup with a number of test payment service provider connections so you can start taking test payments right away!

*For a more detailed explanation of setup, see [here](setup).*

## Paypages
With Asperato ONE you do not need to build your own checkout pages. Asperato ONE comes with Paypages pre-built and ready for Salesforce. They allow you to securely capture all the sensitive data (card numbers, bank account details etc) required to collect money from your customers. 

Asperato ONE paypages are dynamic, meaning they respond to the data you populate in Salesforce. For example, if you want give someone the option to pay you by card or Paypal, just tell Salesforce and the paypages will adjust in realtime.

Asperato ONE paypages are extremely functional and offer the following: bank account Validation (sort code, account number and IBAN), address validation, bank identification number (BIN) checking for cards, expiry date validation, card identification, Direct Debit scheme rule compliance and more. We run our pages through a vast array of browsers to ensure successful rendering and transactions time after time. Your customer will never know we built them and your branded journey remains fully intact.

Paypages handle multi-currency and multi language. They can be pre-populated and offer full control of success and fail pages, meaning your customer has an excellent tailored experience every single time they transact.

*For a more detailed explanation of the payment page, see [here](paypage).*

## Objects
Asperato ONE provides all its functionality using just four objects.

### Authorisation
Authorisation records are used when you want to collect and save a payment method from one of your customers. An authorisation can consist of saved card details, a Direct Debit mandate or ACH authoristaion.

Saved payment method details such as card or account number are always tokenised to protect you and your customer from fraud. Your customer can register multiple authorisations with you, so a single customer could have both a card payment method on record as well as a Direct Debit mandate in place.

Asperato ONE will always maintain these records, feeding into Salesforce any state changes that you need to be aware of. For example, if your customer cancels a direct debit, Asperato will update the appropriate authorisation to a cancelled state within Salesforce. Acting on these state changes is something you can do via Salesforce automation.

Key fields include:

<table>
<tr>
<th>Authorisation URL</th>
<td>This is the link you provide to your customer to enable them to provide authority to save a payment method.</td>
</tr>
<tr>
<th>Status</th>
<td>Tells you if the Authorisation is ready to use or not. Autorisations have to be ‘In Force’ before they can be used to collect payments.</td>
</tr>
<tr>
<th>Status description</th>
<td>A descriptive text showing the reason related to the current status. Might contain the reason for cancellation or failure for example.</td>
</tr>
<tr>
<th>Payment Route Options</th>
<td>Allows you to choose which Authorisation routes are available to your customer to use. E.g. Card, Direct Debit or ACH</td>
</tr>
</table>

### Payment
The payment object is the means by which you request and record the outcome of a payment. **Every time you need to collect a payment, you must create a payment record first. This is the only way you can capture and record a payment.**

Payments are created in Salesforce either manually by a user, or by an automated process. Ultimately they can be collected by one of three methods:

1. By the customer via a secure URL;
2. By a Salesforce user by taking details over the phone;
3. Automatically if you already have a saved payment method (an "In Force" authorisation).

Payment records are exactly that, a request for a payments. They can be a card payment, direct debit payment, ACH/eCheck payment or a Paypal payment - we treat them all the same.

Payment records contain all of the information needed to control the payor's experience via the paypage; this includes currencies, payment routes available, amounts, languages and more, as well as directing the user to different pages depending on if the payment was successful or failed.

Payment records can be pre-populated with as much or as little information as you choose. 

Once a Payment record has been processed, all the relevant information from the PSP is populated on to this record alongside a status update. Details such as the payor's name, time and date of payments, any error codes, transaction references etc. are all visible on the payment record.

Key fields include:

<table>
<tr>
<th>Payment Route Options</th>
<td>Allows you to choose which payment routes are available to your customer to use. E.g. Card, Direct Debit or ACH</td>
</tr>
<tr>
<th>ECOM URL</th>
<td>This is the link you provide to your customer to enable them to process the payment.</td>
</tr>
<tr>
<th>Status</th>
<td>Tells you if the payment is awaiting submission, if it's successfully processed, or if it failed for some reason.</td>
</tr>
<tr>
<th>Status description </th>
<td>A descriptive text showing the reason related to the current status. Might contain the reason for cancellation or failure for example.</td>
</tr>
</table>
 
### Refund
The refund object is a child of the payment object. 

Refund contains both the request for a refund to occur and also the response once it has been processed. By default this object does not have an application tab and is only accessed as a related list to the relevant Payment record.

Refunds are processed by Salesforce users only, typically via a Salesforce "quick action" on the payment record.

Refund functionality is dependant on the Payment Service provider but typically you can do any number of partial refunds up to the amount of the original payment. For Direct Debit refunds are possible but come with added risk as it is very easy for a customer to request a refund for a Direct Debit payment direct from their bank and as such this is normally the recommended approach.

### Payment Schedule
Payment Schedule contains the information needed to drive the creation of payments where they need to recur automatically. Payment schedules have a lookup relationship with Authorisation.

Their only function is to create Payment records, linked to Authorisations (Saved Payment methods) on a fixed schedule so that these payments can be collected automatically.

Most of our customers use their own objects (such as invoices or orders) to drive the automatic creation of payment records rather than using payment schedules.

## Sandboxes
If cloning your org into a sandbox, you *must* make sure that any configuration data in the "Asperato ONE" custom settings object is *not* copied to the sandbox, and a separate configuration is set up on our staging server instead. If you need help with this, or want us to confirm your sandbox is not pointing at your live org, please email support@asperato.com with details.
