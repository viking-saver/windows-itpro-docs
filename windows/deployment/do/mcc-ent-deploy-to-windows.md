---
title: Deploy MCC cache software to a Windows host machine
description: Details on how to deploy Microsoft Connected Cache for Enterprise and Education (MCC) cache software to a Windows host machine.
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

# Deploy Microsoft Connected Cache caching software to a Windows host machine

This article describes how to deploy Microsoft Connected Cache for Enterprise and Education (MCC) caching software to a Windows host machine.

Deploying MCC to a Windows host machine requires designating a [Group Managed Service Account (gMSA)](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts) or a [Local User Account](https://support.microsoft.com/windows/create-a-local-user-or-administrator-account-in-windows-20de74e0-ac7f-3502-a866-32915af2a34d) as the MCC runtime account. This prevents tampering with the MCC container and the cached content on the host machine.

Before deploying MCC to a Windows host machine, ensure that the host machine meets all [requirements](mcc-ent-prerequisites.md), and that you have [created and configured your MCC Azure resource](mcc-ent-create-resource-and-cache.md).

## Steps to deploy MCC cache node to Windows

# [Azure portal](#tab/portal)

1. Within the Azure portal, navigate to the "Provisioning" tab of your cache node and copy the provisioning command.
1. Download the provisioning package using the button at the top of the Cache Node Configuration page and extract the package onto the host machine.
1. Open a PowerShell window *as administrator* on the host machine, then change directory to the extracted provisioning package.
1. Set the Execution Policy to "Unrestricted" to allow the provisioning scripts to run.
1. Create a `$User` environment variable containing the username of the account you intend to designate as the MCC runtime account. For gMSAs, the value should be formatted as `"Domain\Username$"`. For Local User accounts, `$User` should be formatted as `"LocalMachineName\Username"`.

   If you're using a Local User account as the MCC runtime account, you'll also need to create a [PSCredential Object](/dotnet/api/system.management.automation.pscredential) named `$myLocalAccountCredential`.

1. Run the provisioning command on the host machine.

# [Azure CLI](#tab/cli)

To deploy a cache node programmatically, you'll need to use Azure CLI to get the cache node's provisioning details and then run the provisioning command on the host machine.

1. To get the cache node's provisioning details, use `az mcc ent node get-provisioning-details`.

   ```azurecli-interactive
   az mcc ent node get-provisioning-details --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg
   ```

1. Save the resulting output. These values will be passed as parameters within the provisioning command.
1. Download and extract the [MCC provisioning package for Windows](https://aka.ms/MCC-Ent-InstallScript-WSL) to your host machine.
1. Open a PowerShell window *as administrator* on the host machine, then change directory to the extracted provisioning package.
1. Set the Execution Policy to "Unrestricted" to allow the provisioning scripts to run.
1. Create a `$User` environment variable containing the username of the account you intend to designate as the MCC runtime account. For gMSAs, the value should be formatted as `"Domain\Username$"`. For Local User accounts, `$User` should be formatted as `"LocalMachineName\Username"`.

   If you're using a Local User account as the MCC runtime account, you'll also need to create a [PSCredential Object](/dotnet/api/system.management.automation.pscredential) named `$myLocalAccountCredential`.

1. Replace the values in the following provisioning command before running it on the host machine. Note that `-mccLocalAccountCredential $myLocalAccountCredential` is only needed if you are using a Local User account as the MCC runtime account.

   ```powershell-interactive
   ./provisionmcconwsl.ps1 -installationFolder c:\mccwsl01 -customerid [enter mccResourceId here] -cachenodeid [enter cacheNodeId here] -customerkey [enter customerKey here] -registrationkey [enter registration key] -cacheDrives "/var/mcc,enter drive size"  -shouldUseProxy [enter true if present, enter false if not] -proxyurl "http://[enter proxy host name]:[enter port]"  -mccRunTimeAccount $User -mccLocalAccountCredential $myLocalAccountCredential
   ```

## Next step

> [!div class="nextstepaction"]
> [Verify cache node functionality](mcc-ent-verify-cache-node.md)

## Related content

- [Deploy to a Linux host machine](mcc-ent-deploy-to-linux.md)
- [Uninstall MCC](mcc-ent-uninstall-cache-node.md)
