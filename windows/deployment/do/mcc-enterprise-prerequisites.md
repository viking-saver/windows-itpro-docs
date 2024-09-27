---
title: Requirements for MCC for Enterprise and Education
description: Overview of prerequisites and recommendations for using Microsoft Connected Cache for Enterprise and Education (MCCE).
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: conceptual
ms.author: lichris
author: chrisjlin
manager: naengler
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>
ms.date: 09/27/2024
---

# Microsoft Connected Cache for Enterprise and Education Requirements (Public Preview)

This article details the requirements and recommendations for using Microsoft Connected Cache for Enterprise and Education (MCCE).

## Licensing requirements

- **Valid Azure subscription**: To use the Microsoft Connected Cache for Enterprise and Education (MCCE) service, you will need a valid Azure subscription that can be used to provision the necessary [Azure resources](/azure/cloud-adoption-framework/govern/resource-consistency/resource-access-management).

    If you don't have an Azure subscription already, you can create an Azure [pay-as-you-go](https://azure.microsoft.com/offers/ms-azr-0003p/) account, which requires a credit card for verification purposes. For more information, see the [Azure Free Account FAQ](https://azure.microsoft.com/free/free-account-faq/).

    The resources used for the public preview and in the future when this product is ready for production will be free to you, like other caching solutions.

- **E3/E5 or A3/A5 license**: Your organization must have one of the following license subscriptions for each device that downloads content from a MCCE cache node.

    - [Windows Enterprise E3 or E5](https://learn.microsoft.com/en-us/windows/whats-new/windows-licensing#windows-11-enterprise), included in [Microsoft 365 F3, E3, or E5](https://www.microsoft.com/en-us/microsoft-365/enterprise/microsoft365-plans-and-pricing?msockid=32c407b43d5968050f2b13443c746916)
    - Windows Education A3 or A5, included in [Microsoft 365 A3 or A5](https://www.microsoft.com/en-us/education/products/microsoft-365?msockid=32c407b43d5968050f2b13443c746916#Education-plans)

## Cache node host machine requirements

   > [!NOTE]
   > If you'd like to install your cache node on VMWare, see the [Appendix](mcc-enterprise-appendix.md) for a few additional configurations.

### General requirements

- Any previous installations of MCC must be [uninstalled](mcc-enterprise-update-uninstall.md) prior to installing the latest version of MCC.
- [These listed endpoints](delivery-optimization-endpoints.md) must be reachable by the host machine.
- There must be no other services / applications utilizing port 80 on the host machine (e.g. ConfigManager, Distribution Point)
- There must be at least 4 GB of free memory on the host machine.

### Additional requirements for Windows host machines

- The Windows host machine must be using Windows 11 or Windows Server 2022 with the Latest Cumulative Update (LCU) applied.
    - Windows 11 must have [OS Build 22631.3296](https://support.microsoft.com/en-us/topic/march-12-2024-kb5035853-os-builds-22621-3296-and-22631-3296-a69ac07f-e893-4d16-bbe1-554b7d9dd39b) or later
    - Windows Server 2022 must have [OS Build 20348.2227](https://support.microsoft.com/en-us/topic/january-9-2024-kb5034129-os-build-20348-2227-6958a36f-efaf-4ef5-a576-c5931072a89a) or later
- The Windows host machine must support nested virtualization.
- The Windows host machine must have [WSL2 installed](https://learn.microsoft.com/en-us/windows/wsl/install#install-wsl-command).

### Additional requirements for Linux host machines

- The Linux host machine must be using one of the following Operating Systems:

    - Ubuntu 20.04
    - Red Hat Enterprise Linux 8.* or 9.*
        - If using RHEL, the default container engine (Podman) must be replaced with [Moby](https://github.com/moby/moby#readme)

### Networking recommendations for host machines

- Multiple network interface cards (NICs) on a single MCC instance aren't supported.
- 1 Gbps NIC is the minimum speed recommended but any NIC is supported.
- For best performance, NIC and BIOS should support SR-IOV.

### Host machine sizing recommendations

| Component  | Branch Office / Small Enterprise | Large Enterprise |
| -- | --- | --- |
| OS|  Windows Server 2022 <br> Windows 11 (Pro or Enterprise) | Same |
|NIC | 1 Gbps | 5 Gbps |
|Disk | SSD <br>1 drive <br>50 GB each  |SSD <br>1 drive <br>200 GB each  |
|Memory | 4 GB | 8 GB |
|Cores | 4 | 8  |
