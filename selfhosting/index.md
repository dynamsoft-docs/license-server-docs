---
layout: default-layout
title: Self-hosted License Tracking
keywords: self-hosted, activation, import
description: This page is about how to use self-hosted license tracking.
breadcrumbText: Self-hosted DLS
needAutoGenerateSidebar: true
noTitleIndex: true
---

# Self-hosted DLS

If your production environment does not allow internet connection, an alternative option is to host the license server program on your internal server machine so all your devices or end users can connect and get licensed via intranet connection.

* [Set Up DLS](#set-up-dls)
* [Activate the License](#activate-the-license)
* [Import the License](#import-the-license)
* [Manage License Keys](#manage-license-keys)
* [Upgrade DLS](#upgrade-dls)

## Set Up DLS

The first step in using your own DLS is to install it. Please read one of the following guides

* [Set up DLS on Windows]({{site.selfhosted}}dlsonwindows.html)
* [Set up DLS on Linux]({{site.selfhosted}}dlsonlinux.html)

After the installation, you can proceed to the next step.

## Activate the License

In the [customer portal](https://www.dynamsoft.com/customer/license/fullLicense), activate a license you want to use in your own DLS and select "Connect to My Self-Hosted License Server".

![Choose-Activation-Option-2]({{site.assets}}imgs/activate-004.png)

You'll be asked to input the `UUID` of your DLS, the UUID is found on the home page of your DLS.

![DLS-HomePage-001]({{site.assets}}imgs/dls-homepage.png)

Once done, an activated License File will be generated and downloaded automatically, the next step is to [import the license](#import-the-license).

> Read more on [what is License File]({{site.about}}terms.html#license-file)

## Import the License

This step imports the License File into DLS so that you can configure and use the purchased license(s).

* Click "Items" to go to the **License Items** page
* Click "Select File" to open the License File you just downloaded

![License Items - import]({{site.assets}}imgs/licenseitems-002.png)

After that, you will be asked to either create a new project for this license or insert it to an existing project

![License Items - import]({{site.assets}}imgs/licenseitems-003.png)

If you clicked "New Project", you will be asked to provide a name for this project

![License Items - import]({{site.assets}}imgs/licenseitems-004.png)

Once imported, you can find the project listed on the **Projects** page where you can get the license key string to use in your applications.

![License Items - import]({{site.assets}}imgs/licenseitems-005.png)

## Manage License Keys

To manage a license key is to configure the project bound to this license key. For more details, please see [Project Configurartion]({{site.common}}project.html).

## Track the License

For Self-Hosted DLS, all usage data is submitted to [DLS]({{site.about}}terms.html#dynamsoft-license-server) hosted by yourself. You can

* [View the license usage statistics]({{site.common}}statistics.html)
* [Get notified about license status]({{site.common}}usagealerts.html)

## Upgrade DLS

Because a license gets bound to a copy of DLS as soon as it's activated, you must be cautious when upgrading DLS. Dynamsoft recommends that DLS should not be upgraded unless absolutely necessary. An important thing to keep in mind is that the license itself usually needs to be regenerated during a DLS upgrade, so always contact [Dynamsoft Support Team](mailto:support@dynamsoft.com) before you plan a DLS upgrade.
