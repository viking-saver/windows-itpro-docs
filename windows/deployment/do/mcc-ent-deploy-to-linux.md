---
title: Deploy MCCE cache software to a Linux host machine
description: Details on how to deploy Microsoft Connected Cache for Enterprise and Education (MCCE) cache software to a Linux host machine.
author: chrisjlin
ms.author: lichris
manager: naengler
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.date: 09/27/2024
appliesto: 
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>	
---

# Deploy MCCE cache node to a Linux host machine

This article describes how to deploy Microsoft Connected Cache for Enterprise and Education (MCCE) caching software to a Linux host machine.

Before deploying MCCE to a Linux host machine, ensure that the host machine meets all [requirements](mcc-enterprise-prerequisites.md), and that you have [created and configured your MCC Azure resource](https://aka.ms/mccent-create-resources).

## Steps to deploy MCCE cache node to Linux

1. Within the Azure portal, navigate to the "Provisioning" tab of your cache node and copy the provisioning command.
1. Download the provisioning package using the button at the top of the Cache Node Configuration page and extract the package onto the host machine.
1. Open a command line window *as administrator* on the host machine, then change directory to the extracted provisioning package.
1. Set access permissions to allow the `provisionmcc.sh` script within the provisioning package directory to execute.
1. Run the provisioning command on the host machine.

## Next step

> [!div class="nextstepaction"]
> [Verify cache node functionality](mcc-ent-verify-cache-node.md)

## Related content

- [Deploy to a Windows host machine](mcc-ent-deploy-to-windows.md)
- [Uninstall MCCE](mcc-ent-uninstall-cache-node.md)