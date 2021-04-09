---
layout: default-layout
title: Dynamsoft Licensing FAQ
keywords: Barcode reader, licensing
description: This page lists the frequently asked questions about Dynamsoft's License Tracking Server.
breadcrumbText: Licensing FAQ
needAutoGenerateSidebar: true
hasCustomLdJson: true
customLdJsonScript: 
---
<script type="application/ld+json">
{
  "@context": "https://schema.org", 
  "@type": "FAQPage", 
  "mainEntity": [{

    "@type": "Question",
    "name": "Does license tracking disclose any private information?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "No, the license tracking process does not disclose any private information. For licensing purposes, Dynamsoft SDKs that use trackable licensing will keep track of the actual usage locally (for example, the symbology types and number of scans for Dynamsoft Barcode Reader), then the usage information is condensed into a report and sent to the License Tracking Server ( LTS ) every 3 minutes. Once submitted, the records are purged on the local machine. Note that the report is all about usage of certain features and nothing about the actual output of these operations."

    }

  }, {

    "@type": "Question",
    "name": "How secure is the License Tracking Server?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "The License Tracking Server ( LTS ) is the only software that Dynamsoft SDKs would be communicating with at runtime, so the security of LTS matters."

    }

  }, {

    "@type": "Question",
    "name": "Can a client device work offline?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Yes, once a client device gets authorized, it can be used offline for no more than 7 days. After that, it must connect to LTS again for another authorization. Otherwise, it will stop working.

During the offline period, all usage data is kept on the client side and will be sent to the LTS all at once the next time the device gets online."

    }

  }, {

    "@type": "Question",
    "name": "Can I use Dynamsoft SDKs in an environment with no internet connection?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Yes. There are two scenarios in this case.

All client devices can connect to a local network within the organization. In this case, you can simply host your own LTS for license tracking. Please see Self-hosting License Tracking.
Client devices never connect to any network. In this case, you may require a special license. Please contact Dynamsoft Support Team for details."

    }

  }, {

    "@type": "Question", 
    "name": "Can I unregister inactive devices?", 
    "acceptedAnswer": {
      "@type": "Answer", 
      "text": "As mentioned in Per Device license, Dynamsoft keeps a list of UUIDs which identify the active devices. By default, only if a device hasn’t been used for over 365 days will its UUID be removed from the list. This is done automatically."

    }

  }, {

    "@type": "Question",
    "name": "Can I extend the quota of my license to support more devices or process more documents?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Yes. If you are using Dynamsoft-Hosting LTS, you can either contact sales@dynamsoft.com to add quota or log in the customer portal and place an order for extra quota yourself. Rest assured that the Handshake Code remains unchanged during the process, so no code change is required to your application once the quota is added.

If you are hosting your own LTS, all you need to do is purchase another license, import it in the LTS and configure it to the Handshake Code you have been using."

    }

  }, {

    "@type": "Question", 
    "name": "Can I renew my license before its current expiration date?", 
    "acceptedAnswer": {
      "@type": "Answer", 
      "text": "Yes, you can log into the customer portal to renew your license by credit card or PayPal any time before it expires. Alternatively, you can contact sales@dynamsoft.com if you prefer other payment methods (wire transfer or check)."

    }

  }, {

    "@type": "Question", 
    "name": "Can I purchase a license valid for more than one year?", 
    "acceptedAnswer": {
      "@type": "Answer", 
      "text": "Yes. Please contact sales@dynamsoft.com with your request."

    }

  }, {

    "@type": "Question", 
    "name": "Will the unused quota be rolled over to the next period?", 
    "acceptedAnswer": {
      "@type": "Answer", 
      "text": "No."

    }

  }, {

    "@type": "Question", 
    "name": "What is counted as a single application?", 
    "acceptedAnswer": {
      "@type": "Answer", 
      "text": "Definition of a single application >"

    }

  }, {

    "@type": "Question", 
    "name": "Policies", 
    "acceptedAnswer": {
      "@type": "Answer", 
      "text": "Learn more about our policies ›"

    }

  }]
}
</script>

# Dynamsoft Licensing FAQ

## Does license tracking disclose any private information?

No, the license tracking process does not disclose any private information.

For licensing purposes, Dynamsoft SDKs that use trackable licensing will keep track of the actual usage locally (for example, the symbology types and number of scans for Dynamsoft Barcode Reader or the number of images acquired by Dynamic Web TWAIN), then the usage information is condensed into a report and sent to the License Tracking Server ( `LTS` ) every 3 minutes. Once submitted, the records are purged on the local machine. Note that the report is all about usage of certain features and nothing about the actual output of these operations.

> Read more about [the mechanism]({{site.common}}mechanism.html) behind license tracking.

In addition, to uniquely identify a device, the SDK generates an UUID that is cached locally and included in all communication with the `LTS` . This UUID is random and doesn't contain any information about the device itself. For more information, check out [how a UUID is generated]({{site.about}}terms.html#generate-a-uuid).

Apart from the license usage and the UUID, the `LTS` collects no more information which means it does not know anything about the user or device except that it is using Dynamsoft SDKs.

A few things to note

* The `LTS` can either be the official one provided by Dynamsoft or one that’s hosted by the customers on their own servers.
* Offline licenses that do not require any information to be sent anywhere are also supported. Contact [Dynamsoft Sales](mailto:sales@dynamsoft.com) for more information.

## How secure is the License Tracking Server?

The License Tracking Server ( `LTS` ) is the only software that Dynamsoft SDKs would be communicating with at runtime, so the security of `LTS` matters. The following are the security features of `LTS` :

* `LTS` is responsible for authorizing the SDK as well as tracking the usage. It is designed to send/receive static data only when requested. No script can be run remotely on `LTS` nor from `LTS` to the requesting clients.
* `LTS` supports HTTPS and it is highly recommended that it runs via HTTPS.
* `LTS` supports domain binding. With domain binding, authorization to use the SDK is only granted to requests sent from the specified domain(s).
* `LTS` also supports setting a session password to avoid abuse.
* The authorization sent back from `LTS` and the usage reports sent to `LTS` are both encrypted.

## How reliable is the Dynamsoft-Hosting License Tracking Server?

Customer devices rely on the License Tracking Server to get authorized for using Dynamsoft SDKs, therefore, its reliability is crucial. The following are the measures we have in place for maximum uptime:

* `LTS` is hosted on AWS.
* `LTS` database is backed up every 12 minutes.
* The two instances of "LTS" run in parallel with each other on different machines, and their databases are synchronized every 2 minutes. If one of them fails, the other will take over all incoming requests.
* Once a device is authorized, it can work offline for up to 7 days.
* Technicians are notified of any server exception within 30 seconds of its occurrence.

Also, Dynamsoft has been a online service provider for over 13 years and has an experienced team who have been maintaining products like SourceAnywhere Hosted, SCMAnywhere Hosted, TFS Hosted, etc.

## What happens if my license runs out?

Generally, each trackable license has a fixed quota. If the quota is used up, the license will no longer be valid and the software will stop running. Of course, this is unacceptable for production use, and Dynamsoft has the following measures to ensure that it does not happen accidentally.

* Dynamsoft allows excessive usage of the licenses in case the licensee fails to extend or expand the license in time. Please refer to [Tolerance Stage]({{site.about}}terms.html#tolerance-stage).

* Dynamsoft notifies the licensee multiple times about the status of the license. Please refer to [Usage Alerts]({{site.common}}usagealerts.html).

## Can a client device work offline?

Yes, once a client device gets authorized, it can be used offline for no more than 7 days. After that, it must connect to `LTS` again for another authorization. Otherwise, it will stop working.

During the offline period, all usage data is kept on the client side and will be sent to the `LTS` all at once the next time the device gets online.

Contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) if you would like your devices to work offline for a longer period of time.

## Can I use Dynamsoft SDKs in an environment with no internet connection?

Yes. There are two scenarios in this case

* All client devices can connect to a local network within the organization.

  In this case, you can simply host your own `LTS` for license tracking. Please see [Self-hosting License Tracking]({{site.selfhosting}}index.html).

* Client devices never connect to any network.

  In this case, you may require a special license. Please contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) for details.

## Can I unregister inactive devices?

As mentioned in [Per Device license]({{site.about}}licensetypes.html#per-device), Dynamsoft keeps a list of UUIDs which identify the active devices. By default, only if a device hasn't been used for over 365 days will its UUID be removed from the list. This is done automatically.

If you are in a business with a high turnover rate of your devices/users, you can choose a different license option, like [Concurrent Device license]({{site.about}}licensetypes.html#cucurrent-device) or [Per Active Device license]({{site.about}}licensetypes.html#per-active-device).

If you use a Per-Device license and would like to clear the registered devices so that you can use other devices. You can contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) and pay a certain amount for the service (which comes in the form of temporary quota expansion).

## Can I extend the quota of my license to support more devices or process more documents?

Yes. If you are using Dynamsoft-Hosting `LTS` , you can either contact [sales@dynamsoft.com](mailto:sales@dynamsoft.com) to add quota or log in the [customer portal](https://www.dynamsoft.com/customer/order/list) and place an order for extra quota yourself. Rest assured that the [Handshake Code]({{site.about}}terms.html#handshake-code) remains unchanged during the process, so no code change is required to your application once the quota is added.

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
