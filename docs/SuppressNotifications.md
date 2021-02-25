---
id: suppressnotifications
title: Guide to Suppressing Payment Notification of GoCardless for Subscription Payments
sidebar_label: Suppress Payment Notifications of GoCardless
---

# Approval Process
To be able to handle customer notifications yourself, you will need to be granted permission. It is a 2 step approval process when you are using GoCardless connection with Asperato
1. Write to GoCardless Support at help@gocardless.com to handle “payment_created” notification for all the schemes that you intend to use (eg., SEPA, BACS, BECS, PAD, ACH, etc.). Please note that to GoCardless, you will have to individually mention the scheme for which you intend to handle the notifications.
2. Write to Asperato Support at support@asperato.com to enable the suppression of GoCardless Notifications for Payments being created.We are required by GoCardless to see evidence of your handling of notifications. Details will be provided.

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
![Cancel mandate button](/userdocs/img/auth/cancelmandate.png "Cancel mandate button")


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
![Payment Page Layout](/userdocs/img/supress_payment_notification/paymentpagelayoout.png, "Payment Page Layout")

## Recurring Payments
### Payments Created by Payment Schedule
After getting necessary approvals, check section “Approvals”, if the value of the custom setting field is set to true., as mentioned in section “Configuration in Asperato Package”, then all the payments created by payment schedule will have the value of “Suppress Notifications by PSP” set as True.
So, for the GoCardless notifications for payments created by payment schedule (As mentioned in above point) notifications would be suppressed.
