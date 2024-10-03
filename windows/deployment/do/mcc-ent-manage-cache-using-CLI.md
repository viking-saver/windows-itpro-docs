---
title: Manage MCCE cache nodes using CLI
description: Details on how to manage Microsoft Connected Cache for Enterprise (MCCE) cache nodes via Azure CLI commands.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
manager: aaroncz
ms.author: nidos
author: doshnid
ms.reviewer: mstewart
ms.collection: tier3
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 10</a>
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise</a>	
ms.date: 06/03/2024
---

# Manage cache nodes using CLI

<br>

This article outlines how to create, configure, and deploy Microsoft Connected Cache for Enterprise (MCC) cache nodes using Azure CLI.

 
## Prerequisites:
1. **Install Azure CLI**: [How to install the Azure CLI](/cli/azure/install-azure-cli)
1. **Install MCC extension**: [Install the MCC extension.](/cli/azure/azure-cli-extensions-overview#how-to-install-extensions)

<br>
<br>

### 1. Create a Resource group
The first step is to create a resource group if you don't already have one.
An Azure resource group is a logical container into which Azure resources are deployed and managed.

To create a resource group, use `az group create`. You can find more details on this CLI command [here](/cli/azure/group#az-group-create).
<br>

```azurecli-interactive
az group create --name myrg --location westus
```

Once the resource group is created, you'll need to create a Microsoft Connected Cache for Enterprise resource.


### 2. Create an Azure resource
An MCC Azure resource is a top-level Azure resource under which cache nodes can be created.

To create an MCC Azure resource, use `az mcc ent resource create`

```azurecli-interactive
az mcc ent resource create --mcc-resource-name mymccresource --resource-group myrg
```

<br>

>[!IMPORTANT]
>In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully started creating MCC resource.

<br>

The next step is to create a cache node under this resource.


### 3. Create a cache node
To create a cache node, use `az mcc ent node create`

```azurecli-interactive
az mcc ent node create --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg --host-os linux
```

<br>

>[!IMPORTANT]
>In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully started creating cache node.

<br>

### 4. Confirm cache node creation
Before you can start configuring your cache node, you need to confirm that the cache node was successfully created.

To confirm cache node creation, use `az mcc ent node show`

<br>

```azurecli-interactive
az mcc ent node show --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg  
```

>[!IMPORTANT]
>In the output look for cacheNodeState. If **cacheNodeState = Not Configured**, you can continue with cache node configuration.
>If **cacheNodeState = Registration in Progress**, then the cache node is still in process of being created. Please wait for a minute or two more and run the command again.

<br>

Once successful cache node creation is confirmed, you can proceed to configure the cache node.


### 5. Configure cache node
To configure your cache node, use `az mcc ent node update`

The below example configures a Linux cache node with proxy enabled:

```azurecli-interactive
az mcc ent node update --cache-node-name <mycachenode> --mcc-resource-name <mymccresource> --resource-group <myrg>
--cache-drive "[{physical-path:</physical/path>,size-in-gb:<size of cache drive>},{</physical/path>,size-in-gb:<size of cache drive>}...]"> --proxy <enabled> --proxy-host <"proxy host name"> --proxy-port <proxy port>  --auto-update-day <day of week> --auto-update-time <time of day> --auto-update-week <week of month> --auto-update-ring <update ring>
```

>[!Note]
>* For a cache node that is to be deployed on Windows host OS, the physical path of the cache drive <u>must</u> be **/var/mcc**.<br>
>* In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully updated the cache node. You will also see that cacheNodeState will show "Not Provisioned". <br>
>* Please save values for <u>physicalPath, sizeInGb, proxyPort, proxyHostName</u> as these values will be needed to construct the provisioning script.


<br>

### 6. Get provisioning details for the cache node
After successfully configuring the cache node, the next step is to deploy the cache node to a host machine. To deploy the cache node, you'll need to create a provisioning script with relevant information.

To get the relevant information for provisioning script, use `az mcc ent node get-provisioning-details`

```azurecli-interactive
az mcc ent node get-provisioning-details --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg
```

Save the resulting values for cacheNodeId, customerKey, mccResourceId, registrationKey. These GUIDs are needed to create the provisioning script.

<br>

### 7. Deploy cache node


#### Deploy cache node to Linux host machine
Before you deploy your cache node to a Linux host machine, make sure you have met the prerequisites listed here: [Host machine requirements](mcc-ent-prerequisites.md)

Use the following link to download and extract the Linux-compatible MCCE provisioning package onto the host machine.

[Download MCC provisioning package for Linux host machine](https://aka.ms/MCC-Ent-InstallScript-Linux)

<br>

To deploy the cache node to a **Linux** host machine, see [Deploy cache node to Linux](mcc-ent-deploy-to-linux.md)
<br>

#### Deploy cache node to Windows host machine

Before you deploy your cache node to a Windows host machine, make sure you have met the prerequisites listed here: [Host machine requirements](mcc-ent-prerequisites.md)

Use the following link to download and extract the Windows-compatible MCCE provisioning package onto the host machine.
[Download MCC provisioning package for Windows host machine](https://aka.ms/MCC-Ent-InstallScript-WSL)
<br>

To deploy the cache node to a **Windows** host machine, see [Deploy cache node to Windows](mcc-ent-deploy-to-windows.md)

<br>

## Next step

To verify cache node functionality, see [Verify cache node functionality](mcc-ent-verify-cache-node.md)


<br>
<br>

### Sample script:
Below is a pseudo code that shows how the above can be scripted for bulk creation and configuration of cache node.

