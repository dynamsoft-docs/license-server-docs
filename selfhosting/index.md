---
layout: default-layout
title: Sample Folder Index Page
keywords: sample, index page
description: Sample folder index page
breadcrumbText: Sample Folder
---

# Self-Hosting License Tracking

This article is about Self-Hosting License Tracking, if you would rather let Dynamsoft track your license usage, check out [Dynamsoft-hosting License Tracking]({{site.dshosting}}index.html).

If you have not purchased any Dynamsoft SDK license that requires usage tracking, please check out [how to purchase a license]({{site.about}}license-purchase.html).

The following assumes you have purchased a license, logged into the customer portal, [generated a license]({{site.about}}license-purchase.html#generate-a-license) and landed on the "License Detail" page.

## Download the License File

To track the license usage yourself, you need to install the "License Tracking Server" on a designated server machine in your environment which serves two purposes:

* Authorize a client device to use the SDK
* Track the usage of the SDK 

The License File that you have generated with your purchased license items is required to set up the LTS. Press the "Download License File" button to get it downloaded. It'll be used in the step [Import License File](#import-license-file).

> Check out [what is a license file]({{site.about}}terms.html#license-file)

## Activate the license

Click "Activate" to go to the "Activate License" page. On this page, choose "On-Premise" and you will be asked to input a UUID. Check out [Generate UUID](#generate-uuid) on how to create a UUID for your LTS server.

Once the activation is completed, you get an activated license file.

## Install the License Tracking Server

### Download the latest LTS from 

* [Windows Server](somelink)
* [Linux Server](somelink)

### Unzip the downloaded file and start LTS

Run startup.bat to start the LTS

### Verify LTS is running

Open the LTS management link http://localhost:48080/index and see if it works. If it does, then installation has completed

## Use the LTS

### Set management password

The first time you open the LTS home page http://localhost:48080/index, you'll be asked to set a password for it.

![LTS-Usage-1]({{site.assets}}imgs/LTS-Usage-1.png)

This password is very important because you will need it to manage and check the usage of your licenses later on. Make sure you don't lose it!

The LTS management portal looks like this 

![LTS-Usage-2]({{site.assets}}imgs/LTS-Usage-2.png)

As it shows, there are 6 menu items on the left, we'll dive deep into what each one does.

### Generate UUID

The UUID here means a unique ID for the machine where LTS is deployed. This UUID will be bound with the license during license activation. After that, this license can only be imported and used on this particular machine. Therefore, make sure this machine is for production usage which is stable.

A UUID is bound to the hardware of the machine, choose one or multiple unique hardware identification labels to generate it. The available labels are

* ProcessorId
* Media Access Control Address
* Machine ID
* Motherboard Serial Number

The more labels you choose, the stricter the license binding. But if the hardware changes and any of the bound labels is different, the license binding will fail and the license will be unusable. Therefore, be cautious and think ahead on which labels to include (at least one is required).

Once a UUID is generated, you can go ahead and [activate the license](activate-the-license).

### Import License File

Here you import a license file that you downloaded from Dynamsoft Customer Portal.

When you import the file, you'll be asked to input your credentials of your Dynamsoft account. This is to ensure that the license file is indeed used by the licensee.

Once the import succeeds, you are redirected to "License Items"

--> Activation during the import or activate in the portal --> choose one!

### License Items

Here the activated items are listed, you can check details like quality, expiration date, etc.

### Configurations

Here you configure custom handshake codes. [What is a handshake code?]({{site.about}}terms.html#handshake-code)

#### Set consumption order

If you have multiple license items for one handshake code, you can set the consumption order which determines which license is consumed first. In most cases, you can just keep the default order which is already optimized.

#### Show Statistics

Click "Statistics" button to view the usage report for each handshake code.

Read more on ["Statistics Page"]({{site.about}}statistics-page.html)

#### Edit or add a handshake code

When you add or edit a handshake code, you are navigated to the "Handshake Details" page. Read more [here]({{site.selfhosting}}configure-handshake.html)

### Email Config

When the quota on the license is about to be used up, you may want to be notified. The License Tracking Server does it via email notifications. In Email config, you can set the email sender and who to notify.

Check out more on [Email Notification]({{site.selfhosting}}email-notification.html)
