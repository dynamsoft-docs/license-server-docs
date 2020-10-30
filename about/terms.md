---
layout: default-layout
title: Sample Folder Index Page
keywords: sample, index page
description: Sample folder index page
breadcrumbText: Sample Folder
---

# Terms

## License 2.0

License 2.0 is the second-generation license protocol designed and implemented by Dynamsoft in products including Dynamsoft Barcode Reader and Dynamic Web TWAIN, etc.

The following table shows the differences between License 1.0 and 2.0

| | License 1.0 | License 2.0 |
|:-:|:-:|:-:|
| Expirable | Yes | Yes |
| Usage Trackable | No | Yes |
| Hardware binding | Optional | Required |
| Use Handshake Code | No | Yes |
| Use the license itself | Yes | No |

## Alias

An Alias is basically a name for the license. You can set a meaningful Alias to a certain license so that you can easily identify the purpose of the license.

A default Alias is created automatically that follows the patterm "DM_{License Id}_Date{Activation Date}", a more meaningful Alias could be something like "BarcodeReader_License_For_Dynamsoft_ABC_Project".

A few things to know about the Alias

* It can only be changed when the license is new. Once the license is activated, it can no longer be changed.
* The Alias will show up in the [License File](#license-file) as a field.

## License Item

A License Item contains a permit to use a product. The permit is not splittable.

## Handshake Code

The permits in License Items are not consumed directly by applications because 

* The same permit can be used by multiple applications
* The same application can use multiple permits from different License Items

Therefore, Dynamsoft invented the concept of "Handshake Code". An application making use of Dynamsoft SDKs gets authorized by Dynamsoft [License Tracking Service](#license-tracking-service) through a specific Handshake Code. Within License Tracking Service

* The same Handshake Code can be configured to contain permits from different License Items
* The permit from the same License Item can be share by multiple Handshake Codes

By doing this, the part of the application in charge of license verification doesn't need to change even if different permits are needed at a later date. 

A few things to note

* Quota consumption is counted against the License Item in use
* Statistics are summarized per Handshake Code

## Validation Field

A Handshake Code is just a string that shows up in your code. It is important to secure it so that other people who knows your Handshake Code can not use your license. The Validation Fields are designed for this purpose.

A Validation Field is an unalterable characteristic of your application, at present, the following three are supported

* Website Domain

> Usage: Dynamsoft Barcode Reader JavaScript Edition, Dynamic Web TWAIN

* Application ID

> Usage: Dynamsoft Barcode Reader Mobile Edition

* Process Name

> Usage: Dynamsoft Barcode Reader Server Edition & Embedded Edition

## Session Password

The Session Password is another way to protect your license. Unlike the Validation Field which is essentially validating a characteristic of your application, the Session Password is a simpler and more flexible string that you set in your application. To verify the password, all products use the same API, for example

* Dynamic Web TWAIN

``` javascript
Dynamsoft.WebTwainEnv.SessionPassword = "";
```

## License File

## License Tracking Service

## LTS UUID

The UUID here means a unique ID for the machine where LTS is deployed. This UUID will be bound with the license during license activation. After that, this license can only be imported and used on this particular machine. Therefore, make sure this machine is for production usage which is stable.

A UUID is bound to the hardware of the machine, choose one or multiple unique hardware identification labels to generate it. The available labels are

* ProcessorId
* Media Access Control Address
* Machine ID
* Motherboard Serial Number

The more labels you choose, the stricter the license binding. But if the hardware changes and any of the bound labels is different, the license binding will fail and the license will be unusable. Therefore, be cautious and think ahead on which labels to include (at least one is required).

Once a UUID is generated, you can go ahead and [activate the license](activate-the-license).
