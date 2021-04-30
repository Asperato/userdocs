---
id: authorisations
title: Authorisations
sidebar_label: Authorisations
---

## Overview of Authorisations in Salesforce
Authorisation records are used when you want to collect and save a payment method from one of your customers. The authorisation object in Salesforce is used to store a saved payment method that can authorise payments in the future. An authorisation can be created for any payment route aside from Paypal.
 
Saved payment method details, such as card or account number are always tokenised to protect you and your customer from fraud, don’t accept anything less.
 
Your customer can register multiple authorisations with you, so you could have both a card payment method on record as well as a Direct Debit mandate in place.
 
Asperato will always maintain these records, updating Salesforce with any state changes that you need to be aware of (such as if your customer cancels a direct debit.) Acting on these state changes is something you can do via Salesforce automation.
 
Key fields include:

<table>
<tr>
<th>Authorisation URL</th>
<td>This is the link you provide to your customer to enable them to provide authority to save a payment method.</td>
</tr><tr>
<th>Status</th>
<td>Tells you if the Authorisation is ready to use or not.</td>
</tr><tr> 
<th>Status description </th>
<td>A descriptive text showing the reason related to the current status. Might contain the reason for cancellation or failure for example.</td>
 </tr><tr>
<th>Payment Route Options</th>
<td>Allows you to choose which Authorisation routes are available to your customer to use. E.g. Card, Direct Debit or ACH</td>
</tr><tr>
<th>Payment Route Selected</th>
<td>Tells you which type of payment method has been granted by the customer.</td>
</tr></table>
 
Autorisations have to be ‘In Force’ before they can be used to collect payments.
 
 
## Required data 
“Available payment routes” is the only required field on the authorisation object. Optional address fields can be populated if necessary, which will pre-fill the payment page when the authorisation is processed.
 
## Statuses
The following statuses are available on the authorisation object:

<table>
<tr>
<th>Awaiting submission</th>
<td>The authorisation has not yet been processed through a payment service provider.</td>
</tr><tr>
<th>Pending</th>
<td>This status is used for direct debits, and indicates the authorisation has been processed but is not yet in force. Direct debit authorisations have a lead time of a few days before they become active - see <a href="https://support.gocardless.com/hc/en-gb/articles/360000593445-Timing-cycles" target="_blank">Timing cycles</a> for details. This status isn’t relevant for card authorisations, as they become active (or fail) instantly.</td>
</tr><tr>
<th>In force</th>
<td>The authorisation has been confirmed, is valid, and can be used to authorise a payment.</td>
</tr><tr>
<th>Submitted for Cancellation</th>
<td>Status value introduced in package version 2.16. This status is used for direct debit payments created using GoCardless connection. It shows that the mandate/authorisation has been submitted for cancellation at the request of the payor, or at your request. The status is automatically updated to Cancelled when the mandate is cancelled at GoCardless</td>
</tr><tr>
<th>Cancelled</th>
<td>The authorisation has been cancelled at the request of the payor, or at your request.</td>
</tr><tr>
<th>Failed</th>
<td>The authorisation is not valid / no longer valid and cannot be used to take payments.</td>
</tr><tr>
<th>Expired</th>
<td>The authorisation has expired, and can no longer be used to take payments.</td>
<tr>
</table>
 
## Creating and Requesting Authorisations
 
An Asperato Authorisation is completed in 2 steps as follows:

(1) Creating an Authorisation Record in Salesforce;

(2) Processing an Authorisation.

### Creating an Authorisation Record in Salesforce
An authorisation can be created manually in Salesforce by clicking the "New" button on the Authorisation object, completing the details and saving the record. 

### Processing an Authorisation
Authorisations can either be processed internally to the org (for example, if an agent in a call centre was taking details over the phone to set up an authorisation) or externally (if a link to setup the authorisation is required outside of Salesforce.)
 
The Asperato package can cover both of these use cases.
 
To process an authorisation internally, hit the “Process authorisation” button. This will appear as a standard button in classic, and a quick action in lightning:
 
![Process authorisation button](/userdocs/img/auth/process_authorisation.png "Process authorisation button")
 
An overlay will appear showing the payment form. When this form is submitted, details of the authorisation will then show on the Salesforce object:
 
![Auth details](/userdocs/img/auth/auth_details.png "Auth details")
 
To supply a link for processing externally, look for the “Ecommerce URL” field on the authorisation object:
 
![ECOM URL](/userdocs/img/auth/auth_ecom_url.png "ECOM URL")
 
This will contain a URL pointing to a webpage for the user to enter their details to set up the authorisation, and can be distributed by any means necessary (email, IM, etc.) When the user has completed the form, the authorisation object will be populated in Salesforce the same way as before.

## Viewing GoCardless Authorisation/Mandate (2.16+)
To view the mandate click on "View Mandate" quick action button on the Authorisation record.

![View mandate button](/userdocs/img/auth/viewmandate.PNG "View mandate button")

Clicking on the button will open the mandate (as saved with GoCardless) in a new tab of the browser.

## Updating a GoCardless Authorisation/Mandate

Updating a GoCardless Authorisation/Mandate can be done internally to the Salesforce Org (for example, if an agent in a call centre was taking details over the phone to set up an authorisation) or externally (if a link to setup the authorisation is required outside of Salesforce.)

To update an authorisation manually, hit the “Process authorisation” button on the authorisation record in Salesforce. 

![Process authorisation button](/userdocs/img/auth/process_authorisation.png "Process authorisation button")

An overlay will appear containing the payment form, the updated details should be entered on this form and submitted. This will create a new mandate in GoCardless rather than update the details on the existing one, all new payments against the updated Asperato authorisation record will use the newly created GoCardless mandate. 

To supply a link for processing externally, look for the “eCommerce URL” field on the Asperato authorisation record:

![ECOM URL](/userdocs/img/auth/auth_ecom_url.png "ECOM URL")

This will contain a URL pointing to a webpage for the user to enter their updated details to ‘update’ the authorisation. When the user has submitted the form, the Asperato authorisation record will be populated with the updated details. As above, this will create a new mandate in GoCardless rather than update the details on the existing one, all new payments against the updated Asperato authorisation record will use the newly created GoCardless mandate. 

## Cancelling a GoCardless Authorisation/Mandate
For users running on Asperato **package 2.15 and below**, this has to be done directly on the GoCardless by logging in to your GoCardless Dashboard.

For users running Asperato **package 2.16+**, to cancel mandate
+ Go to Authorisation that needs to be cancelled
+ Select Quick Action “Cancel Mandate”

![Cancel mandate button](/userdocs/img/auth/cancelmandate.PNG "Cancel mandate button")

+ You will see a confirmation screen. Upon confirming the mandate will be cancelled at both SF and GC side and the status of authorisation record would be updated to "Cancelled".

![Cancel mandate confirmation screen](/userdocs/img/auth/cancelmandateconfirmationscreen.PNG "Confirmation Screen")

Note that, if the same Authorisation record, which was cancelled earlier, is processed from the SF then
+ In SF the same Authorisation Record will be updated from Cancelled to Pending status
+ In GC, a new Customer record would be created

Clicking on the button will open the mandate (as saved with GoCardless) in a new tab of the browser.

## Custom references (2.13+)

Some PSPs allow you to specify a custom reference attached to an authorisation. You can specify this by using the "Custom reference" field available on the authorisation object.

However, note that not all PSPs or PSP account types support custom references, and some often have restrictions on the maximum length of a reference. You should check your PSPs documentation for any rules around specifying custom references. Note that setting a custom reference where they are not supported, or setting an invalid custom reference may cause a transaction to fail.

## Importing Authorisations to Salesforce
 
If you require existing authorisations from your PSP to be populated in Salesforce, then please contact support@asperato.com with details of your requirements.

## Notes for existing users upgrading to 2.16 package

If you upgrading to package 2.16 then ask your salesforce admin to update the authorisation <a href="https://help.salesforce.com/articleView?id=sf.customize_layout.htm&type=5"> _page layout_</a> to include
+ "View Mandate" quick action button
+ "Cancel Mandate" quick action button
+ Authorisation status "Submitted for Cancellation"
