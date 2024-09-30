---
title: Create and configure MCCE cache nodes
description: Details on how to create and configure Microsoft Connected Cache for Enterprise and Education (MCCE) cache nodes.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
manager: naengler
ms.author: nidos
author: doshnid
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise</a>	
ms.date: 06/03/2024
---

# Create MCCE Azure resource and cache nodes

This article outlines how to create and configure your Microsoft Connected Cache for Enterprise and Education (MCCE) cache nodes. The creation and configuration of your cache node takes place in Azure. The deployment of your cache node requires downloading and running an OS-specific provisioning package on your host machine.

## Prerequisites
1. **Azure Pay-As-You-Go subscription**: Microsoft Connected Cache is a free-of-charge service hosted in Azure. You'll need a pay-as-you-go Azure subscription in order to onboard to our service. To create a subscription, go to [pay-as-you-go subscription page](https://azure.microsoft.com/offers/ms-azr-0003p/).
2. **Hardware to host MCC**: The recommended configuration serves approximately 35,000 managed devices, downloading a 2-GB payload in 24-hour timeframe at a sustained rate of 6.5 Gbps.
For more information on sizing and OS requirements, see [the prerequisites for using MCCE](mcc-ent-prerequisites.md).

## Create MCCE Azure resource

# [Azure portal](#tab/portal)

1. In the [Azure portal](https://portal.azure.com), select **Create a Resource** and search for "Microsoft Connected Cache for Enterprise and Education".
<!--
    :::image type="content" source="images/mcc-isp-provision-cache-node-numbered.png" alt-text="Screenshot of the Azure portal depicting the cache node configuration page of a cache node. This screenshot shows all of the fields you can choose to configure the cache node." lightbox="./images/mcc-isp-provision-cache-node-numbered.png":::  
-->

1. Select the Microsoft Connected Cache for Enterprise resource. When prompted, choose the subscription, resource group, and location for the resource. Then enter a name for the resource and select Review + Create.
<!--
    :::image type="content" source="images/mcc-isp-provision-cache-node-numbered.png" alt-text="Screenshot of the Azure portal depicting the cache node configuration page of a cache node. This screenshot shows all of the fields you can choose to configure the cache node." lightbox="./images/mcc-isp-provision-cache-node-numbered.png":::  
-->
1. After a few moments, you'll see a "Validation successful" message, indicating you can move onto the next step and select Create.

1. The creation of the resource might take a few minutes. After a successful creation, you'll see a Deployment complete page as below. Select Go to resource to create cache nodes.


# [Azure CLI](#tab/cli)

### Prerequisites

* An Azure CLI environment:

  * Use the Bash environment in [Azure Cloud Shell](/azure/cloud-shell/get-started/classic).

  * Or, if you prefer to run CLI reference commands locally, [install the Azure CLI](/cli/azure/install-azure-cli)

    * Sign in to the Azure CLI by using the [az login](/cli/azure/reference-index#az-login) command.

    * Run [az version](/cli/azure/reference-index#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/cli/azure/reference-index#az-upgrade).

    * Install Azure CLI extension **mcc** by following the instructions [here](/cli/azure/azure-cli-extensions-overview#how-to-install-extensions).

    * Resource group under which an MCC resource can be created. Use the [az group create](/cli/azure/group#az-group-create) command to create a new Resource group if you don't already have one.

#### Create MCCE Azure resource
Replace the following placeholders with your own information:
* *\<resource-group>*: An existing resource group in your subscription.
* *\<mcc-resource-name>*: A name for your Microsoft Connected Cache for Enterprise resource.
* *\<location>*: The Azure region where your Microsoft Connected Cache will be located.

```azurecli-interactive
az mcc ent resource create --mcc-resource-name <mymccresource> --resource-group <myrg> --location <region>
```

---

## Create MCCE cache node

# [Azure portal](#tab/portal)

  1. Open Azure portal and navigate to the Microsoft Connected Cache for Enterprise resource that you created.
  1. Under Cache Node Management, select on Cache Nodes and then on + Create Cache Node.
  <!--
    :::image type="content" source="images/mcc-isp-provision-cache-node-numbered.png" alt-text="Screenshot of the Azure portal depicting the cache node configuration page of a cache node. This screenshot shows all of the fields you can choose to configure the cache node." lightbox="./images/mcc-isp-provision-cache-node-numbered.png":::  
    -->
  1. Provide a name for your cache node and select the host OS you plan to deploy the cache node on and select create. Note, cache node names have to be unique under the Microsoft Connected Cache resource.
  <!--
    :::image type="content" source="images/mcc-isp-provision-cache-node-numbered.png" alt-text="Screenshot of the Azure portal depicting the cache node configuration page of a cache node. This screenshot shows all of the fields you can choose to configure the cache node." lightbox="./images/mcc-isp-provision-cache-node-numbered.png":::  
    -->
  The creation of cache node might take a few minutes. Select Refresh to see your recently created cache node.
Once the status changes to **Not Configured**, you can now configure your cache node.


# [Azure CLI](#tab/cli)

Use the following command to create a new cache node if you don't already have one.

Replace the following placeholders with your own information:
* *\<resource-group>*: An existing resource group in your subscription.
* *\<mcc-resource-name>*: A name for your Microsoft Connected Cache for Enterprise resource.
* *\<cache-node-name>*: The Azure region where your Microsoft Connected Cache will be located.
* *\<host-os>*: The OS on which cache node will be provisioned.
  Accepted values: windows, linux

```azurecli-interactive
az mcc ent node create --cache-node-name <mycachenode> --mcc-resource-name <mymccresource> --resource-group <myrg> --host-os <linux>
```

<br>

>[!NOTE]
>To ensure cache node has been created successfully, please run the following command before continuing with cache node configuration.
>```azurecli-interactive
>az mcc ent node show --cache-node-name <mycachenode> --mcc-resource-name <mymccresource> --resource-group <myrg>  
>```
>In the output look for cacheNodeState. If cacheNodeState = Not Configured, you can continue with cache node configuration.
>If cacheNodeState = Registration in Progress, then the cache node is still in process of being created. Please wait for a minute or two more and run the command again.


<!-- `code blah blah`
-->



---

## Configure MCCE cache node

# [Azure portal](#tab/portal)
Enter required values to configure your cache node. To learn more about the definitions of each field, review the Configuration fields at the bottom of this article.
Don't forget to select save after adding configuration information.


# [Azure CLI](#tab/cli)

Use the following command to configure cache node for deployment to a **Linux** host machine.

Replace the following placeholders with your own information:
* *\<resource-group>*: An existing resource group in your subscription.
* *\<mcc-resource-name>*: A name for your Microsoft Connected Cache for Enterprise resource.
* *\<cache-node-name>*: The Azure region where your Microsoft Connected Cache will be located.
* *\<physical-path>*: The cache drive path. You can add upto nine cache drives.
* *\<size-in-gb>*: The size of cache drive. Must be at least 50 Gb.
* *\<proxy>*: If proxy needs to be enabled or not.<br>
  Accepted values: enabled, disabled
  If proxy is set to enabled, you must provide proxy host and proxy port information
* *\<proxy-host>*: The proxy host name or ip address
* *\<proxy-port>*: Proxy port
* *\<auto-update-ring>*: Update ring the cache node should have.<br>
  Accepted values: slow, fast.
  If update ring is set to slow, you must provide the day of week, time of day and week of month the cache node should be updated.
* *\<auto-update-day>*: The day of the week cache node should be updated. Week starts from Monday.<br>
  Accepted values: 1,2,3,4,5,6,7
* *\<auto-update-time>*: The time of day cache node should be updated in 24 hour format (hh:mm)
* *\<auto-update-week>*: The week of month cache node should be updated.<br>
  Accepted values: 1,2,3,4

```azurecli-interactive
az mcc ent node update --cache-node-name <mycachenode> --mcc-resource-name <mymccresource> --resource-group <myrg>
--cache-drive "[{physical-path:</physical/path>,size-in-gb:<size of cache drive>},{</physical/path>,size-in-gb:<size of cache drive>}...]"> --proxy <enabled> --proxy-host <"proxy host name"> --proxy-port <proxy port>  --auto-update-day <day of week> --auto-update-time <time of day> --auto-update-week <week of month> --auto-update-ring <update ring>
```

<br>
<br>

Use the following command to configure cache node for deployment to a **Windows** host machine.

Replace the following placeholders with your own information:
* *\<resource-group>*: An existing resource group in your subscription.
* *\<mcc-resource-name>*: A name for your Microsoft Connected Cache for Enterprise resource.
* *\<cache-node-name>*: The Azure region where your Microsoft Connected Cache will be located.
* *\<physical-path>*: The cache drive path.<br>
  Accepted value: /var/mcc
* *\<size-in-gb>*: The size of cache drive. Must be at least 50 Gb.
* *\<proxy>*: If proxy needs to be enabled or not.<br>
  Accepted values: enabled, disabled
  If proxy is set to enabled, you must provide proxy host and proxy port information
* *\<proxy-host>*: The proxy host name or ip address
* *\<proxy-port>*: Proxy port
* *\<auto-update-ring>*: Update ring the cache node should have.<br>
  Accepted values: slow, fast.
  If update ring is set to slow, you must provide the day of week, time of day and week of month the cache node should be updated.
* *\<auto-update-day>*: The day of the week cache node should be updated. Week starts from Monday.<br>
  Accepted values: 1,2,3,4,5,6,7
* *\<auto-update-time>*: The time of day cache node should be updated in 24 hour format (hh:mm)
* *\<auto-update-week>*: The week of month cache node should be updated.<br>
  Accepted values: 1,2,3,4
  
```azurecli-interactive
az mcc ent node update --cache-node-name <mycachenode> --mcc-resource-name <mymccresource> --resource-group <myrg>
--cache-drive "[{physical-path:/var/mcc,size-in-gb:<size of cache drive>}]" --proxy <enabled> --proxy-host <"proxy host name"> --proxy-port <proxy port>  --auto-update-day <day of week> --auto-update-time <time of day> --auto-update-week <week of month> --auto-update-ring <update ring>
```

---

## Next step

### [Azure portal](#tab/portal)
To deploy the cache node to a **Windows** host machine, see [Deploy cache node to Windows](mcc-ent-deploy-to-windows.md)

To deploy the cache node to a **Linux** host machine, see [Deploy cache node to Linux](mcc-ent-deploy-to-linux.md)

### [Azure CLI](#tab/cli/)
To deploy cache nodes using Azure CLI, see [Bulk management of cache nodes](mcc-ent-manage-cache-using-CLI.md)

---
<br>
<br>


### General configuration fields

| Field Name |Expected Value |Description|
|---|---|---|
|**Cache node name** | Alphanumeric string that contains no spaces| The name of the cache node. You may choose names based on location such as "Seattle-1". This name must be unique and can't be changed later |
|**Host OS** | Linux or Windows| This is the operating system of the host machine that the cache node will be deployed to.|

### Storage fields

##### Cache node for Linux

>[!Important]
>All cache drives must have full read/write permissions set or the cache node will not function. For example, in a terminal you can run: sudo chmod 777 /path/to/cachedrivefolder
<br>

| Field Name |Expected Value |Description|
|---|---|---|
|**Cache drive folder**| File path string |Up to nine drive folders accessible by the cache node can be configured for each cache node to configure cache storage. Enter the location of the folder in Ubuntu where the external physical drive is mounted. For example: /dev/sda3/. Each cache drive should have read/write permissions configured. Ensure your disks are mounted and visit Attach a data disk to a Linux VM for more information.|
|**Cache drive size in gigabytes**| Integer in GB| Set the size of each drive configured for the cache node. Minimum cache drive size is 50 GB.|

##### Cache node for Windows

| Field Name |Expected Value |Description|
|---|---|---|
|**Cache drive folder**| File path string /var/mcc| This is the folder path where content is cached. You can't change the folder path.|
|**Cache drive size in gigabytes**| Integer in GB| Set the size of each drive configured for the cache node. Minimum cache drive size is 50 GB. |

#### Proxy settings
<br>
You can choose to enable or disable proxy settings on your cache node.

<br>

>[!IMPORTANT]
>Enabling or disabling the proxy settings after your cache node has been deployed will require running the provisioning script again. This will ensure that proxy changes are in effect on the cache node. 

| Field Name	|Expected Value	 |Description|
|---|---|---|
|**Proxy host name**|	String or number|	Proxy host name or address|
|**Proxy port**|	Integer|	Proxy port
