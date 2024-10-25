---
title: Microsoft Connected Cache Release Notes
description: Release Notes for Microsoft Connected Cache for Enterprise and Education.
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

# Release Notes for Microsoft Connected Cache for Enterprise and Education

This article contains details about the latest releases of Connected Cache. Since Connected Cache is a Preview service, some releases may contain breaking changes that will be highlighted as such.

## Release v0.1.0 (Public Preview launch)

- Released on **10/17/2024**
- Contains breaking changes
- Contains service changes
- Contains client changes
- Affects Linux, Windows host machines

### Changenotes

- Added new "Outbound egress" and "Volume by Content type" monitoring charts to Azure portal user interface
- Added ability to create custom monitoring charts under the Metrics tab in the Azure portal user interface
- Added support for creating both Windows-hosted and Linux-hosted cache nodes under the same Connected Cache Azure resource
- Added Azure CLI support for programmatic creation and management of Connected Cache Azure resources and cache nodes
- Added support for unauthenticated proxy and cloud proxy integration
- Added ability to set each cache node's Update Ring to govern cadence of Connected Cache container updates

## Related content

- [Overview of Connected Cache](mcc-ent-edu-overview.md)
