---
layout: default-layout
title: Sample Folder Index Page
keywords: sample, index page
description: Sample folder index page
breadcrumbText: Sample Folder
---

# Terms

## License 2.0

## Alias

An Alias is basically a name for the license. You can set a meaningful Alias to a certain license so that you can easily identify the purpose of the license.

A default Alias is created automatically that follows the patterm "DM_{License Id}_Date{Activation Date}", a more meaningful Alias could be something like "BarcodeReader_License_For_Dynamsoft_ABC_Project".

A few things to know about the Alias

* It can only be changed when the license is new. Once the license is activated, it can no longer be changed.
* The Alias will show up in the [License File](#license-file) as a field.

## Handshake Code

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
