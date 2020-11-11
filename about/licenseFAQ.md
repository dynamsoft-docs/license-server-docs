---
layout: default-layout
title: Dynamsoft Licensing FAQ
keywords: Barcode reader, licensing
description: This page lists the frequently asked questions about Dynamsoft's License Tracking Service.
breadcrumbText: Licensing FAQ
needAutoGenerateSidebar: true
---

# Dynamsoft Licensing FAQ

## Can a client device work offline?

Yes, once a client device gets authorized, it can be used offline for a maximum of 7 days after which it must connect to `LTS` again for further authorization. Otherwise, it will stop working.

During the offline period, all usage data is kept on the client side and will be sent to the `LTS` all at once the next time the device gets online.

## Can I use Dynamsoft SDKs in an environment with no internet connection?

Yes. There are two scenarios in this case

* All client devices can connect to a local network within the organization.

  In this case, you can simply host your own `LTS` for license tracking.

* Client devices are never connected to any network.

  In this case, you may require a special license. Please contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for details.

## Can I unregister an inactive device?

Yes, Dynamsoft has a mechanism to delete inactive devices. The following explains how it is done.

As mentioned in [per device license]({{site.about}}licensetypes.html#per-device), Dynamsoft keeps a list of UUIDs which identify the active devices. For a "Per Device" license, each active device will consume the license quota. With a default official "Per Device" license, the list of UUIDs is automatically refreshed once every 366 days. That means, if a device hasn't been used over 366 days, its UUID will be deleted on the `LTS` .

However, if you are in a business with a high turnover rate of your devices/users, you might want the refreshing to happen more frequently so that you can buy less "seats". In this case, you can contact your account manager to refresh your device allowance every three or six months or set a faster pace for automatical renewals. Please note that an additional fee is required for the special configuration.

## Can I extend the quota of my license to support more devices or process more documents?

Yes, you can either contact [sales@dynamsoft.com](mailto:sales@dynamsoft.com) to add quota or log in the [customer portal](https://www.dynamsoft.com/customer/order/list) and place an order for extra quota yourself.

Rest assured that the Handshake Code remains unchanged during the upgrade process, so no code change is required to your application.

> Read more on [What is a Handshake Code]({{site.about}}terms.html#handshake-code)

## Can I renew my license before its current expiration date?

Yes, you can log into the customer portal to renew your license by credit card or PayPal any time before it expires. Or, you can contact [sales@dynamsoft.com](mailto:sales@dynamsoft.com) if you prefer other payment methods (wire transfer or check).

Rest assured that the Handshake Code remains unchanged during the renewal process, so no code change is required to your application.

> Read more on [What is a Handshake Code]({{site.about}}terms.html#handshake-code)

## Can I purchase a license valid for more than one year?

Yes. Please contact [sales@dynamsoft.com](mailto:sales@dynamsoft.com) with your request.

## Will the unused quota be rolled over to the next period?

No.

## What is counted as a single application?

[Definition of a single application >](https://www.dynamsoft.com/Products/single-application.aspx)

## Policies

[Learn more about our policies ›](https://www.dynamsoft.com/Products/policies.aspx)
