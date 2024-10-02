---
title: Manage MCC cache nodes using CLI
description: Details on how to manage Microsoft Connected Cache for Enterprise (MCC) cache nodes via Azure CLI commands.
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


### 2. Create an MCC Azure resource
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
>For a cache node that is to be deployed on Windows host OS, the physical path of the cache drive must be **/var/mcc**.
<br>

>[!NOTE]
>Proxy info changes, required to provision cache node.
<br>

>[!IMPORTANT]
>In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully updated the cache node.
<br>

>[!IMPORTANT]
>Please save values for physicalPath, sizeInGb, proxyPort, proxyHostName as these values will be needed to create the provisioning script.


<br>

### 6. Get provisioning details for the cache node
After successfully configuring the cache node, the next step is to deploy the cache node to a host machine. To deploy the cache node, you'll need to create a provisioning script with relevant information.

To get the relevant information for provisioning script, use `az mcc ent node get-provisioning-details`

```azurecli-interactive
az mcc ent node get-provisioning-details --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg
```

Save the resulting values for cacheNodeId, customerKey, mccResourceId, registrationKey. These GUIDs are needed to create the provisioning script.

### Example script:
Below is a pseudocode example of how to script bulk creation and configuration of an MCC Azure resource and five MCC cache nodes.

<!--# [Bash](#tab/bash)

:::code language="azurecli" source="~/azure_cli_scripts/azure-cli/create-azure-resources-at-scale/bash/create-azure-resources-at-scale.sh" id="step4":::

In your console output, are you missing the last row in your CSV file?  This can be caused by a missing line continuation character after the last line. Add a blank line at the end of your CSV file to fix the issue.

# [PowerShell](#tab/powershell)

:::code language="azurecli" source="~/azure_cli_scripts/azure-cli/create-azure-resources-at-scale/powershell/create-azure-resources-at-scale.ps1" id="step4":::

-->

# [PowerShell](#tab/powershell)

```powershell
#Define variables
$mccResourceName = "demo-01"
$cacheNodeName = "demo-node"
$cacheNodeOperatingSystem = "Windows"
$resourceGroup = "myRG"
$resourceLocation = "westus"
$cacheNodesToCreate = 5
$proxyHost = "yourProxyHost.com"
$proxyPort = "8080"

#Create MCC Azure resource
az mcc ent resource create --mcc-resource-name $mccResourceName --location $resourceLocation --resource-group $resourceGroup

#Create 5 cache nodes
for ($cacheNodeNumber = 1; $cacheNodeNumber -le $cacheNodesToCreate; $cacheNodeNumber++) {
    $iteratedCacheNodeName = $cacheNodeName + "-" + $cacheNodeNumber
    
    #Create cache node
    az mcc ent node create --cache-node-name $iteratedCacheNodeName --mcc-resource-name $mccResourceName --host-os $cacheNodeOperatingSystem --resource-group $resourceGroup

    #Configure cache node
    az mcc ent node update --cache-node-name $iteratedCacheNodeName --mcc-resource-name $mccResourceName --resource-group $resourceGroup --cache-drive  "[{physical-path:/var/mcc,size-in-gb:50}]" --proxy enabled --proxy-host $proxyHost --proxy-port $proxyPort
}
```

## Next step

> [!div class="nextstepaction"]
> [Deploy cache node to Linux host machine](mcc-ent-deploy-to-Linux.md)
> [Deploy cache node to Windows host machine](mcc-ent-deploy-to-Windows.md)
