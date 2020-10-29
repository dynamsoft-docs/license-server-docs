---
layout: default-layout
title: Sample Sub-Folder Index Page
keywords: sample, index page
description: Sample sub-folder index page
breadcrumbText: Sample Sub-folder
---

# Purchase a License

## How to purchase

The Licenses to use Dynamsoft Products can be purchased in a few ways

* Purchase on the Dynamsoft Store
  + [Purchase Dynamic Web TWAIN](https://www.dynamsoft.com/store/dynamic-web-twain/)
  + [Purchase Dynamsoft Barcode Reader](https://www.dynamsoft.com/store/dynamsoft-barcode-reader/)

> This option is the easiest, you get the license within minutes.

* Purchase via a Purchase Order

> This usually means sending a digital copy of the order to [Dynamsoft Sales Team](mailto:sales@dynamsoft.com). Since the order is processed manually, this option usually takes one business day.

* Purchase via a Reseller

> Dynamsoft has many resellers around the world, you can buy from one that is most convenient for you. Find the reseller list [here](https://www.dynamsoft.com/Partner/Resellers.aspx).

## Check the purchased items

Each purchased item is registered to a specific Dynamsoft account associated with your organization. You can check your purchases in the customer portal once you log in with your account.

If you already have a Dynamsoft account and you used the same email to make a purchase, you can login from https://www.dynamsoft.com/api-common/Login/Login.

If you don't have a Dynamsoft account or you used an unregistered email to make a purchase, a new Dynamsoft account will be automatically created with that email. In this case, you must first click [Forgot Password?](https://www.dynamsoft.com/api-common/Regist/ForgotPassword) to set a password before logging in.

> If you don't have an account, you can also register on this page https://www.dynamsoft.com/api-common/Regist/Regist before making a purchase.

Once logged in, go to License -> Generate License(s) and you can see all the orders there.

![CustomerPortal-License-GenerateLicense]({{site.assets}}imgs/CustomerPortal-License-GenerateLicense.png)

## Generate a License

As shown in the image above, there is a "Generate License" button for each License item. You can click this button to generate a license, or you can check multiple items and click the "Generate one License" button to generate one license for multiple items.

![CustomerPortal-License-GenerateLicense2]({{site.assets}}imgs/CustomerPortal-License-GenerateLicense2.png)

After that, you are navigated to the License Detail page where you can "Activate" and "Download License File".

![CustomerPortal-License-GenerateLicense3]({{site.assets}}imgs/CustomerPortal-License-GenerateLicense3.png)

At this moment, the license has been generated but not activated. You can now choose one of the two activation options

* Activate the License and let Dynamsoft track its usage.
* Set up your own local License Tracking Server, activate the license and use your server to track its usage.

Both options use the same software we call License Tracking Server (LTS) to track the license usage. The differences are shown in the following table

| Question | Dynamsoft-hosting| Self-hosting |
|:-:|:-:|:-:|
| Need to designate a server to host LTS| No | Yes |
| Need to Install and manage LTS | No | Yes |
| Must maintain connection to Dynamsoft Server | Yes | No |
| Must send usage data to Dynamsoft Server | Yes | No |

Generally, you choose to host your own LTS if

* Your client devices may not be able to connect to the internet
* You don't want to share your usage data with Dynamsoft
* You believe your own server would work faster

If you decide to host your own LTS, please read more on [Self-hosting License Tracking]({{site.selfhosting}}index.html).

Otherwise, read more on [Dynamsoft-hosting License Tracking]({{site.dshosting}}index.html).
