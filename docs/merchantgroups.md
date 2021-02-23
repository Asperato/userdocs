---
id: merchantgroups
title: Merchant Groups
sidebar_label: Merchant Groups
---

**Note: This feature is available from version 2.13 of Asperato ONE. An Asperato Multi-Merchant License is required to enable this feature.**

## Introduction
The Asperato ONE PRO license allows for up to 5 connected Payment Service Providers (PSPs) settling into separate bank accounts of different currencies. If you require to settle into multiple bank accounts of the same currency you will need our Multi-Merchant License. For example, you may have a Stripe account for GBP and EUR card payments, a GoCardless account for GBP and EUR direct debit payments and a Cybersource account for USD card payments. However, if you need to connect a second Stripe account to use for a subset of GBP card payments, then an Asperato Multi-Merchant License is required. The Merchant Groups feature is used to manage this requirement. 
Before the introduction of Merchant Groups, Asperato customers were unable to set-up their multi-merchant license requirements themselves, instead the Asperato support team carried this out on their behalf. 

Merchant Groups enable you to set up different groups of PSP connections, and then assign those groups to different payments and authorisations.

Merchant Groups can be created and used in both lightning and classic. The screenshots here show the process in lightning experience, however it is near identical in classic. If you're struggling, just drop us a line at support@asperato.com and we'll do our best to help out.

## Upgrading from a previous multi-merchant configuration
If you hold an Asperato multi-merchant license and are using version 2.11 or earlier, then you can still upgrade to 2.13 and your package will function as before.

You can switch to using merchant groups instead, but this will require some configuration changes both in Salesforce and with Asperato. If you wish to do this, please email support@asperato.com for further instructions.

## In what situation would I want to use merchant groups?
You can use them however you wish. We find the most common use case is with different legal entities - a franchise for example may have a single Salesforce org managing a few hundred stores across a region, and each of those stores would have their own merchant PSP accounts. The merchant group functionality facilitates this use case by allowing a new merchant group to be set up per store.

Another use case could be when a merchant has a requirement to settle funds into separate bank accounts each with the same PSP and currency for regulatory reasons, for example paying household rent and deposit payments into separate bank accounts. 

## Is it possible to customise paypage with different templates for different merchant groups?
We recommend to use the default paypage template. But if there is a requirement to customise the paypages based on merchant group, then it is possible to make some basic changes. Please write to support@asperato.com with your requirement.

## Do I have to use merchant groups?
No. If, for any given currency and payment route, you only need a single PSP connected, then you can carry on using the package exactly as before, with no changes. The new merchant group functionality is backwards compatible. If you don't need to use it, your existing PSP connections, payments and authorisations will all be created and processed as before against a predefined "Default" merchant group.

## Creating a new merchant group
Head to the Asperato Setup page, and hit the "New group..." button:

![New group button](/userdocs/img/merchant_group/newgroupbutton.png)

Then type in the new group name in the dialog that appears. Be careful here - the group name *cannot* be changed later, aside from deleting and re-adding the merchant group.

![New group dialog](/userdocs/img/merchant_group/newgroupdialog.png)

You'll then see the new group created and selected on the setup page. It will be empty - you'll need to populate it with at least one PSP connection before you can use it:

![New group created](/userdocs/img/merchant_group/newgroupcreated.png)

## Adding PSP connections to a merchant group
To add a PSP connection to a merchant group, first select the group on the Asperato Setup page, then hit the "Add new connection" button.

For a more in-depth description of this process, see <a href="https://asperato.github.io/userdocs/docs/connectingpsp">here</a>.

Repeat the process of [Creating new merchant groups](#creating-a-new-merchant-group) and [Adding PSP Connections to the merchant groups](#adding-psp-connections-to-a-merchant-group) as many times as is required.

## Assigning a merchant group to a payment or authorisation
Assigning a merchant group to a payment or authorisation is just a case of populating the "Merchant Group" field with the correct merchant group name. For example, when creating a payment record on the Payment Object:

![New payment](/userdocs/img/merchant_group/newpayment.png)

...just fill in the "Merchant Group" field that appears to the right hand side of the "Amount" field with the appropriate Merchant Group name. (Note that when populating the Merchant group field via an API call, or via Apex, the field name needed is "asp04__Merchant_group__c".) When the payment or authorisation is then processed, it will be processed using the PSP connections specified in the merchant group that is entered in the "Merchant Group" field.

If the "Merchant Group" field is left blank then the "Default" merchant group will be assigned and used instead to ensure backwards compatibility.

## Assigning a merchant group to a repeat payment
For a merchant group to be assigned to a repeat payment (a payment attached to an authorisation), then the "Merchant Group" field on both the payment and authorisation objects *must* match exactly. If they do not, then the payment will not be processed but instead return a failure status of "Merchant groups must match."

## Assigning a merchant group to a payment schedule
There is no need to assign a merchant group to a payment schedule directly - the merchant group used will be the one that is set on the authorisation record(s) attached to the payment schedule.

## Renaming merchant groups
Merchant groups deliberately *cannot* be renamed, as this would break any automation in place that relied on the merchant group's name. If the group has to be renamed, it should be first deleted, then a new one created with the correct name, then the PSP connections re-established against the new group.
