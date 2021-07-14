---
id: suppressnotifications
title: Guide to Suppressing Payment Notification of GoCardless for Subscription Payments
sidebar_label: Suppress Payment Notifications of GoCardless
---
# Overview
This feature will allow GoCardless customers  to manage the advance payment collection notices  sent to customers, rather than using the GoCardless emails. This will not affect the mandatory emails which are part of the BACS Scheme rules (e.g. the emails sent following Direct Debit set up). To use this feature you need to complete the mandatory approval process and package configuration as described below.

# Approval Process
To be able to handle customer notifications yourself, you will need to be granted permission by GoCardless. It is a two step approval process when you are using GoCardless connection with Asperato to ensure compliance with Direct Debit scheme rules
1. Write to GoCardless Support at help@gocardless.com.  Mention that you wish to handle “payment_created” notification for all the schemes that you intend to use (eg., SEPA, BACS, BECS, PAD, ACH, etc.).  Please note that to GoCardless, you will have to individually mention the schemes for which you intend to handle the notifications. Refer GoCardless documentation [here](https://support.gocardless.com/hc/en-us/articles/115003735105-Custom-notifications). Check in the section “Getting custom notifications enabled” for more information.
2. Write to Asperato Support at support@asperato.com to enable the suppression of GoCardless Notifications for Payments being created.We are required by GoCardless to see evidence of your handling of notifications. For this purpose our Customer Success team would ask you to complete a self-signed form and provide the confirmation email from GoCardless. Once we have these two documents our team would enable this feature for your Salesforce org.

# Configuration in Asperato Package
After getting the required approval you do following configurations in the AsperatoOne package
+ Login to Salesforce org where the AsperatoOne package is installed.
+ Go to Setup
+ Write “Custom Settings” in the quick find box
+ Click on “Custom Settings”
+ Go to Asperato One settings
![Aspertao One Settings - Custom Settings](/userdocs/img/supress_payment_notification/AsperatoOneSettings.png "Custom Settings")
+ Click on Manage
+ Set the value of “Suppress Notification for Payments” as true
![Suppress Notification field - Custom Settings](/userdocs/img/supress_payment_notification/CustomSettings.png "Custom Setting Value")
+ Save the changes

# Suppressing Notification for Payments
## Single Payments
### Creating Payments from Authorisation Record
+ Go to Authorisation record, against which to take payment
+ Click on Process Payment using Authorisation
+ Check the “checkbox" as true. Refer below diagram
![Checkbox on Process Payment screen](/userdocs/img/supress_payment_notification/paymentscreen.PNG "Process Payment Screen")
+ Click on Process Payment.

### Creating Payments from Payment tab
+ Go to Payments tab -> Click on New
+ Enter the required details
+ In the “Payment Reference Information” section, set the value of “Suppress Notification by PSP” to True if you don't want the GoCardless notifications to be sent to customers.
![Payment Page Layout](/userdocs/img/supress_payment_notification/paymentpagelayoout.png "Payment Page Layout")

## Recurring Payments
### Payments Created by Payment Schedule
+ After getting necessary approvals, check section <a href = "https://asperato.github.io/userdocs/docs/suppressnotifications#approval-process"> “Approvals” </a>, if the value of the custom setting field "Suppress Notification for Payments" is set to true, as mentioned in section “Configuration in Asperato Package”, then all the payments created by payment schedule will have the value of “Suppress Notifications by PSP” set as True.
+ So, for the payments created by payment schedule the GoCardless notifications would be suppressed.
