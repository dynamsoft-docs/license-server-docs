---
layout: default-layout
title: Terms involved in Dynamsoft License Server
keywords: Terms, Dynamsoft, License Server, 
description: This page has defintions and descriptions about Dynamsoft License Server Terms
breadcrumbText: Terms
needAutoGenerateSidebar: true
---

# Terms

## License 2.0

License 2.0 is a new generation licensing protocol designed and implemented by Dynamsoft for its products, including Dynamsoft Barcode Reader, Dynamic Web TWAIN, and more.

The following table shows the major differences between License 1.0 and 2.0:

| | License 1.0 | License 2.0 |
|:-:|:-:|:-:|
| Expirable | Yes | Yes |
| Network | Not required | Required |
| Usage trackable | No | Optional |
| Hardware binding | Optional | Optional |

## Dynamsoft License Server

Dynamsoft License Server (DLS) is proprietary software developed by Dynamsoft to manage and distribute License 2.0 based licenses.

Dynamsoft provides both Dynamsoft-hosting and self-hosting options of DLS. For more information, please see:

* [Use DLS Hosted by Dynamsoft]({{site.dshosting}}index.html)
* [Use Your own DLS]({{site.selfhosting}}index.html)

## Dynamsoft License Client

Dynamsoft License Client (DLC) is proprietary software developed by Dynamsoft to acquire License 2.0 based licenses from DLS and manage them in a local device. The software is embedded in all Dynamsoft products that support License 2.0.

## License File

When you acquire a license based on License 2.0, you get a License File that contains the license definition.

Each License File has a unique `LicenseId` and an [`Alias`](#alias). You can also find out information like the licensee (OrganizationID) and whether the license has been activated (LicenseStatus), etc. For example:

```text
LicenseId: 100028117
Alias: Used for Application A
LicenseTextVersion: 2.0
OrganizationID: 216998
LicenseStatus: Activated
LicenseItems:
...//one or multiple License Items
```

The license contained in the license file is only effective after it is activated. Read more on [activate the license]({{site.about}}activate.html).

If you are using Dynamsoft-Hosted DLS, the License File will be imported immediately after it is activated. On the other hand, when hosting your own DLS, you will need to do the license importing manually.

### Alias

Alias is another way to identify a license. You can set a meaningful Alias to a license so that you can easily identify the purpose of the license.

A default Alias is created automatically that follows the pattern `DM_{License Id}_Date{Activation Date}`.  A more meaningful Alias could be something like `BarcodeReader_License_For_Dynamsoft_Project_ABC`.

A few things to know about the Alias:

* It will show up in the [License File](#license-file) and there can only be one Alias per license file.
* It can only be changed when the "LicenseStatus" is "New".

### LicenseTextVersion

"LicenseTextVersion" tells DLS how to parse this license file.

### OrganizationID

OrganizationID uniquely designates an organization as the licensee.

### License Item

License Item is the basic concept of License 2.0. It defines the exact restrictions for using a Dynamsoft product and is the basic unit when purchasing a license. For example, a license item can be described as a "30-device package for using Dynamsoft Barcode Reader within Browsers".

## License Key

License Key is an alphanumeric string that tells DLC how to connect to DLS and get the required licenses.

Each License Key corresponds to a specific Handshake Code within an organization.

## Handshake Code

If you have multiple projects for which you want to assign different License Items, you can configure different Handshake Codes and use their corresponding License Keys in these projects.

A few things to note:

* One Handshake Code can contain permits of multiple License Items.
* Multiple Handshake Codes can share the permit of one single License Item.
* Quota consumption is counted against the License Item in use.
* Statistics are summarized both per Handshake Code and per License Item.

### Default Handshake Code

For each "new" organization added to DLS during the importing of a license file, a default Handshake Code is created. This Default Handshake Code is used when the license key used to connect to DLS specifies only the ID of the organization without specifying a Handshake Code.

### Validation Field

Validation Field is a security feature meant to protect the license configured in a Handshake Code. This field is a static characteristic of the application using the license. At present, the following three Validation Fields are supported:

* Website Domain

> Applicable to web applications. For example: *demo.dynamsoft.com*.

* Application ID

> Applicable to mobile applications. For example: *com.dynamsoft.DbrDemo*.

* Process Name

> Applicable to desktop/server/embedded applications. For example: *DynamsoftBarcodeReader.exe*.

### Session Password

Session Password is another way to protect the license configured in a Handshake Code. Unlike the Validation Field, which essentially validates application characteristics, the Session Password is a simpler, more flexible string used to authenticate the connection to the DLS itself.

> When you change the Session Password, the License Key will be updated to reflect the change.

## Trial License

### Public Trial License

A public trial license is a special license based on [license 2.0](#license-20) which is provided by Dynamsoft to all users for the purpose of testing Dynamsoft products for a temporary period of time. This license is implemented in most code samples for Dynamsoft products like the ones found in the [Dynamsoft Github repositories](https://github.com/orgs/Dynamsoft/repositories).

> As of March, 2022, the license is good for 24 hours.

Dynamsoft is gradually rolling out this license in the products. If you are having trouble getting this license to work, please feel free to [contact us](https://www.dynamsoft.com/company/contact/).

### Private Trial License

Private trial licenses are also based on [license 2.0](#license-20) and are meant for customers who have registered with Dynamsoft. These licenses are good for 30 days and can be extended for another 15 days when necessary.

After registering with Dynamsoft, you can log in and request the private trial license in the [customer portal](https://www.dynamsoft.com/customer/license/trialLicense).

