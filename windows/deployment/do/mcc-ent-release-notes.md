---
title: MCC Release Notes
description: Release Notes for Microsoft Connected Cache for Enterprise and Education (MCC).
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: conceptual
ms.author: lichris
author: chrisjlin
manager: naengler
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>	
ms.date: 09/27/2024
---

# Release Notes for Microsoft Connected Cache for Enterprise and Education (MCC)

This article contains details about the latest releases of MCC. Since MCC is a Preview service, some releases may contain breaking changes that will be highlighted as such.

## Release v0.1.0 (Public Preview launch)

- Released on **10/17/2024**
- Contains breaking changes
- Contains service changes
- Contains client changes
- Affects Linux, Windows host machines

### Feature updates

- **Metrics and charts in Azure portal**: You can now visualize "Outbound egress" and "Volume by Content type" charts for your cache node on Azure portal. You can also create custom monitoring charts for your cache nodes. You will find this capability under the Metrics tab on Azure portal.
- **Cache nodes for Windows or Linux host machines**: Cache nodes can now be created and deployed to Windows host machine or Linux host machines by simply choosing the OS when creating cache nodes.
- **Azure CLI support**: Cache nodes can now be created and managed via Azure CLI.
- **Proxy**: We added support for unauthenticated proxy and cloud proxy integration.
- **Updates**: Your cache nodes will now be updated automatically and we also added capability to set each cache node's Update Ring to govern cadence of MCC container updates.

### Fixes
- We fixed various bugs to achieve smoother install experience.


<br>

## Related content

- [Overview of MCC](mcc-ent-edu-overview.md)
