---
id: scasupport
title: SCA Support
sidebar_label: SCA Support
---

The Financial Conduct Authority (FCA) have once more extended merchants‘ deadline for full SCA compliance, the previous date being March 2021 and the newly extended date being September 2021.
 
Please see latest guidance from FCA
https://www.fca.org.uk/firms/strong-customer-authentication
 
In summary:
+ Merchants (you, our customer) have to be compliant from September 2021
+ Because Asperato as a Third Party Processor we have to be compliant from 14th March 2021
+ UK Customers will not see declines as a result of SCA prior to the 14th March 2021
 
As a result, all of our Customers will be able to use SCA ready connections to their preferred Payment Service Provider via our Salesforce package no later than the 14th March 2021.
 
You will be able to use the updated SCA ready connections without a package upgrade.

We have already added SCA support for following PSPs and shall be available from within the package
+ Stripe
+ Sagepay
+ Braintree (A Paypal company)

## General Notes for Establishing SCA Connection in Asperato Package
Below is general guidance to create and use a SCA enable connection for a PSP
+ For SCA support, you need to create a new connection from Asperato Setup Page.
+ For PSD2 supported PSPs you will find a new PSP in the list with SCA appended to it.
+ See image 
+ Some cards require authentication everytime a transaction is made. For such cards future payments will fail.

## Setting Up Stripe SCA Connection
To create a Stripe SCA connection in Asperato package, follow below steps
1. Go to Asperato Setup page
2. Click on "New PSP Connection". In the popup screen, select
+ Currency as "British Pound"
+ Mode as "ECOM"
+ PSP as "Stripe SCA"
+ Select, Use custom Gateway detail
+ Description - any of your choice
+ Secret API Key - Use same API key as you were using earlier for non Sca connection
+ Publishable Key - You can get it from the stripe dashboard (via "Developers" and "API keys" on left hand menu). Refer help page: https://dashboard.stripe.com/test/apikeys 
3. Upon save, if connection is established successfully, you will see a green tick besides the connection just created.
Refer [here](https://stripe.com/docs/testing) for Stripe PSD2 testing guidance.

## Setting Up Sagepay SCA Connection
Create a new PSP connection from Asperato Setup with “Sagepay SCA”
1. Go to Asperato Setup page
2. Click on "New PSP Connection". In the popup screen, select
+ Currency as "British Pound"
+ Mode as "ECOM"
+ PSP as “Sagepay SCA”
+ Description - Of your choice
+ Vendor name - Use same name as you have used for Sagepay (without SCA) connection.
3. Upon save, if connection is established successfully, you will see a green tick besides the connection just created.
Refer [here](https://www.opayo.co.uk/support/12/36/test-card-details-for-your-test-transactions) for Sagepay PSD2 testing guidance

## Setting Up Braintree SCA Connection
Create a new PSP connection from Asperato Setup with “Sagepay SCA”
1. Go to Asperato Setup page
2. Click on "New PSP Connection". In the popup screen, select
+ Currency as "British Pound"
+ Mode as "ECOM"
+ PSP as “Sagepay SCA”
+ Description - Of your choice
+ Merchant Id - same as used for non-sca connection
+ Public Key - same as used for non-sca connection
+ Private Key - same as used for non-sca connection
+ Click on "Save PSP Connection" button
3. Upon save, if connection is established successfully, you will see a green tick besides the connection just created.
Refer [here](https://developers.braintreepayments.com/guides/3d-secure/testing-go-live/php) for Braintree PSD2 testing guidance


