---
id: successplus
title: GoCardless Success+ Support to Automatic Retry Failed Payment
sidebar_label: Success+ Support
---

# Overview
GoCardless Success+ is a feature to intelligently retry a failed payment. You can read more about it <a href="https://gocardless.com/gc/success-plus/">here</a>.

# Using GoCardless Success+

## Enable Success+ in GoCardless Account
You need to enable Success+ separately for each currency from GoCardless Dashborord

## Enable Success+ support in Asperato Package
You need to write to support@asperato.com to get this feature enabled in Asperato app. We will confirm you once this setting is enabled.

## How it works?
After required configurations are done, then asperato package will inform the gocardless to retry the payments and GoCardless will take care of your payments as per the settings done in GoCardless account.
It works as following
+ A payment is created in Asperato
+ Aspearto informs Gocardless about
++ New payment being created
++ Availability of permission to Retry the Payment if it fails
+ Payment status changes to Submitted for Collection
+ Payment collection fails
+ Status of payment changes to "Retry in Progress"
+ Payment is resubmitted for collection as per the settings done in the GoCardless Account.
+ if payment collection is successful, status on payment changes to "Collected from Customer"
+ if the retry attempts are exausted and still payment could not be collected then the payment status is updated to "Failed"

Please Note, if you have enable success plus at both the places, GoCardless and Asperato, then it is recommended to not take payment from an alternative route when payment status is "Retry in Progress".
