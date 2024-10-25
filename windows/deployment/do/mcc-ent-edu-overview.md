---
title: Microsoft Connected Cache for Enterprise and Education Overview
description: Overview, supported scenarios, and content types for Microsoft Connected Cache for Enterprise and Education.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: conceptual
ms.author: carmenf
author: cmknox
manager: aaroncz
ms.reviewer: mstewart
ms.collection: tier3
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 10</a>
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>	
ms.date: 05/09/2023
---

# Microsoft Connected Cache for Enterprise and Education Overview

> [!IMPORTANT]
> Microsoft Connected Cache is currently a preview feature. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Microsoft Connected Cache for Enterprise and Education (preview) is a software-only caching solution that delivers Microsoft content within Enterprise and Education networks. Connected Cache can be managed from an Azure portal or through Azure CLI and can be deployed to as many Windows devices, Linux devices, or VMs as needed. Managed Windows devices can be configured to download cloud content from a Connected Cache server by applying the client policy using management tools such as Intune.

Microsoft Connected Cache for Enterprise and Education (preview) is a standalone cache for customers moving towards modern management and away from Configuration Manager distribution points. For information about Microsoft Connected Cache in Configuration Manager (generally available, starting Configuration Manager version 2111), see [Microsoft Connected Cache in Configuration Manager](/configmgr/core/plan-design/hierarchy/microsoft-connected-cache).

Microsoft Connected Cache deployed directly to Windows relies on [Windows Subsystem for Linux](/windows/wsl/about) and either a [Group Managed Service Account](/windows-server/identity/ad-ds/manage/group-managed-service-accounts/group-managed-service-accounts/getting-started-with-group-managed-service-accounts), local user account, or domain user account are required to run WSL. WSL needs to run in a user context and any user, even if the currently logged-in user, could be used to run WSL and Microsoft Connected Cache.

## Supported scenarios and configurations

Microsoft Connected Cache for Enterprise and Education (preview) is intended to support the following content delivery scenarios:

- Pre-provisioning of devices using Windows Autopilot
- Co-managed clients that get monthly updates and Win32 apps from Microsoft Intune
- Cloud-only managed devices, such as Intune-enrolled devices without the Configuration Manager client, that get monthly updates and Win32 apps from Microsoft Intune

Microsoft Connected Cache is built for flexible deployments to support a number of enterprise configurations:

### Branch office

Customers may have globally dispersed offices that meet the following parameters:

- 10 – 50 Windows Clients
- No dedicated server hardware
- Internet bandwidth is great to limited (satellite internet)
- Possibly intermittent connectivity

To support the branch office scenario, customers can deploy a Connected Cache node to a Windows 11 client device.

### Large Enterprise

Customers may have office spaces, data centers, or Azure deployments that meet the following parameters:  

- 100's or 1,000's of Windows devices (client or server).
- Existing hardware – Decommissioned DP, file server, cloud print server
- Azure VMs and Azure Virtual Desktop
- Internet bandwidth is great to limited (T1)

To support the large enterprise scenario, customers can deploy a Connected Cache node to a server running Windows Server 2022 or Ubuntu 22.04.

See [Connected Cache node host machine requirements](mcc-ent-prerequisites.md) for recommended host machine specifications in each configuration.

| Enterprise configuration | Download speed range | Download speeds and approximate content volume delivered in 8 Hours |
|---|---|---|
|Branch Office|< 1 Gbps Peak| 500 Mbps => 1,800 GB </br></br> 250 Mbps => 900 GB </br></br> 100 Mbps => 360 GB </br></br> 50 Mbps => 180 GB|
|Small to Medium Enterprises/Autopilot Provisioning Center (50 - 500 devices in a single location) |1 - 5 Gbps| 5 Gbps => 18,000 GB </br></br>3 Gbps => 10,800 GB </br></br>1 Gbps => 3,600 GB|
|Medium to Large Enterprises/Autopilot Provisioning Center (500 - 5,000 devices in a single location) |5 - 101 Gbps Peak|   9 Gbps => 32,400 GB </br></br> 5 Gbps => 18,000 GB </br></br>3 Gbps => 10,800 GB|

## Supported content types

When clients download cloud-managed content, they use Delivery Optimization from the cache server installed on a Windows server or VM. Cloud-managed content includes the following types:

- Windows updates: Windows feature and quality updates
- Office Click-to-Run apps: Microsoft 365 Apps and updates
- Client apps: Intune, store apps, and updates
- Endpoint protection: Windows Defender definition updates

For the full list of content endpoints that Microsoft Connected Cache for Enterprise and Education supports, see [Microsoft Connected Cache content and services endpoints](delivery-optimization-endpoints.md).

## How it works

The following diagram displays an overview of how Connected Cache functions:

:::image type="content" source="./images/mcc_ent_publicpreview.png" alt-text="Diagram displaying the components of Connected Cache." lightbox="./images/mcc_ent_publicpreview.png":::

1. The Azure management portal for Microsoft Connected Cache or CLI are used to create cache nodes, configure deployments, including unauthenticated proxy settings.
1. Prepare Windows or Linux devices. If deploying to Windows devices, prepare accounts - gMSA, local user account, domain account. Deploy to Windows or Linux devices using scripts.
1. The Microsoft Connected Cache container is deployed to the device using Azure IoT Edge container management services and the cache server begins reporting status and metrics to Delivery Optimization services.
1. The DOCacheHost setting is configured using Intune or other MDM, DHCP custom option, or registry key.
1. Devices request content from the cache server, the cache server forwards the requests to the CDN and fills the cache, the cache server delivers the content requested to the devices, and uses Peer to Peer (depending on DO Download mode settings) for all DO content. 
1. Devices can fallback to CDN if cache server is unavailable for any reason or use Delivery Optimization delay fallback to http (CDN )settings to prefer the local cache server.
Customers can view data regarding Microsoft Connected Cache downloads on management portal and Windows Update for Business reports

## Next steps

>[!div class="nextstepaction"]
>[Create Connected Cache Azure resources](mcc-ent-create-resource-and-cache.md)