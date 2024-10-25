---
title: Microsoft Connected Cache for Enterprise and Education troubleshooting
description: Details on how to troubleshoot common issues for Microsoft Connected Cache for Enterprise.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
manager: naengler
ms.author: lichris
author: chrisjlin
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise</a>	
ms.date: 09/27/2024
---


# Troubleshoot Microsoft Connected Cache for Enterprise and Education

This article contains instructions on how to troubleshoot different issues you may encounter while using Connected Cache. These issues are categorized by the task in which they may be encountered.

## Steps to obtain an Azure subscription ID

<!--Using include file, get-azure-subscription.md, do/mcc-isp.md for shared content-->
[!INCLUDE [Get Azure subscription](includes/get-azure-subscription.md)]

## Troubleshooting Azure resource creation

[Connected Cache Azure resource creation](mcc-ent-create-resource-and-cache.md) can be initiated using either the Azure portal user interface or the Azure CLI command set.

If you're encountering an error during resource creation, check that you have the necessary RPaaS permissions and have filled out all required fields during the resource creation process.

## Troubleshooting cache node configuration

[Configuration of your Connected Cache node](mcc-ent-create-resource-and-cache.md) can be done using either the Azure portal user interface or the Azure CLI command set.

If you're encountering a validation error, check that you have filled out all required configuration fields.

If your configuration doesn't appear to be taking effect, check that you have clicked the "Save" button at the top of the configuration page in the Azure portal user interface.

## Troubleshooting cache nodes created during early preview

Cache nodes created and deployed during the [Microsoft Connected Cache for Enterprise and Education early preview](mcc-ent-private-preview.md) should continue to function but can no longer be managed or monitored remotely via the Connected Cache Azure service.

As such, we strongly recommend you [recreate your existing resources in Azure](mcc-ent-create-resource-and-cache.md) and then [redeploy the Connected Cache software to your host machines](mcc-ent-deploy-to-windows.md) using the latest OS-specific installer.

## Troubleshooting cache node deployment to Windows host machine

[Deploying a Connected Cache node to a Windows host machine](mcc-ent-deploy-to-windows.md) involves running a series of PowerShell scripts contained within the Windows provisioning package. These scripts will attempt to write log files to the installation directory specified in the provisioning command (`C:\mccwsl01\InstallLogs` by default).

There are three types of installation log files:

1. **WSL_Mcc_Install_Transcript**: This log file records the lines printed to the PowerShell window when running the installation script
1. **WSL_Mcc_Install_FromRegisteredTask_Status**: This log file records the high level status that is written during the registered tasks install
1. **WSL_Mcc_Install_FromRegisteredTask_Transcript**: This log file records the detailed status that is written during the registered tasks install

The Registered Task Transcript is usually the most useful for diagnosing the installation issue.

Once the Connected Cache software has been successfully deployed to the Windows host machine, you can check if the cache node is running properly by doing the following on the Windows host machine:

1. Launch a PowerShell process as the account specified as the runtime account during the Connected Cache install
1. Run `wsl -d Ubuntu-22.04-Mcc-Base` to access the Linux distribution that hosts the Connected Cache container
1. Run `sudo iotedge list` to show which containers are running within the IoT Edge runtime

If it shows the **edgeAgent** and **edgeHub** containers but doesn't show **MCC**, you can view the status of the IoT Edge security manager using `sudo iotedge system logs --f`.

You can also reboot the IoT Edge runtime using `sudo iotedge restart`.

## Troubleshooting cache node deployment to Linux host machine

[Deploying a Connected Cache node to a Linux host machine](mcc-ent-deploy-to-linux.md) involves running a series of Bash scripts contained within the Linux provisioning package.

Once the Connected Cache software has been successfully deployed to the Linux host machine, you can check if the cache node is running properly by doing the following on the Linux host machine:

1. Run `sudo iotedge list` to show which containers are running within the IoT Edge runtime

If it shows the **edgeAgent** and **edgeHub** containers but doesn't show **MCC**, you can view the status of the IoT Edge security manager using `sudo iotedge system logs --f`.

You can also reboot the IoT Edge runtime using `sudo iotedge restart`.

## Troubleshooting cache node monitoring

Connected Cache node status and performance can be [monitored using the Azure portal user interface](mcc-ent-monitoring.md).

If the [basic monitoring](mcc-ent-monitoring.md#basic-monitoring) visuals on the Overview tab are showing unexpected or erroneous values, refresh the browser window.

If the issue persists, check that you have configured the Timespan and Cache nodes as desired.

## Diagnose and Solve

You can also use the **Diagnose and solve problems** functionality provided by the Azure portal interface. This tab within the Microsoft Connected Cache Azure resource will walk you through a few prompts to help narrow down the solution to your issue.
