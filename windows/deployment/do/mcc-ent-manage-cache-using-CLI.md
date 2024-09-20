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
1. **Install Azure CLI**: How to install the Azure CLI | Microsoft Learn
2. **Install MCC extension**: Install the MCC extension.





### 1. Create a Resource group
The first step is to create a resource group if you don't already have one.
An Azure resource group is a logical container into which Azure resources are deployed and managed.

To create a resource group, use az group create.
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

[!IMPORTANT]
In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully started creating MCC resource.
The next step is to create a cache node under this resource.


### 3. Create a cache node
To create a cache node, use az mcc ent node create

```azurecli-interactive
az mcc ent node create --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg --host-os linux
```

<br>

[!IMPORTANT]
In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully started creating cache node.


### 4. Confirm cache node creation
Before you can start configuring your cache node, you need to confirm that cache node creation has been successful. 
To confirm cache node creation, use az mcc ent node show

<br>

```azurecli-interactive
az mcc ent node show --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg  
```

[!IMPORTANT]
In the output look for cacheNodeState. If **cacheNodeState = Not Configured**, you can continue with cache node configuration.
If **cacheNodeState = Registration in Progress**, then the cache node is still in process of being created. Please wait for a minute or two more and run the command again.


Once the cache node has been created successfully, you can now configure the cache node.


### 5. Configure cache node
To configure your cache node, use az mcc ent node update

Ex: configure linux cache node, proxy, slow

```azurecli-interactive
az mcc ent node update --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg
--cache-drive "[{physical-path:/cachenode/drive1,size-in-gb:50},{physical-path:/cachenode/drive2,size-in-gb:51}]" --proxy enabled --proxy-host "abc.xyz" --proxy-port 80  --auto-update-day 2 --auto-update-time 15:33 --auto-update-week 3 --auto-update-ring slow
```

[!IMPORTANT]
If your cache node is a Windows cache node, the physical path of the cache drive must be **“C:\mccwsl01”**.
In the output, look for operationStatus. **operationStatus = Succeeded** indicates that our services have successfully updated the cache node.

[!IMPORTANT]
Please save values for physicalPath, sizeInGb, proxyPort, proxyHostName as these values will be needed to create the provisioning script.

[!NOTE]
Proxy info changes, required to provision cache node.


### 6. Get provisioning details for the cache node
Now that you have configured the cache node, the next step is to provision the cache node on the server. To provision the cache node, you will need to create a provisioning script with relevant information.
To get the relevant information for provisioning script, use az mcc ent node get-provisioning-details

```azurecli-interactive
az mcc ent node get-provisioning-details --cache-node-name mycachenode --mcc-resource-name mymccresource --resource-group myrg
```

In the output, please save the values for cacheNodeId, customerKey, mccResourceId, registrationKey. These values are needed to create the provisioning script.

### 7. Provisioning cache node
Now
#### Provisioning cache node on Linux host os:
Before you provision your cache node on Linux machine, please make sure you have completed the requisites listed here: Host machine requirements

Use the link below to download and unzip the provisioning package on the server and run the below script to provision your cache node. 

https://aka.ms/MCC-Ent-InstallScript-Linux

[!IMPORTANT]
Note: before you execute the script,  please make sure you change access permissions by running 

```azurepowershell-interactive
sudo chmod +x provisionmcc.sh
```

[!NOTE]
Please replace the sample values in the script below with the values that you saved in the step 5 and 6.

[!IMPORTANT]
'shoulduseproxy' parameter is required, whether or not your network uses proxy to access internet.


Provisioning script:
```powershell-interactive
sudo ./provisionmcc.sh customerid="enter mccResourceId here" cachenodeid=" enter cacheNodeId here " customerkey=" enter customerKey here " registrationkey="enter registrationKey here" drivepathandsizeingb="enter physicalPath value,enter sizeInGb value here" shoulduseproxy="true" proxyurl=http://enter proxy hostname:enter port
```


#### Provisioning cache node on Windows host os:

Before you provision your cache node on Windows, please make sure you have completed the requisites listed here: Host machine requirements

Please download and unzip the provisioning package on the server and run the below script to provision your cache node.
Note: Please replace the sample values with the values that you saved in the above steps.

Important
'shoulduseproxy' parameter is required, whether or not your network uses proxy to access internet.


https://aka.ms/MCC-Ent-InstallScript-WSL

If you are using a **gmsa** account:

```powershell-interactive
./provisionmcconwsl.ps1 -installationFolder c:\mccwsl01 -customerid enter mccResourceId here -cachenodeid enter cacheNodeId here -customerkey enter customerKey here -registrationkey enter registration key -cacheDrives "/var/mcc,enter drive size"  -shouldUseProxy $true -proxyurl " http://enter proxy host name:enter port"  -mccRunTimeAccount $User
```
<br>

If you are using **local user account** or **domain user account**:

```powershell-interactive
./provisionmcconwsl.ps1 -installationFolder c:\mccwsl01 -customerid enter mccResourceId here -cachenodeid enter cacheNodeId here -customerkey enter customerKey here -registrationkey enter registration key -cacheDrives "/var/mcc,enter drive size"  -shouldUseProxy $true -proxyurl " http://enter proxy host name:enter port"  -mccRunTimeAccount $User -mccLocalAccountCredential $myLocalAccountCredential 
```


To verify cache node functionality, please see: Verify cache node functionality


Sample script:
Below is a pseudo code that shows how the above can be scripted for bulk creation and configuration of cache node.



## Next step

TODO: Add your next step link(s)

> [!div class="nextstepaction"]
> [Write concepts](article-concept.md)

<!-- OR -->

## Related content

TODO: Add your next step link(s)

- [Write concepts](article-concept.md)

<!--
Remove all the comments in this template before you sign-off or merge to the main branch.
-->

