---
title: Verify cache node functionality
description: How to verify functionality of a Microsoft Connected Cache for Enterprise and Education cache node.
author: chrisjlin
ms.author: lichris
manager: naengler
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.date: 09/27/2024
appliesto: 
- ✅ Windows-hosted MCCE cache nodes
- ✅ Linux-hosted MCCE cache nodes
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>	
---

# Verify MCCE cache node functionality

This article describes how to verify that a Microsoft Connected Cache for Enterprise and Education (MCCE) cache node is functioning correctly.

This should be done after deploying MCCE caching software to a [Windows](mcc-enterprise-deploy-windows.md) or [Linux](mcc-enterprise-deploy-linux.md) host machine.

## Steps to verify functionality of MCCE cache node

1. To verify that the MCCE container on the host machine is running and reachable, run the following command from the host machine:

    ```powershell
    wget http://localhost/filestreamingservice/files/7bc846e0-af9c-49be-a03d-bb04428c9bb5/Microsoft.png?cacheHostOrigin=dl.delivery.mp.microsoft.com
    ```

    If successful, there should be an HTTP response with StatusCode 200.

1. To verify that the MCCE cache node can be reached by Windows clients in your network, visit the following address from a web browser on a Windows client device:

    `http://[HostMachine-IP-address]/filestreamingservice/files/7bc846e0-af9c-49be-a03d-bb04428c9bb5/Microsoft.png?cacheHostOrigin=dl.delivery.mp.microsoft.com`

    If successful, the Windows client device should begin to download a small image file from the MCCE cache node.

1. To check how much content an individual Windows client has pulled from a MCCE cache node, open the [Delivery Optimization activity monitor](https://learn.microsoft.com/en-us/microsoft-365-apps/updates/delivery-optimization#viewing-data-about-the-use-of-delivery-optimization) on the Windows client device.

    You should see a donut chart titled Download Statistics. If the Windows client has pulled content from the cache node, you'll see a segment of the donut labeled "From Microsoft cache server".

## Related content

- [Monitor cache node usage](mcc-enterprise-monitoring.md)
- [Troubleshoot cache node](mcc-enterprise-support-troubleshoot.md)