---
layout: default-layout
title: Dynamsoft Licensing FAQ
keywords: Barcode reader, licensing
description: This page lists the frequently asked questions about Dynamsoft's License Tracking Server.
breadcrumbText: Licensing FAQ
needAutoGenerateSidebar: true
---

# Dynamsoft Licensing FAQ

## Does the Barcode Reader library disclose any information to the outside world?

No, once the barcode reading is complete, the library returns the results in a callback to be further processed by the remaining code. The image data is purged as soon as the reading is done. The results stay in the memory for a little while before it’s purged. Neither is sent anywhere.

For licensing purposes, the library by default keeps track of the symbology types and the number of scans (nothing about the actual barcode text) and will send the info to the License Tracking Server for license usage tracking purposes. Once submitted, the records are purged. In addition, the library generates an UUID which identifies the device for license tracking purposes. This UUID is included in all communications with the License Tracking Server. Check out more information on [Generate a UUID]({{site.about}}terms.html#generate-a-uuid).

A few things to note

* The License Tracking Server can either be the official one provided by Dynamsoft or one that’s hosted by the customers on their own servers.
* Offline licenses that do not require any information to be sent anywhere are also supported. Contact [Dynamsoft Sales](mailto:sales@dynamsoft.com) for more information.
* For debugging purposes, the actual barcode images that are read can be exported and saved. However, this is controlled in customer's code.

## How secure is the License Tracking Server?

The License Tracking Server ( `LTS` ) is the only software that Dynamsoft SDKs would be communicating with at runtime, so the security of `LTS` matters. The following are the security features of `LTS` :

* `LTS` is responsible for authorizing the SDK as well as tracking the usage. It is designed to send/receive static data only when requested. No script can be run remotely on `LTS` nor from `LTS` to the requesting clients.
* `LTS` supports HTTPS and it is highly recommended that it runs via HTTPS.
* `LTS` supports domain binding. With domain binding, authorization to use the SDK is only granted to requests sent from the specified domain(s).
* `LTS` also supports setting a session password to avoid abuse.
* The authorization sent back from `LTS` and the usage reports sent to `LTS` are both encrypted.

## Can a client device work offline?

Yes, once a client device gets authorized, it can be used offline for no more than 7 days. After that, it must connect to `LTS` again for another authorization. Otherwise, it will stop working.

During the offline period, all usage data is kept on the client side and will be sent to the `LTS` all at once the next time the device is online.

Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) if you would like your devices to work offline for a longer period of time.

## Can I use Dynamsoft SDKs in an environment with no internet connection?

Yes. There are two scenarios in this case

* All client devices can connect to a local network within the organization.

  In this case, you can simply host your own `LTS` for license tracking. Please see [Self-hosting License Tracking]({{site.selfhosting}}index.html).

* Client devices never connect to any network.

  In this case, you may require a special license. Please contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for details.

## Can I unregister inactive devices?

As mentioned in [per device license]({{site.about}}licensetypes.html#per-device), Dynamsoft keeps a list of UUIDs which identify the active devices. By default, if a device hasn't been used for over 365 days, its UUID will be removed from the list. However, if you are in a business with a high turnover rate of your devices/users, you might want inactive devices to be removed sooner. In this case, you can contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for a special license.

## Can I extend the quota of my license to support more devices or process more documents?

Yes. If you are using Dynamsoft-Hosting `LTS` , you can either contact [sales@dynamsoft.com](mailto:sales@dynamsoft.com) to add quota or log in the [customer portal](https://www.dynamsoft.com/customer/order/list) and place an order for extra quota yourself. Rest assured that the [Handshake Code]({{site.about}}terms.html#handshake-code) remains unchanged during the upgrade process, so no code change is required to your application once the quota is added.

If you are hosting your own `LTS` , all you need to do is purchase another license, import it in the `LTS` and configure it to the Handshake Code you have been using.

## Can I renew my license before its current expiration date?

Yes, you can log into the customer portal to renew your license by credit card or PayPal any time before it expires. Alternatively, you can contact [sales@dynamsoft.com](mailto:sales@dynamsoft.com) if you prefer other payment methods (wire transfer or check).

If you are using Dynamsoft-Hosting `LTS` , the new license will be automatically configured to the same [Handshake Code]({{site.about}}terms.html#handshake-code) that you have been using, so no code change is required to your application.

If you are hosting your own `LTS` , you need to download the new license file after the renewal, import it in the `LTS` and configure it to the Handshake Code you have been using.

## Can I purchase a license valid for more than one year?

Yes. Please contact [sales@dynamsoft.com](mailto:sales@dynamsoft.com) with your request.

## Will the unused quota be rolled over to the next period?

No.

## What is counted as a single application?

[Definition of a single application >](https://www.dynamsoft.com/Products/single-application.aspx)

## Policies

[Learn more about our policies ›](https://www.dynamsoft.com/Products/policies.aspx)
