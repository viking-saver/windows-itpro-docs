---
title: MCC for Enterprise manage cache nodes using CLI
description: Microsoft Connected Cache for Enterprise. Learn about managing cache nodes using CLI
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

This article outlines how to create, configure and provision your Microsoft Connected Cache for Enterprise cache nodes using Azure CLI.

 
## Prerequisites:
1. **Install Azure CLI**: [How to install the Azure CLI](/cli/azure/install-azure-cli)
1. **Install MCC extension**: [Install the MCC extension.](/cli/azure/azure-cli-extensions-overview#how-to-install-extensions)

<br>
<br>

### 1. Create a Resource group
The first step is to create a resource group if you don't already have one.
An Azure resource group is a logical container into which Azure resources are deployed and managed.

To create a resource group, use [az group create](/cli/azure/group?view=azure-cli-latest#az-group-create).
<br>

```azurecli-interactive
az group create --name myrg --location westus
```

Once the resource group is created, you will need to create a Microsoft Connected Cache for Enterprise resource.


### 2. Create a MCC resource
A MCC resource is a resource under which cache nodes can be created.

To create a mcc resource, use az mcc ent resource create

```azurecli-interactive
az mcc ent resource create --mcc-resource-name mymccresource --resource-group myrg
```

<br>

>[!IMPORTANT]
>In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully started creating MCC resource.

<br>

The next step is to create a cache node under this resource.


### 3. Create a cache node
To create a cache node, use az mcc ent node create

```azurecli-interactive
az mcc ent node create --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg --host-os linux
```

<br>

>[!IMPORTANT]
>In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully started creating cache node.

<br>

### 4. Confirm cache node creation
Before you can start configuring your cache node, you need to confirm that cache node creation has been successful. 
To confirm cache node creation, use az mcc ent node show

<br>

```azurecli-interactive
az mcc ent node show --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg  
```

>[!IMPORTANT]
>In the output look for cacheNodeState. If **cacheNodeState = Not Configured**, you can continue with cache node configuration.
>If **cacheNodeState = Registration in Progress**, then the cache node is still in process of being created. Please wait for a minute or two more and run the command again.

<br>

Once the cache node has been created successfully, you can now configure the cache node.


### 5. Configure cache node
To configure your cache node, use az mcc ent node update

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
Now that you have configured the cache node, the next step is to provision the cache node on the server. To provision the cache node, you will need to create a provisioning script with relevant information.
To get the relevant information for provisioning script, use az mcc ent node get-provisioning-details

```azurecli-interactive
az mcc ent node get-provisioning-details --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg
```

In the output, please save the values for cacheNodeId, customerKey, mccResourceId, registrationKey. These values are needed to create the provisioning script.

### 7. Provisioning cache node
<br>

#### Provisioning cache node on Linux host OS:
Before you provision your cache node on Linux machine, please make sure you have completed the requisites listed here: Host machine requirements

Use the link below to download and unzip the provisioning package on the server and run the below script to provision your cache node. 

[Download MCC package for Linux host OS](https://aka.ms/MCC-Ent-InstallScript-Linux)

<br>

>[!IMPORTANT]
>Note: before you execute the script,  please make sure you change access permissions by running the command below <br>
>```azurepowershell-interactive
>sudo chmod +x provisionmcc.sh
>```

<br>

>[!NOTE]
>Please replace the sample values in the script below with the values that you saved in the step 5 and 6.

<br>

>[!IMPORTANT]
>'shoulduseproxy' parameter is required, whether or not your network uses proxy to access internet.

<br>

Provisioning script:<br>
`powershell-interactive
sudo ./provisionmcc.sh customerid="enter mccResourceId here" cachenodeid=" enter cacheNodeId here " customerkey=" enter customerKey here " registrationkey="enter registrationKey here" drivepathandsizeingb="enter physicalPath value,enter sizeInGb value here" shoulduseproxy="true" proxyurl=http://enter proxy hostname:enter port
`
<br>

#### Provisioning cache node on Windows host OS:

Before you provision your cache node on Windows, make sure you have completed the requisites listed here: [Host machine requirements](mcc-ent-prerequisites.md)

Please download and unzip the provisioning package on the server and run the below script to provision your cache node.
Note: Please replace the sample values with the values that you saved in the above steps.

>[!IMPORTANT]
>'shoulduseproxy' parameter is required, whether or not your network uses proxy to access internet.

<br>

[Download MCC package for Windows host OS](https://aka.ms/MCC-Ent-InstallScript-WSL)
<br>


If you are using a **gmsa** account:<br>

```powershell-interactive
./provisionmcconwsl.ps1 -installationFolder c:\mccwsl01 -customerid enter mccResourceId here -cachenodeid enter cacheNodeId here -customerkey enter customerKey here -registrationkey enter registration key -cacheDrives "/var/mcc,enter drive size"  -shouldUseProxy $true -proxyurl " http://enter proxy host name:enter port"  -mccRunTimeAccount $User
```

<br>

If you are using **local user account** or **domain user account**:<br>

```powershell-interactive
./provisionmcconwsl.ps1 -installationFolder c:\mccwsl01 -customerid enter mccResourceId here -cachenodeid enter cacheNodeId here -customerkey enter customerKey here -registrationkey enter registration key -cacheDrives "/var/mcc,enter drive size"  -shouldUseProxy $true -proxyurl " http://enter proxy host name:enter port"  -mccRunTimeAccount $User -mccLocalAccountCredential $myLocalAccountCredential 
```

<br>


## Next step

To verify cache node functionality, visit, [Verify cache node functionality](mcc-ent-verify-cache-node.md)


<br>
<br>

### Sample script:
Below is a pseudo code that shows how the above can be scripted for bulk creation and configuration of cache node.

