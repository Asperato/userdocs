---
id: packagestructure
title: Package Structure
sidebar_label: Package Structure
---

The package data objects are called `Payment`, `Payment schedule`, `Authorisation` and `Refund` and they are related to each other as per the diagram below.

![Authorisation has a reference to payment and payment schedule, payment schedule has a reference to payment](/userdocs/img/sf_diagram.png)

The following provides a description of the available Asperato ONE objects and their fields.

## Authorisation
<table>
  <tr>
    <th>Field</th>
    <th>Usage</th>
  </tr>
  <tr>
    <td>Account Name</td>
    <td>Records the name on the bank account or the cardholder name for future reference.</td>
  </tr>
  <tr>
    <td>Account Reference</td>
    <td>A partially obscured record of the bank account or credit card number for future reference.</td>
  </tr>
  <tr>
    <td>Asperato Repeat Token</td>
    <td>One of a pair of fields needed to make a repeat payment request.</td>
  </tr>
  <tr>
    <td>Billing Address City</td>
    <td>Records the city in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Billing Address Country</td>
    <td>Records the country in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Billing Address PostalCode</td>
    <td>Records the postal code in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Billing Address State</td>
    <td>Records the state/county in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Billing Address Street</td>
    <td>Records the street(s) in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Cancel Endpoint</td>
    <td>The link or URL that will be executed if the customer presses the cancel link on the payment page.</td>
  </tr>
  <tr>
    <td>Card Type</td>
    <td>The type of credit or debit card, or `Not Applicable` for the other Authorisation Types.</td>
  </tr>
  <tr>
    <td>Company Name</td>
    <td>Records the company name that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>CPA Granted</td>
    <td>Indicates that the customer has given permission for card details to be used to collect automatic payments.</td>
  </tr>
  <tr>
    <td>Customer ID</td>
    <td>This is the Asperato Customer ID.  It defaults to the value that is entered into the Asperato Getting Started page.  Under normal circumstances there is no need to interfere with this value.  It can be updated in the scenario where there are multiple Asperato Customer IDs in force in a single Salesforce org.</td>
  </tr>
  <tr>
    <td>Direct Debit Error Code</td>
    <td>In the event that the BACS system passes back an error response this will contain the raw BACS error code.</td>
  </tr>
  <tr>
    <td>eCommerce URL</td>
    <td>This is the URL needed to invoke the Asperato paypage is an eCommerce situation.  For example, this can be used to email someone a link by which to make a payment.</td>
  </tr>
  <tr>
    <td>Email</td>
    <td>Records the email address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Error Code</td>
    <td>This is a santised error code that is created by Asperato when a transaction fails.  It is based on the data that is returned from the Payment Service Provider(s). The actual codes are recorded in the <a href="#sanitised-responses">Sanitised responses</a> section of this document.</td>
  </tr>
  <tr>
    <td>Expiry Date</td>
    <td>The date on the which the authorisation will expire (if applicable).</td>
  </tr>
  <tr>
    <td>Fail Endpoint</td>
    <td>The link or URL that will be executed if the customer presses the 'Finished' button on the transaction error response screen.</td>
  </tr>
  <tr>
    <td>First Name</td>
    <td>Records the first name that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Last Name</td>
    <td>Records the last name that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Mandate Reference</td>
    <td>The reference for a Direct Debit mandate that will need to be displayed to the end customer in emails and other communication.</td>
      </tr>
  <tr>
    <td>Merchant group</td>
    <td>The merchant group that should be used for this transaction. The default merchant group will be used if left blank. More information on Merchant groups is available <a href="https://asperato.github.io/userdocs/docs/merchantgroups">here</a>.</td>
  </tr>
    <tr>
    <td>PSP Passthrough Parameters</td>
      <td>See <a href="https://asperato.github.io/userdocs/docs/psppassthrough">here</a>.</td>
  </tr>
  <tr>
    <td>Pass Thru Parameters</td>
    <td>A JSON REST format list of the parameters that were passed through from the starting URL.</td>
  </tr>
  <tr>
    <td>Payment Route Options</td>
    <td>One or more of of:
      <ul>
        <li><b>Card</b> Credit or debit card</li>
        <li><b>Direct Debit</b> Direct Debit</li>
        <li><b>eCheck</b>	US ACH Bank payment</li>
        <li><b>PayPal</b></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Payment Route Selected</td>
    <td>One or more of:
      <ul>
        <li><b>Card</b> Credit or debit card</li>
        <li><b>Direct Debit</b> Direct Debit</li>
        <li><b>eCheck</b> US ACH Bank payment</li>
        <li><b>PayPal</b></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Payment Service Provider Repeat Token</td>
    <td>One of a pair of fields needed to make a repeat payment request.</td>
  </tr>
  <tr>
    <td>Status</td>
    <td>The status of the authorisation.  Can be one of:
      <ul>
        <li><b>Pending</b> Has been created but is not yet active</li>
        <li><b>In Force</b> In force and ready to use</li>
        <li><b>Cancelled</b> Has been stopped</li>
        <li><b>Failed</b> Has failed for some reason</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Status Description</td>
    <td>A descriptive text showing the reason related to the current status.  Might contain the reason for cancellation or failure for example.</td>
  </tr>
  <tr>
    <td>Success Endpoint</td>
    <td>The link or URL that will be executed if the customer presses the 'Finished' button on the transaction success response screen.</td>
  </tr>
</table>


## Payment Schedule
<table>
  <tr>
    <th>Field</th>
    <th>Usage</th>
  </tr>
  <tr>
    <td>Authorisation</td>
    <td>A link to the related Authorisation object.  A Payment Schedule must have and entry here in order to process a payment.</td>
  </tr>
  <tr>
    <td>Authorisation Status</td>
    <td>A formula reflecting the status of the associated Authorisation.</td>
  </tr>
  <tr>
    <td>Final Payment Date</td>
    <td>After this date no more payments will be taken from this Payment Schedule</td>
  </tr>
  <tr>
    <td>Frequency</td>
    <td>The payment frequency for the Payment Schedule. One of:
      <ul>
        <li><b>Single</b></li>
        <li><b>Daily</b></li>
        <li><b>Weekly</b></li>
        <li><b>Monthly</b></li>
        <li><b>Quarterly</b></li>
        <li><b>Semi-annual</b></li>
        <li><b>Annual</b></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Last Payment Date</td>
    <td>The date on which the last payment request was raised.</td>
  </tr>
  <tr>
    <td>Next Payment Date</td>
    <td>The date on which the next payment request will be raised.</td>
  </tr>
  <tr>
    <td>Next Process Date</td>
    <td>A formula that calculates the next date on which a payment request should be processed.  This takes into account any delay caused by Direct Debit processing</td>
  </tr>
  <tr>
    <td>Payment Route Selected</td>
    <td>A formula reflecting the selected payment route of the associated Authorisation.</td>
  </tr>
  <tr>
    <td>Regular Amount</td>
    <td>The amount of the payment charge.  The currency will be determined based on the currency of the Payment Schedule record in a multi-currency org or from the org default currency for a single currency org.</td>
  </tr>
  <tr>
    <td>Status</td>
    <td>The status of the subscription.  Can be one of:
      <ul>
        <li><b>Active</b> In force and ready to use</li>
        <li><b>Inactive</b> Is stopped and therefore no payments will be processed</li>
        <li><b>Expired</b> Has been stopped because the Final Payment Date has been reached</li>
      </ul>
    </td>
  </tr>
</table>


## Payment
<table>
  <tr>
    <th>Field</th>
    <th>Usage</th>
  </tr>
  <tr>
    <td>Account Name</td>
    <td>Records the name on the bank account or the cardholder name for future reference.</td>
  </tr>
  <tr>
    <td>Account Reference</td>
    <td>A partially obscured record of the bank account or credit card number for future reference.</td>
  </tr>
  <tr>
    <td>Amount</td>
    <td>The amount of the payment.  Will contain either the requested amount of the amount actually collected depending on the status of the payment.</td>
  </tr>
  <tr>
    <td>Asperato Reference</td>
    <td>A unique reference to the payment transaction generated by Asperato and reflected through to the payment gateway.</td>
  </tr>
  <tr>
    <td>Asperato Repeat Token</td>
    <td>A formula reflecting the Asperato Repeat Token from the associated authorisation if appropriate.  Contains the text "Not set up yet" if there is no value.</td>
  </tr>
  <tr>
    <td>Authorisation</td>
    <td>A link to the related Authorisation object if appropriate.</td>
  </tr>
  <tr>
    <td>Billing Address City</td>
    <td>Records the city in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Billing Address Country</td>
    <td>Records the country in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Billing Address PostalCode</td>
    <td>Records the postal code in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Billing Address State</td>
    <td>Records the state/county in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Billing Address Street</td>
    <td>Records the street(s) in the billing address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Cancel Endpoint</td>
    <td>The link or URL that will be executed if the customer presses the cancel link on the payment page.</td>
  </tr>
  <tr>
    <td>Card Type</td>
    <td>The type of credit or debit card, or `Not Applicable` for the other Payment Types</td>
  </tr>
  <tr>
    <td>Company Name</td>
    <td>Records the company name that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Customer ID</td>
    <td>This is the Asperato Customer ID.  It defaults to the value that is entered into the Asperato Getting Started page.  Under normal circumstances there is no need to interfere with this value.  It can be updated in the scenario where there are multiple Asperato Customer IDs in force in a single Salesforce org.</td>
  </tr>
  <tr>
    <td>Direct Debit Error Code</td>
    <td>In the event that the BACS system passes back an error response this will contain the raw BACS error code.</td>
  </tr>
  <tr>
    <td>Due Date</td>
    <td>The date on which the payment is scheduled for collection.</td>
  </tr>
  <tr>
    <td>eCommerce URL</td>
    <td>This is the URL needed to invoke the Asperato paypage is an eCommerce situation.  For example, this can be used to email someone a link by which to make a payment.</td>
  </tr>
  <tr>
    <td>Email</td>
    <td>Records the email address that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Error Code</td>
    <td>This is a santised error code that is created by Asperato when a transaction fails.  It is based on the data that is returned from the Payment Service Provider(s). The actual codes are recorded in the <a href="#sanitised-responses">Sanitised responses</a> section of this document.</td>
  </tr>
  <tr>
    <td>Fail Endpoint</td>
    <td>The link or URL that will be executed if the customer presses the 'Finished' button on the transaction error response screen.</td>
  </tr>
  <tr>
    <td>First Name</td>
    <td>Records the first name that was captured on the payment page.</td>
  </tr>
  <tr>
    <td>Frequency</td>
    <td>A formula reflecting the payment frequency from the associated payment schedule if appropriate.</td>
  </tr>
  <tr>
    <td>Is Gift Card</td>
    <td>When checked this indicates that the payment was related to a gift card</td>
  </tr>
  <tr>
    <td>Last Name</td>
    <td>Records the last name that was captured on the payment page.</td>
  </tr>
    <tr>
    <td>Merchant group</td>
    <td>The merchant group that should be used for this transaction. The default merchant group will be used if left blank. More information on Merchant groups is available <a href="https://asperato.github.io/userdocs/docs/merchantgroups">here</a>.</td>
  </tr>
    <tr>
    <td>PSP Passthrough Parameters</td>
      <td>See <a href="https://asperato.github.io/userdocs/docs/psppassthrough">here</a>.</td>
  </tr>
  <tr>
    <td>Pass Thru Parameters</td>
    <td>A JSON REST format list of the parameters that were passed through from the starting URL.</td>
  </tr>
  <tr>
    <td>Payment Date</td>
    <td>The date on which the payment is either expected to clear or was cleared. <i>Note that this payment date is always in GMT, not the default timezone of the org.</i></td>
  </tr>
  <tr>
    <td>Payment Route Options</td>
    <td>One or more of:
      <ul>
        <li><b>Card</b> Credit or debit card</li>
        <li><b>Direct Debit</b> Direct Debit</li>
        <li><b>eCheck</b> US ACH Bank payment</li>
        <li><b>PayPal</b></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Payment Route Selected</td>
    <td>Shows the actual payment route that has been selected.  One of:
      <ul>
        <li><b>Card</b> Credit or debit card</li>
        <li><b>Direct Debit</b> Direct Debit</li>
        <li><b>eCheck</b> US ACH Bank payment</li>
        <li><b>PayPal</b></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Payment Schedule</td>
    <td>A link to the related Payment Schedule record if appropriate.</td>
  </tr>
  <tr>
    <td>Payment Service Provider Reference</td>
    <td>A reference to the payment generated by the payment gateway.</td>
  </tr>
  <tr>
    <td>Payment Service Provider Repeat Token</td>
    <td>A formula reflecting the repeat cross reference from the associated authorisation if appropriate.  Contains the text "Not set up yet" if there is no value.</td>
  </tr>
  <tr>
    <td>Payment Stage</td>
    <td>The status of the payment.  Can be one of:
      <ul>
        <li><b>Awaiting submission</b> Payment has been created but not yet processed</li>
        <li><b>Submitted for collection</b> Payment has been submitted to the PSP for processing but the outcome has not yet been determined</li>
        <li><b>Collected from customer</b> Payment has been collected successfully</li>
        <li><b>Failed</b> The payment attempt failed</li>
        <li><b>Expired</b> Select this stage if you wish to disable a payment link, ensuring that the payment cannot be processed. It can be re-activated again by changing the Stage to 'Awaiting Submission'.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Payment Stage Description</td>
    <td>A descriptive text showing the reason related to the current payment stage.  Might contain the reason for cancellation or failure for example.</td>
  </tr>
  <tr>
    <td>Process Date</td>
    <td>A formula that calculates the date on which a payment is scheduled to be processed.  Takes into account any delay caused by direct debit processing.</td>
  </tr>
  <tr>
    <td>Source</td>
    <td>The way the Payment was created.  Can be one of:
     <ul>
      <li><b>Web</b></li>
      <li><b>Holder not present</b></li>
      <li><b>Repeat</b></li>
     </ul>
    </td>
  </tr>
  <tr>
    <td>Success Endpoint</td>
    <td>The link or URL that will be executed if the customer presses the 'Finished' button on the transaction success response screen.</td>
  </tr>
  <tr>
    <td>Total Refunded</td>
    <td>This is a roll-up total of all the refunds that have been made against this Payment.</td>
  </tr>
  <tr>
    <td>Transaction Group</td>
    <td>This is a code that links separate payment records together to form a single transaction.</td>
  </tr>
</table>

## Refund
<table>
  <tr>
    <th>Field</th>
    <th>Usage</th>
  </tr>
  <tr>
    <td>Asperato Reference</td>
    <td>A unique reference to the payment transaction generated by Asperato and reflected through to the payment gateway.</td>
  </tr>
  <tr>
    <td>Direct Debit Error Code</td>
    <td>In the event of a direct debit payment failure this will show the detailed error code that was sent from either BACS or SEPA indicating the reason for failure.</td>
  </tr>
  <tr>
    <td>Error Code</td>
    <td>This is a santised error code that is created by Asperato when a transaction fails.  It is based on the data that is returned from the Payment Service Provider(s). The actual codes are recorded in the <a href="#sanitised-responses">Sanitised responses</a> section of this document.</td>
  </tr>
  <tr>
    <td>Payment</td>
    <td>The Salesforce ID that links the refund to the original payment</td>
  </tr>
  <tr>
    <td>Payment Date</td>
    <td>The date on which the payment is either expected to clear or was cleared.</td>
  </tr>
  <tr>
    <td>Payment Route</td>
    <td>Shows the actual payment route that has been used.  One of:
      <ul>
        <li><b>Card</b> Credit or debit card</li>
        <li><b>Direct Debit</b> Direct Debit</li>
        <li><b>eCheck</b> US ACH Bank payment</li>
        <li><b>PayPal</b></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Payment Service Provider Reference</td>
    <td>A reference to the payment generated by the payment gateway.</td>
  </tr>
  <tr>
    <td>Refund Amount</td>
    <td>The amount of the refund.</td>
  </tr>
  <tr>
    <td>Refund Stage</td>
    <td>The status of the refund transaction.  Can be one of:
      <ul>
        <li><b>Processing</b> Has been set to Asperato for processing.</li>
        <li><b>Refunded to customer</b> Has been refunded to the customer account.</li>
        <li><b>Failed</b> Has failed for some reason</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Refund Stage Description</td>
    <td>A descriptive text showing the reason related to the current refund stage.  Might contain the reason for failure, for example.</td>
  </tr>
</table>

## Asperato ONE settings

There are five fields in the ‘Asperato ONE settings’ custom settings in the Asperato package. These are described in the table below.

These settings are not routinely changed from the default values, unless specifically instructed to do so by the Asperato team. Changing the values could break your integration with Asperato. 

<table>
  <tr>
    <th>Field</th>
    <th>Usage</th>
  </tr>
  <tr>
    <td>BACS Delay</td>
    <td>The number of days grace to allow a DD payment to be processed by BACS. This is used to change a real Due Date to an artificial value so that the payment is collected from the bank account when it is actually due to be taken. The default value is created at installation and shouldn’t need to be amended unless there is a specific reason to do so.</td>
  </tr>
  <tr>
    <td>Create Payment Schedule</td>
    <td>Deprecated setting. Do not use.</td>
  </tr>
  <tr>
    <td>Customer ID</td>
    <td>This value will be populated with your Customer ID when the connection from Salesforce to Asperato has been established. The Asperato ONE package will not function without this value being set.</td>
  </tr>
  <tr>
    <td>Is Running Live</td>
    <td>The Asperato team will check this box as part of the go-live process.</td>
  </tr>
  <tr>
    <td>Server URL</td>
    <td>This is the URL of the server that Asperato will use to process payments, refunds and authorisations. At application download this is set to the test server route. For a live installation this will be amended by the Asperato team to point to the live server instance.</td>
  </tr>
  <tr>
    <td>Suppress Notification for Payments</td>
    <td>Introduced in release 2.16. And it is currently supported only with GoCardless Payments. If you have obtained <a href="https://asperato.github.io/userdocs/docs/suppressnotifications"> required approvals</a>, and if this setting is set to true, the Payment releated notifications from PSP would be suppressed. This would allow you to send your custom notifications for Payment.</td>
  </tr> 
  <tr>
    <td>Enable Pay/auth URL Data Integrity</td>
    <td> Introduced in release 2.17. When set true, an additional mechanism is used with the payment and authorisation URLs to enforce the data integrity of the payments and authorisations. It is recommended to enable it at all the times to maximise data protection and minimise GDPR exposure</td>
  </tr>
</table>
