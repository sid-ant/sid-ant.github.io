---
layout: post
title:  "Zerodha Coin or PayTM Money?"
date:   2021-05-08 13:45:55 +0530
categories: tech
published: false
---

A google search on `Zerodha Coin vs PayTM Money` led to nothing conclusive. Besides the difference in how they hold Mutual Funds ( Demat vs Statement of Account respectively) there seems be no other substancial difference. However there is. 

## PayTM Money is less secure than Zeroda Coin. Let me explain. 

Your PayTM Money account is linked to your primary paytm account as in they share the username/password and the phone number. To login into your PayTM account, you need to enter your password and an OTP which is sent to your mobile phone. Hence, they claim to have a working 2FA. However, if you lose your phone, an attacker can put the sim in an another phone and reset your password. The thing is PayTM sends the password reset link as a SMS. Hence, in reality there is no 2FA. They might as well get rid of the password step since if you have access to the mobile phone, you can reset the password anyhow.

This is an easy problem for PayTM to fix i.e. they could send the passsword reset link only to the registered email, instead of sending it as an SMS too. I reached out to them on Twitter and they replied that I can just disable my account if my phone is lost. This is missing the point. The time taken to conclude the device has been lost and additional time spent on blocking the account, is enough for an attacker to do the damage.  

![PayTM Twitter Reply](/assets/img/paytm-money.jpg)

Zerodha on the other hand is completly independent of your mobile number. It offers true 2FA with a Password and Time Based OTP (Authenticator apps). However, Coin lacks behind severily in the UI and the feature set as compared to PayTM. 

## What Damage? 

The another question we need to address is what damage can be done if an attacker gets access to your PayTM Money account. As far as I understand, nothing substancial. The attacker can look at the total amount you've invested, when you've invested it ( in what intervals) and where you've invested it. As of 8 May 2021, an attacker (or even you) can't add a new bank account and redem mutual funds in it. 

Hence, <b> *Zerodha Coin is more secure* </b> and I recommend using it for any serious investments. 
