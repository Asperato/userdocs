---
id: testing
title: Testing Payments
sidebar_label: Testing
---

Once you have completed the setup steps in Asperato, or are in the process of adding configuration it is likely that you will want to complete some test payments. 
 
 - Please note that this guidance is for testing payments whilst in test mode only. 
 - Please note that only test payment methods can be used whilst in test mode,  live card or bank details must never be used as the test environment is not PCI compliant.
 
The following article gives you a little guidance to successful testing.
 
## Identifying failed Payments and Authorisations.
Every payment  or authorisation request you make with the Asperato solution will come back with an outcome, be it successful or failed. If a transaction succeeds, the payment or authorisation stage will show “Success”. If a transaction fails, the outcomes are detailed on the associated payment / authorisation records.  Find them as follows: 
 
### Failed Authorisation

<table>
<tr>
<td>Status</td>
<td>Failed. (Has failed for some reason)</td>
</tr>
<tr>
<td>Status Description</td>
<td>A descriptive text showing the reason related to the current status. Might contain the reason for cancellation or failure for example.</td>
</tr>
<tr>
<td>Direct Debit Error Code</td>
<td>In the event that the BACS system passes back an error response this will contain the raw BACS error code.</td>
</tr>
<tr>
<td>Error Code</td>
<td>This is a santised error code that is created by Asperato when a transaction fails. It is based on the data that is returned from the Payment Service Provider(s). These codes can be used to automate outcome responses. </td>
</tr>
</table>
 
### Failed Payment

<table>
<tr>
<td>Payment Stage</td>
<td>Failed. (The payment attempt failed)</td>
</tr>
<tr>
<td>Payment Stage Description</td>
<td>A descriptive text showing the reason related to the current payment stage. Might contain the reason for cancellation or failure for example.</td>
</tr>
<tr>
<td>Error Code</td>
<td>This is a santised error code that is created by Asperato when a transaction fails. It is based on the data that is returned from the Payment Service Provider(s). These codes can be used to automate outcome responses. </td>
</tr>
</table>
 
### Failed Refund
 
<table>
<tr>
<td>Refund Stage</td>
<td>Failed Has failed for some reason</td>
</tr>
<tr>
<td>Refund Stage Description</td>
<td>A descriptive text showing the reason related to the current refund stage. Might contain the reason for failure, for example.</td>
</tr>
<tr>
<td>Direct Debit Error Code</td>
<td>In the event of a direct debit payment failure this will show the detailed error code that was sent from either BACS or SEPA indicating the reason for failure</td>
</tr>
<tr>
<td>Error Code</td>
<td>This is a santised error code that is created by Asperato when a transaction fails. It is based on the data that is returned from the Payment Service Provider(s). These codes can be used to automate outcome responses. </td>
</tr>
</table>
 
Asperato sanitise each and every message that comes back from the PSPs,  making it simpler for you to handle them:
https://asperato.github.io/userdocs/docs/payments#payment-outcomes
 
## Testing Card Payments
The process of testing card payments is fairly simple.  The user must enter the card details as required on the Asperato payment page,  each card gateway has its own set of agreed test card numbers, these can be found by heading to your chosen gatewaywebsite and searching for test card details.
 
Responses from card gateways will the outcome of your test will be almost instantaneous. You should get a result into the Asperato payment record quickly, but may need to refresh the record to see the result.
 
To check which card gateway you are using, head to the asperato setup page and check details against each currency you have set up.
 
### Failed card payment scenarios 
In some cases you will want to test certain scenarios,  to ensure that the outcomes are being passed back to the relevant record. For example, failed payments due to insufficient funds,  card expired etc  Again each PSP has its own set of agreed mechanisms for doing this. They can be found by heading to your chosen PSP website and searching for test cards.  Typical methods for doing this include using specific card numbers, payor names or amounts. If at any point you struggle to find the details please drop an email to support@asperato.com and we can try to assist.
 
## Testing Direct Debit (GoCardless)
 
Testing Direct Debits is mildly more complex due to the timing cycles involved. 
 
If you set up a  mandate or attempt to process a payment there are certain delays involved when receiving an outcome.  These delays can cause challenges (or lots of tea drinking) for testing / development.
 
For example the time it takes between setting up a mandate and confirming a mandate in the UK is around 3 days,  a long time to wait if you're testing.  The way to get around this is to use what are called Scenario Simulators offered by GoCardless.
 
Given the nature of the Asperato integration we suggest using the “Name triggered scenarios”, details of which can be found here:
https://developer.gocardless.com/developer-tools/scenario-simulators
 
For full details of different timing cycles please ask your Direct Debit provider: here we give a link to the BACS UK timings: https://support.gocardless.com/hc/en-gb/articles/210535689-Bacs-UK-Payment-Timings
 
## Testing payments in live mode
Once you go live it is also strongly recommended that you process a few test transactions to ensure that your PSP and Asperato is configured correctly. 
 
To do this, you will require live payment credentials and you will likely want a method to refund them too.  Please note that there is no way to speed up live testing of Direct Debit payments.
