---
layout: default-layout
title: Dynamsoft License Server - Stable Releases
keywords: DLS Stable Release
noTitleIndex: false
description: This page is about the releases of DLS
breadcrumbText: Stable Releases
needAutoGenerateSidebar: true
---

# Stable Releases

## `2.2`

### New Features

* Added a new license option called "Per Active Device". [Requirements]({{site.schedule}}requirements/per-active-device.html)
* Added a new hidden property `handShakeCodeId` to a Handshake Code which is generated the same time as the Code and is readonly.
* Added a property `defaultHandShakeCode()` to each organization specified by its Dynamsoft ID. This property specifies which Handshake Code is the default one. There is always one and only one default Code for each organization.
* Added a method `setDefaultHandShakeCode()` which takes two parameters: the first specifies an organization with its Dynamsoft ID and the second specifies a Handshake Code with either its name or its `handShakeCodeId`.
  + If an organization is new, the first Handshake Code generated for one of its license items is set as the default.
* Added version number to all consumption chain files (.ccf).
* Added the "revoke" feature so that DLS accepts a revoked license item as long as the original item is present and then set both items invalid.

### Improvements

* Improved the communication between clients and DLS so that DLS always knows what license item is being used by a particular client. [>>Requirements]({{site.schedule}}requirements/add-item-id-in-request-n-response.html)
  + Based on this change, now DLS supports configuring the same Handshake Code with multiple license items of the types "Concurrent Device", "Concurrent Instance" or "Per Active Device".

* Improved the overflow grace-stage feature for the license options "Concurrent device", "Per Active Device" and "Concurrent Instance" so that accumulated exceptions are cleared every 365 days and the total allowed number of exceptions doesn't drop if the same license item continues to be valid.

* Improved the API `addLicense()` so that it not only specifies a new License File but also tells DLS how to process this License File. For example
  + Generate a new Handshake Code for the License File.
    - In this case, specify whether to make this new Code "Default".
  + Configure the License File to an existing Handshake Code.
  + Add the new License File, then do nothing about it.

## `2.1`

### New Features

* Added the "grace stage" feature which allows users to use more quotas than allowed by each license item.
* Added a new license option called "Concurrent Instance". [Requirements]({{site.schedule}}requirements/concurrent-instance.html)

## `2.0`

## `1.5`

## `1.0`
