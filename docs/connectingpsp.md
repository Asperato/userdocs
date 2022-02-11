---
id: connectingpsp
title: Connecting your PSP
sidebar_label: Connecting your PSP
---

Asperato ONE comes pre-configured with several different PSP connections so you can test payments out of the box. However, with this you are limited to the results that you see in Salesforce - you cannot view the payments as they flow through the PSP.

To test thoroughly therefore, you'll need to connect your own PSP account.

**Please note that the steps detailed here are correct at the time of writing, but PSPs do change them from time to time, so they may not be up-to-date. If you notice any that aren't correct, please email support@asperato.com so that we can get them updated.**

## Connecting your own PSP account

To connect your own PSP account, you first need to make sure you're in lightning experience - see here for instructions on how to switch to lightning experience if you're not already using it. (Don't worry, you can switch back to classic if you wish as soon as setup is complete.)

Once you are in lightning experience, navigate to the "Asperato Setup" tab and then follow the instructions below:

1. Click the "New PSP connection" button on the "PSP connections" lightning component:

![Add new connection](/userdocs/img/merchant_group/newgroupbutton_R2_17.png)

2. In the dialog that appears, select:

 - The currency this connection will be used for
 - The mode (such as ECOM, MOTO, direct debit, etc.)
 - The PSP you wish to connect. *(PSP not in that list? Don't worry, we're always adding more. Email support@asperato.com and we'll see what we can do.)*
 - An optional description of this PSP connection (such as "Wholefood Tavistock branch".)

3. You will get to select option to "Use Custom Gateway Details" or "Use Asperato Gateway Details"

4. Select option "Use Custom Gateway Details". The dialog will then ask you to enter the keys required for the PSP you have selected. You will need to obtain these from your PSP (instructions can be found below for some PSPs.) When you've entered all the details, it should look something like this:

![New connection dialog](/userdocs/img/adding_psp/new_connection_dialog_R_2_15.PNG)

5. Click the "Create PSP connection" button.

The "PSP connections" component should now be updated with your new gateway connection - if all has worked ok, you'll see a green tick by your newly added connection.

If you instead see a red cross, that means we had an issue trying to connect to your PSP with the details that you provided. If you see this, try entering your details again. If you still can't connect successfully, then email support@asperato.com, let us know the details of the PSP you're trying to connect to, and we'll see what we can do to help.

## Test account details

Note that test account details will vary between payment service providers - they each have their own set of test details, though there are some "common" ones used across providers. Most PSPs have pages online where they supply such test details.

## IP whitelisting

Some Payment Service Providers require the Asperato service to have an IP whitelist entry in order to process transactions.  If that applies then use these values:

For TEST

- 35.179.25.58

For LIVE

- 35.177.118.40

Where a subnet mask is required then use the value 255.255.255.255

Where CIDR notation is required add /32 to the end of the addresses above.

## Payment service provider keys

Asperato will require keys to connect to a user's payment service provider.

Unfortunately, retrieving these keys is not consistent across providers. For PSPs listed here, you should be able to find the keys using the following instructions. For those not listed, you will need to contact your payment service provider for instructions.

### Adyen
To connect Adyen to Asperato you will need:

- Merchant account
- API Key
- Url Prefix

The Merchant account dictates the name of the Adyen account you wish Asperato to connect to; it is not a piece of authentication data. You can view instructions for obtaining your API key <a href="https://docs.adyen.com/user-management/how-to-get-the-api-key/">here</a>.
URL prefix is a combination of [Random]-[Companyname]. You can use any value when creating connection on staging. However, to create connection on Live server, you can get this information from you Live Customer Area > Account > API URLs. Read more about URL prefix <a href="https://docs.adyen.com/development-resources/live-endpoints#live-url-prefix">here</a>.

### Authorize.net
To connect Authorize.net to Asperato you will need the values for:

- API Login ID
- Transaction Key

If you don't know what these values are you can create new ones, but beware that this will expire the old ones and will there affect anything that is communicating with Authroize.net via their API.

Go to `Account > Settings > API Credentials & Keys`

### Braintree
The information Asperato needs can be obtained from the Braintree Dashboard.

For test/sandbox this is at <a target="_blank" href="https://sandbox.braintreegateway.com/login">https://sandbox.braintreegateway.com/login</a>

For live/production this is at <a target="_blank" href="https://www.braintreegateway.com/login">https://www.braintreegateway.com/login</a>

On the top of the dashboard screen there is an Account option, and under that appears a `My User` option when you hover over it.

In the My Account screen, towards the bottom, is a section entitled "API Keys, Tokenization Keys, Encryption Keys".  Click on "View Authorizations".

You need to create a new API Key.  Click on the button marked "Generate New API Key".  This will create a new key.  In the line that appears on the screen there is a View link under the heading "Private Key". Click on that.

Asperato then needs the values of the fields marked:<br/>
- Public Key<br/>
- Private Key<br/>
- Merchant ID

### Checkout.com
The information that Asperato needs can be obtained from the Checkout.com administration website, which they call "The Hub".
There is a single piece of information for the configuration, the "Secret key".

For test/sandbox this is:
<a target="_blank" href="https://sandbox.checkout.com/login">https://sandbox.checkout.com/login</a>
<br/>
For live:
<a target="_blank" href="https://.checkout.com/login">https://hub.checkout.com/login</a>
https://hub.checkout.com/login

When you log in, it displays the dashboard, on the left hand menu, click settings, then channel. This will display a page showing the secret key.

You can get a test account directly from their website, however you will have to contact their support team 
(support@checkout.com) so that they can enable the "Full Card details API".

### Cybersource
The information that Asperato needs can be obtained from the Cybersource Enterprise Business Center dashboard.

The Merchant ID is shown on the banner segment on the top of the page.

To generate a Security Key select the "Payment Configuration" option on the left-hand menu, followed by "Key Management".  The press the "+ GENERATE KEY" button.
The type of key should be "Transaction Processing" and the key sub-type should be "SOAP".  The security key will then be displayed.  You should make a copy of this key because it is the only time that it will be shown.

### Forte
The information that Asperato needs can be obtained from the Forte DEX dashboard.

The login page for this is at <a target="_blank" href="https://login.forte.net/account/login">https://login.forte.net/account/login</a>

The Asperato connection requires four bits of information:
- The organisation ID
- The location ID
- API Access ID
- API Secure Key

On the left of the dashboard is a menu. Select the `Developer` option and within that `API Credentials`.  You will need to add a new set of API keys by pressing the `Create` button and giving them a name.  That will then show a screen containing an API Access ID and an API Secure Key.  You need to make copies of these while this screen is displayed because the API Secure Key will not be visible again at any time.

The Organisation ID is the number displayed under the company name on the top left of the desktop itself.

The Location ID is the number displayed under the location name when you select the `Locations` option on the left-hand menu.

### GoCardless
Asperato will redirect you to the GoCardless sign up page to complete your details to obtain a GoCardless account. If you already have a GoCardless Account click the Sign in link at the bottom of the form and enter your details as required. Once complete you will see a message from Asperato confirming the connection.

### IntelliPay
We need two pieces of information:
 - Merchant Key
 - API Key

### Moneris
For testing you will need a username, a store ID and an API key.

1. Sign in at https://developer.moneris.com/ with your username and password (or create an account if you don't have one.)

2. Under "My Profile" on the right hand side, scroll down until you see the "Credentials" section.

3. This should contain the store ID and the API key.  (The other value, your username, is the same that you use to login.)

For the live keys you need to log into your live merchant account at https://esqa.moneris.com/mpg/index.php

Once you are logged in there is an Admin menu option and within that a section called Store Settings.  The API key is displayed at the top of the page.

Asperato require the live store ID and the live API key.

### Paragon

The following information should have been provided by email from Paragon when you opened your account.  If you no longer have that information then you will need to contact Paragon support and request it (ISVgatewaysupport@paragonsolutions.com)
The two bits of data that Asperato requires are:
- Username (API Username)
- Password (API Password)

### Payline

The following information should have been provided by email from payline when you opened your account.
If you have forgotten this information, you will find it on your contract or by contacting Payline support:
- Contract number (This is the VAD (vente à distance) contract number.  For testing this might be a fake one such as "7654321".)
- Merchant ID (Also called "Merchant's Login" or "Identifiant Commerçant", a long numeric field.)
- Access key. (A long alphanumeric key.)

It is possible to find, or create a new Access key from their admin web site, however you will still need information provided by Payline, usually sent to you via email when you set up the account.

To get into site, you will need the following information:
- Merchant's Login ("Identifiant Commerçant" , a long numeric field, as above) 	
- User ID  ("Identifiant utilisateur",  An email address, set up when the account is created).
- Password  

The URLs are:
Test: <a href="https://homologation-admin.payline.com" target="_blank" title="Link to developer dashboard"> https://homologation-admin.payline.com </a>
Live: <a href="https://admin.payline.com" target="_blank" title="Link to production dashboard"> https://admin.payline.com </a>

Under the "settings" tab, click on "Change your access key" to either view or change the access key. 
(or "Configuration", "Gestion des clés d'accès").

For more information on setting up a Payline accounts, see the following:
<a href="https://payline.atlassian.net/wiki/spaces/DT/pages/32079931/Int+gration+pas+pas" target="_blank" title="link to Payline documentation in french"> https://payline.atlassian.net/wiki/spaces/DT/pages/32079931/Int+gration+pas+pas (French)</a>
<a href="https://payline.atlassian.net/wiki/spaces/DT/pages/1052409996/Getting+Started+Guide" target="_blank" title="link to Payline documentation in English"> https://payline.atlassian.net/wiki/spaces/DT/pages/1052409996/Getting+Started+Guide (English).</a>


### PayPal
Asperato will need your Client ID and Secret Key.  You can find these in the PayPal developer dashboard.

Go to <a href="https://developer.paypal.com" target="_blank" title="Link to developer dashboard">https://developer.paypal.com</a> and use your PayPal business credentials to log in.

In the options shown on the top right select `Dashboard`.  In the `My Apps & Credentials` menu option there is a section called `REST API apps`.  If no App already exists then click on the `Create App` button and give your new app a suitable name.

Once an App exist you can click on its name in the `REST API apps` section and the keys we need are displayed.  The two keys are Client ID and Secret.  Make sure you select either Sandbox or Live in the box on the top right of the screen to get either the test or live keys as appropriate.

Although not directly related to keys there are some other considerations for using PayPal as a payment route.  The main issue is that PayPal will not let you run any of their screens in an iframe or overlay, and outside of this the whole process is managed by re-direction.  This means that you will need to use the Asperato PostMessage event `asp--redir` to determine where the redirection should go to when using iframe techniques.  The documentation about the Asperato PostMessage events can be found <a href="https://asperato.github.io/userdocs/docs/paypage#postmessage-events" target="_blank" >here</a>.<br/>
The other set-up issue you need to consider is that because the PayPal payment is managed by re-direction you need to set the Cancel, Success and Fail endpoints on the payment record before you launch the Asperato paypage so that you can control what happens when the payment transaction completes.  The description of these fields can be found <a href="https://asperato.github.io/userdocs/docs/payments#post-transaction-endpoints" target="_blank">here</a>.

### SagePay (Opayo)
Asperato will ask you for your Vendor name to connect to SagePay. This is the same as your SagePay account credentials. If you do not know these, contact your SagePay Administrator.

There is an additional configuration task you will need to perform in order to allow Asperato to talk to the SagePay gateway (for both the test and live environments) because SagePay perform valid IP checks:

- Log into the SagePay desktop
- Under the Settings tab there is a Valid IPs option, select that
- Press the Add button
- For testing set the IP address to 035.179.025.058, the Subnet mask to 255.255.255.255 and the Description to Asperato test
- For live running set the IP address to 035.177.118.040, the Subnet mask to 255.255.255.255 and the Description to Asperato live

### Stripe
You will need your API key to connect Stripe to Asperato.
Your API keys are located in your account settings (there is a menu option on the left called `API`).  The key that we need is called the Secret key and you might need to press a button to reveal the value)

If you do not see your API keys, this means that you are not an administrator for the account.

You will need to get in touch with the administrator of your account for the API keys or to request that they make you an administrator in the account’s team settings.

Stripe have implemented a new set of security rules to discourage merchants who might not have implemented appropriate security measures from processing raw card data.  The knock-on effect is that Asperato, who are Level 1 PCI-DSS compliant, will get blocked from processing transactions on your behalf unless this new feature is disabled.  By checking this box you do lot lessen the security of your transactions processed via the Asperato solution (despite Stripe's statements). We are investigating possible solutions with Stripe that do not negatively impact our customers on price or service.

To enable Asperato to take payments on your behalf you will need to make an update to your Stripe configuration.

Go to the URL: <a href="https://dashboard.stripe.com/settings/integration" target="_blank">https://dashboard.stripe.com/settings/integration</a>

 - Log into Stripe, and on the page that displays enable the 'Handle card information directly' link.<br/>
 - This will open a box with three statements that you have to agree to.<br/>
 - The last statement will open a drop down field where you need to select "I collect payment information securely through a PCI compliant third party vendor".<br/>
 - Finally, enter "Payonomy Limited T/A Asperato" in the required text box and press the 'Continue' button:

![Stripe direct API dialog](/userdocs/img/stripe_config_new.png "Stripe direct API dialog")

Stripe might then ask you to verify you phone number, but once that is complete then you'll be able to process transactions.

### TakePayments
We need below details to create connection
 - Merchant ID / gateway account ID – This can be found in the Take payments Merchant Management System (MMS), under "Account Admin" -> "Gateway Account Admin".
 - Merchant password – This can also be set/reset in the Take payments Merchant Management System (MMS), under "Account Admin" -> "Gateway Account Admin".

In case facing issue with finding the details, it is recommended to contact TakePayments support

### Vanco
We need four pieces of information:
 - Username
 - Password
 - Client ID
 - Encryption key
 
 This information can be obtained from the setup emails sent by your integrations specialist. If you do not have an integrations specialist or have mislaid the original emails, then you'll need to <a target="_blank" href="http://connect.vancopayments.com/contact-vanco">contact Vanco</a> and ask them for this information.

### Vantiv (Worldpay)
We need three pieces of information:
 - Merchant Code
 - Username 
 - Password

These are supplied by Vantiv for both their pre-live and live environments.  These are different to any credentials used to log on to the Vantiv Merchant Management Service.

### Worldpay Online
You need to log onto the <a target="_blank" href="https://online.worldpay.com/login">Worldpay Online Dashboard</a>.
- Ensure you are in TEST mode.
- On the top right of the screen click on `SETTINGS`.
- Select the tab entitled `API Keys`.
- We need the Service key & Client key.
