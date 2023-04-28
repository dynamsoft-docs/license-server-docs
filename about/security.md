---
layout: default-layout
title: Dynamsoft License Server Security FAQ
keywords: Barcode reader, licensing, security
description: This page lists the frequently asked questions about the security of Dynamsoft's Dynamsoft License Server.
breadcrumbText: Security FAQ
needAutoGenerateSidebar: true
hasCustomLdJson: true
noTitleIndex: true
customLdJsonScript: 
---

# Dynamsoft License Server Security FAQ

Table of Contents

* [Do online licenses collect any personal information](#do-online-licenses-disclose-any-personal-information)?
* [How secure is Dynamsoft License Server](#how-secure-is-dynamsoft-license-server)?
* [How reliable is the License Server hosted by Dynamsoft](#how-reliable-is-the-license-server-hosted-by-dynamsoft)?
* [How can I protect my online license](#how-can-i-protect-my-online-license)?

## Do online licenses collect any personal information?

No, online licenses do not collect any personal information.

* About the license usage

For licensing purposes, Dynamsoft SDKs that use online licenses will keep track of the actual usage locally (for example, the symbology types and number of scans for Dynamsoft Barcode Reader or the number of images acquired by Dynamic Web TWAIN), then the usage information is condensed into a report and sent to DLS every 3 minutes. Once submitted, the records are purged on the local machine. Note that the report is all about usage of certain features and nothing about the actual output of these operations. Images and extracted image data are never shared with Dynamsoft.

* About device identification

To uniquely identify a device, an UUID is generated per device that is cached locally and included in all communications with DLS. This UUID is irreversibly encrypted so there is no way to extract any personal information about the device.

DLS does not collect any  other information other than the two pieces of unidentifiable information above - license usage and device UUID. In other words, DLS does not know anything about the user or device except that it is using Dynamsoft SDKs.

A few things to note

* DLS can either be the official one provided by Dynamsoft or one that's hosted by yourself.
* If you don't want to share any information with Dynamsoft, you can contact [Dynamsoft Sales](mailto:sales@dynamsoft.com) to get an offline license.

## How secure is Dynamsoft License Server?

DLS is the only software that Dynamsoft SDKs would be communicating with at runtime, so the security of DLS matters. The following are the security features of DLS :

* DLS supports HTTPS and it is highly recommended that it runs via HTTPS.
* DLS supports application binding. With application binding, authorization to use the SDK is only granted to requests sent from the application that has its ID, name or domain bound.
* DLS supports setting a session password to avoid abuse.
* DLS is responsible for authorizing the SDKs as well as tracking the usage. It is designed to send/receive static data only when requested. No script can be run remotely on DLS nor from DLS to the requesting clients.
* Authorizations sent back by DLS and usage reports sent to DLS are specially encrypted and cannot be deciphered by any other party.

Last but not least, Dynamsoft is [ISO 27001](https://www.iso.org/isoiec-27001-information-security.html) certified and we take information & data security seriously.

## How reliable is the License Server hosted by Dynamsoft?

Customer devices rely on the License Server to get authorizations for using Dynamsoft SDKs, therefore, its reliability is crucial. The following are the measures we have in place for maximum uptime:

* DLS is hosted on AWS.
* DLS database is backed up every 60 minutes.
* There are always two instances of "DLS" running in parallel on different machines with their databases synchronized every 10 minutes. If one of them fails, the other will step up to take over all incoming requests.
* Once a device is authorized, it can work offline for a period of time (from 3 minutes to a maximum of 365 days or more, depending on the license type).
* Dynamsoft server administrators are notified within 30 seconds of any server exceptions.

Also, Dynamsoft has been an online service provider for over 13 years and has an experienced team who have been maintaining products like SourceAnywhere Hosted, SCMAnywhere Hosted, TFS Hosted, etc.

## How can I protect my online license?

To protect your online license, we recommend you take the following measures:

* Set a [session password]({{site.about}}terms.html#session-password). The license only works when the license key you use in your application contains the same session password you set for the license on DLS. If it's not too much trouble, you can update this password every time you update your app.

* Set a [validation field]({{site.about}}terms.html#validation-field). A validation field (also called binding information) is a static characteristic of the application (e.g. the domain of a web application, the process name of a desktop application, etc.). Dynamsoft SDKs will collect this information at runtime and include it in the requests sent to DLS. This way, you can limit unwanted license usage to your application.

