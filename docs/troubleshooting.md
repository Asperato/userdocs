---
id: troubleshooting
title: Troubleshooting
sidebar_label: Troubleshooting
---

Please ensure you are running the latest version of Asperato ONE. New packages, containing new bugfixes, are constantly being released. If you are having issues, as the first port of call please check if you are using the latest package version and upgrade if necessary:

<a target="_blank" href="https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000EcrOnUAJ">https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000EcrOnUAJ</a>

If you are having issues that this page doesn't help you resolve, please email support@asperato.com with details of your issue.

## Can't collect refunds
This is likely to be one of a few scenarios:
 - Refunds are not enabled by your payment processor. If this is the case, you'll need to contact them to get this enabled.
 - A refund is not possible on this payment because of a restriction by your payment processor. Again, you'll need to contact them to find what this is - some processors only allow a certain number of refunds on a single payment, some only allow refunds after a certain length of time has passed, etc.
 - Your user does not have the required permissions to issue refunds. Asperato ships with an "Asperato refund user" permission set which you'll need to apply to the Salesforce user in question to allow them to issue refunds.
 
## The "Asperato Setup" page is blank
You'll need to enable, and deploy "My Domain" to you users before you can view the "Asperato Setup" page. <a href="https://help.salesforce.com/articleView?id=domain_name_overview.htm&amp;type=5" target="_blank">Please see instructions from Salesforce on how to do this</a>.

## Can't complete setup - an error dialog appears
If an error dialog appears when you try to setup Asperato, it may be because you didn't allow the remote sites during setup.

To check this, from Setup, enter Remote Site Settings in the Quick Find box, then select Remote Site Settings. This page displays a list of any remote sites already registered and whether they're active. This is what you should see if the remote sites are configured correctly:

![Remote site settings](/userdocs/img/troubleshooting/remote_site.png)

If not, the "Active" checkbox may be unchecked. If that's the case, you'll need to hit the "Edit" link by each remote site to activate it.

## A transaction has been processed by my PSP, but is still marked as "Pending" or "Awaiting submission"
This is usually caused by Salesforce blocking an update that we tried to post. If this is the case, you should have a "courtesy notification email" with details of what we tried to update, and what stopped us updating it (usually a trigger or flow that failed.) If that doesn't appear to be the case, please email support@asperato.com quoting the "Asperato reference" field of the relevant payments and authorisations so that we can investigate.
