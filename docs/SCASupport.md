---
id: scasupport
title: SCA Support
sidebar_label: SCA Support
---

The Financial Conduct Authority (FCA) have once more extended merchants‘ deadline for full SCA compliance, the previous date being September 2021 and the newly extended date being March 2022.
 
Please see latest guidance from FCA
https://www.fca.org.uk/firms/strong-customer-authentication
 
Click here to the supported payment service providers - https://asperato.github.io/userdocs/docs/supportedpsp
 
You will be able to use the SCA ready connections without a package upgrade. All you need to do is to create a new connection from Asperato Setup Page via Salesforce.

We have already added SCA support for following PSPs and shall be available from within the package
+ Adyen
+ Braintree (A Paypal company)
+ Checkout.com
+ Cybersource
+ Stripe
+ Sagepay
+ Worldpay

## General Notes for Establishing SCA Connection in Asperato Package
Below is a general guidance to create and use a SCA enable connection for a PSP
+ For SCA support, you need to create a new connection from Asperato Setup Page.
+ For PSD2 supported PSPs you will find a new PSP in the list with SCA appended to it. See below image
  ![Sca appended to SCA Supported PSPs](/userdocs/img/SCAConnections.png) 
+ Some cards require authentication everytime a transaction is made. For such cards future payments will fail.

## Setting Up Ayden SCA Connection
Create a new PSP connection from Asperato Setup with “Ayden SCA”
1. Go to Asperato Setup page
2. Click on "New PSP Connection". In the popup screen, select
   + Currency, i.e. GBP
   + Mode as "ECOM" or "MOTO"
   + PSP as “Adyen SCA”
   + Description - Of your choice
   + Merchant account
   + API Key - Generate API key as per the steps given [here](https://docs.adyen.com/development-resources/api-credentials#generate-api-key)
   + Client Key - Generate Client key as per the steps given [here](https://docs.adyen.com/development-resources/client-side-authentication/migrate-from-origin-key-to-client-key#switch-to-using-the-client-key)
   + URL Prefix - Enter as [A random string of hex-encoded bytes to make the hostname unpredictable]-[Company Name]. Refer Adyen documentation [here](https://docs.adyen.com/development-resources/live-endpoints) for more details.
3. Upon save, if the connection is established successfully, you will see a green tick besides the connection just created.
Refer <a href="https://docs.adyen.com/development-resources/test-cards/test-card-numbers">here </a> for Adyen PSD2 testing guidance.

## Setting Up Braintree SCA Connection
Create a new PSP connection from Asperato Setup with “Braintree SCA”
1. Go to Asperato Setup page
2. Click on "New PSP Connection". In the popup screen, select
   + Currency, i.e. GBP
   + Mode as "ECOM" or "MOTO"
   + PSP as “Braintree SCA”
   + Description - Of your choice
   + Merchant Id - same as used for non-sca connection
   + Public Key - same as used for non-sca connection
   + Private Key - same as used for non-sca connection
   + Click on "Save PSP Connection" button
3. Upon save, if the connection is established successfully, you will see a green tick besides the connection just created.
Refer [here](https://developers.braintreepayments.com/guides/3d-secure/testing-go-live/php) for Braintree PSD2 testing guidance.

## Setting Up Cybersource SCA Connection
Create a new PSP connection from Asperato Setup with “Braintree SCA”
1. Go to Asperato Setup page
2. Click on "New PSP Connection". In the popup screen, select
   + Currency, i.e. GBP
   + Mode as "ECOM" or "MOTO"
   + PSP as “Cybersource SCA”
   + Description - Of your choice
   + Merchant Id - same as used for non-sca connection
   + Security Key
   + Org Id
   + Click on "Save PSP Connection" button
3. Upon save, if the connection is established successfully, you will see a green tick besides the connection just created.

## Setting Up Stripe SCA Connection
To create a Stripe SCA connection in Asperato package, follow below steps
1. Go to Asperato Setup page
2. Click on "New PSP Connection". In the popup screen, select
   + Currency, i.e. GBP
   + Mode as "ECOM" or "MOTO"
   + PSP as "Stripe SCA"
   + Select, Use custom Gateway detail
   + Description - any of your choice
   + Secret API Key - You can get it from the stripe dashboard (via "Developers" and "API keys" on left hand menu). Refer help page: https://dashboard.stripe.com/test/apikeys
   + Publishable Key - You can get it from the stripe dashboard (via "Developers" and "API keys" on left hand menu). Refer help page: https://dashboard.stripe.com/test/apikeys 
3. Upon save, if connection is established successfully, you will see a green tick besides the connection just created.
Refer [here](https://stripe.com/docs/testing) for Stripe PSD2 testing guidance.

## Setting Up Sagepay SCA Connection
Create a new PSP connection from Asperato Setup with “Sagepay SCA”
1. Go to Asperato Setup page
2. Click on "New PSP Connection". In the popup screen, select
   + Currency, i.e. GBP
   + Mode as "ECOM" or "MOTO"
   + PSP as “Sagepay Beta Sca”
   + Description - Of your choice
   + Vendor name - Use same name as you have used for Sagepay (without SCA) connection.
3. Upon save, if connection is established successfully, you will see a green tick besides the connection just created.
Refer [here](https://www.opayo.co.uk/support/12/36/test-card-details-for-your-test-transactions) for Sagepay PSD2 testing guidance.

## Setting Up Worldpay SCA Connection
Create a new PSP connection from Asperato Setup with “Worldpay SCA”
1. Go to Asperato Setup page
2. Click on "New PSP Connection". In the popup screen, select
   + Currency, i.e. GBP
   + Mode as "ECOM" or "MOTO"
   + PSP as “Worldpay SCA”
   + Description - Of your choice
   + API Id (iss) - From Worldpay dashboard after changing to Test mode, go to Integration->3DS Flex
   + Merchant Code - You will get it from Worldpay dashboard under Account-> Profile
   + Password - Use the XML password which can be generated by following the steps in Worldpay documentation [here](https://developer.worldpay.com/docs/wpg/directintegration/quickstart#setup)
   + Org Unit ID - From Worldpay dashboard after changing to Test mode you will get it under Integration->3DS Flex
   + API key - From Worldpay dashboard after changing to Test mode you will get it under Integration->3DS Flex
3. Upon save, if connection is established successfully, you will see a green tick besides the connection just created. Refer <a href="https://developer.worldpay.com/docs/wpg/reference/testvalues#3d-secure-3ds-test-values">here</a> for Worldpay PSD2 testing guidance.
