---
title: Deploy MCCE cache software to a Windows host machine
description: Details on how to deploy Microsoft Connected Cache for Enterprise and Education (MCCE) cache software to a Windows host machine.
author: chrisjlin
ms.author: lichris
manager: naengler
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.date: 09/27/2024
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a>	
---

# Deploy MCCE cache node to a Windows host machine

This article describes how to deploy Microsoft Connected Cache for Enterprise and Education (MCCE) caching software to a Windows host machine.

Deploying MCCE to a Windows host machine requires designating a [Group Managed Service Account (gMSA)](https://learn.microsoft.com/en-us/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts) or a [Local User Account](https://support.microsoft.com/en-us/windows/create-a-local-user-or-administrator-account-in-windows-20de74e0-ac7f-3502-a866-32915af2a34d) as the MCCE runtime account. This prevents tampering with the MCC container and the cached content on the host machine.

Before deploying MCCE to a Windows host machine, ensure that the host machine meets all [requirements](mcc-enterprise-prerequisites.md), and that you have [created and configured your MCC Azure resource](https://aka.ms/mccent-create-resources).

## Steps to deploy MCCE cache node to Windows

1. Within the Azure portal, navigate to the "Provisioning" tab of your cache node and copy the provisioning command.
1. Download the provisioning package using the button at the top of the Cache Node Configuration page and extract the package onto the host machine.
1. Open a PowerShell windows *as administrator* on the host machine, then change directory to the extracted provisioning package.
1. Set the Execution Policy to "Unrestricted" to allow the provisioning scripts to run.
1. Create a `$User` environment variable containing the username of the account you intend to designate as the MCC runtime account. For gMSAs, the value should be formatted as `"Domain\Username$"`. For Local User accounts, `$User` should be formatted as `"LocalMachineName\Username"`.
    - If you're using a Local User account as the MCCE runtime account, you'll also need to create a [PSCredential Object](https://learn.microsoft.com/en-us/dotnet/api/system.management.automation.pscredential?view=powershellsdk-7.4.0) named `$myLocalAccountCredential`.
1. Run the provisioning command on the host machine.

## Next step

> [!div class="nextstepaction"]
> [Verify cache node functionality](mcc-ent-verify-cache-node.md)

<!-- OR -->

## Related content

- [Deploy to a Linux host machine](mcc-ent-deploy-to-linux.md)
- [Uninstall MCCE](mcc-ent-uninstall-cache-node.md)