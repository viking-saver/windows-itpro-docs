---
title: Manage Recall for Windows clients
description: Learn how to manage Recall for commercial environments and about Recall features.
ms.topic: how-to
ms.subservice: windows-copilot
ms.date: 11/15/2024
ms.author: mstewart
author: mestew
ms.collection:
  - windows-copilot
  - magic-ai-copilot
appliesto:
- ✅ <a href="https://www.microsoft.com/windows/business/devices/copilot-plus-pcs#copilot-plus-pcs" target="_blank">Copilot+ PCs</a>
---


# Manage Recall
<!--8908044-->
>**Looking for consumer information?** See [Retrace your steps with Recall](https://support.microsoft.com/windows/retrace-your-steps-with-recall-aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c).

Recall (preview) allows users to search locally saved and locally analyzed snapshots of their screen using natural language. By default, Recall is disabled and removed on managed devices. IT admins can choose if they want to allow Recall to be used in their organizations and users, on their own, won't be able to install or enable it on their managed device if the Allow Recall policy is disabled. IT admins, on their own, can't start saving snapshots for end users. Recall is an opt-in experience that requires end user consent to save snapshots. Users can choose to enable or disable saving snapshots for themselves anytime. IT admins can only set policies that give users the option to enable saving snapshots and configure certain policies for Recall.

This article provides information about Recall and how to manage it in a commercial environment.

> [!NOTE]
> - For Copilot+ PCs that are running Windows Insiders, Recall (preview) is now available. For more information, see [**Placeholder WIP Blog link**>](https://aka.ms/windowsinsiders).
> - In-market commercial devices are defined as devices with an Enterprise (ENT) or Education (EDU) SKU or any premium SKU device that is managed by an IT administrator (whether via Microsoft Endpoint Manager or other endpoint management solution), has a volume license key, or is joined to a domain. Commercial devices during Out of Box Experience (OOBE) are defined as those with ENT or EDU SKU or any premium SKU device that has a volume license key or is Microsoft Entra joined. 
> - Recall is optimized for select languages English, Chinese (simplified), French, German, Japanese, and Spanish. Content-based and storage limitations apply. For more information, see [https://aka.ms/copilotpluspcs](https://aka.ms/copilotpluspcs).

## What is Recall?

Recall (preview) allows you to search across time to find the content you need. Just describe how you remember it, and Recall retrieves the moment you saw it. Snapshots are taken periodically while content on the screen is different from the previous snapshot. The snapshots of your screen are organized into a timeline. Snapshots are locally stored and locally analyzed on your PC. Recall's analysis allows you to search for content, including both images and text, using natural language.

When Recall opens a snapshot you selected, it enables Click to Do, which runs on top of the saved snapshot. Click to Do analyzes what's in the snapshot and allows you to interact with individual elements in the snapshot. For instance, you can copy text from the snapshot or send pictures from the snapshot to an app that supports `jpeg` files.

:::image type="content" border="true" source="images/8908044-recall.png" alt-text="Screenshot of Recall with search results displayed for a query for a presentation with a red barn." lightbox="images/8908044-recall.png":::

### Recall security and privacy architecture

Privacy and security are built into Recall's design. With Copilot+ PCs, you get powerful AI that runs locally on the device. No internet or cloud connections are required or used to save and analyze snapshots. Snapshots aren't sent to Microsoft. Recall AI processing occurs locally, and snapshots are securely stored on the local device only.

Recall doesn't share snapshots with other users that are signed into Windows on the same device and IT admins can't access or view the snapshots on end-user devices. Microsoft can't access or view the snapshots. Recall requires users to confirm their identity with [Windows Hello](https://support.microsoft.com/windows/configure-windows-hello-dae28983-8242-bb2a-d3d1-87c9d265a5f0) before it launches and before accessing snapshots. At least one biometric sign-in option must be enabled for Windows Hello, either facial recognition or a fingerprint, to launch and use Recall. Before snapshots start getting saved to the device, users need to open Recall and authenticate. Recall takes advantage of just in time decryption protected by [Hello Enhanced Sign-in Security (ESS)](/windows-hardware/design/device-experiences/windows-hello-enhanced-sign-in-security). Snapshots and any associated information in the vector database are always encrypted. Encryption keys are protected via Trusted Platform Module (TPM), which is tied to the user's Windows Hello ESS identity, and can be used by operations within a secure environment called a [Virtualization-based Security Enclave (VBS Enclave)](/windows/win32/trusted-execution/vbs-enclaves). This means that other users can't access these keys and thus can't decrypt this information. Device Encryption or BitLocker are enabled by default on Windows 11. For more information, see [Recall security and privacy architecture in the Windows Experience Blog](https://blogs.windows.com/windowsexperience/?p=179096).

When using Recall, the **Sensitive information filtering** setting is enabled by default to help ensure your data's confidentiality. This feature operates directly on your device, utilizing the NPU and the Microsoft Classification Engine (MCE) - the same technology leveraged by [Microsoft Purview](/purview/purview) for detecting and labeling sensitive information. When this setting is enabled, snapshots won't be saved when potentially sensitive information is detected. Most importantly, the sensitive information remains on the device at all times, regardless of whether the Sensitive Information Filtering setting is enabled or disabled. For more information about the types of potentially sensitive information, see [Reference for sensitive information filtering in Recall](recall-sensitive-information-filtering.md).

In keeping with Microsoft's commitment to data privacy and security, all saved images and processed data are kept on the device and processed locally. However, Click to Do allows users to choose if they want to perform additional actions on their content.

Click to Do allows users to choose to get more information about their selected content online. When users choose one of the following Click to Do actions, the selected content is sent to the online provider from the local device to complete the request:

-	**Search the web**: Sends the selected content to the default search engine of the default browser
-	**Open website**: Opens the selected website in the default browser
-	**Visual search with Bing**: Sends the selected content to Bing visual search using the default browser. 

When users choose to send content from Click to Do to an app, like Paint, Click to Do will temporarily save the selected content in order to complete the transfer. Click to Do creates a temporary file in one of the following locations: 
- `C:\Users\[username]\AppData\Local\Temp` 
- `C:\Users\{username}\AppData\Local\Packages\MicrosoftWindows.Client.AIX_cw5n1h2txyewy\TempState`

The temporary file is deleted once the app is finished with the content.

## System requirements

Recall has the following minimum requirements:

- A [Copilot+ PC](https://www.microsoft.com/windows/business/devices/copilot-plus-pcs#copilot-plus-pcs)
- 40 TOPs Neural Processing Unit (NPU)
- 16 GB RAM
- 8 logical processors
- 256 GB storage capacity
  - To enable Recall, you need at least 50 GB of space free
  - Saving snapshots automatically pauses once the device has less than 25 GB of disk space
- Users need to enroll into [Windows Hello](/windows/security/identity-protection/hello-for-business/) with at least one biometric sign-in option enabled in order to authenticate.

## Supported browsers

Users need a supported browser for Recall to [filter websites](#app-and-website-filtering-policies) and to automatically filter private browsing activity. Supported browsers, and their capabilities include:

- **Microsoft Edge**: filters specified websites and filters private browsing activity
- **Firefox**: filters specified websites and filters private browsing activity
- **Opera**: filtered specified websites and filters private browsing activity
- **Google Chrome**: filters specified websites and filters private browsing activity
- **Chromium based browsers** (124 or later): For Chromium-based browsers not listed, filters private browsing activity only, doesn't filter specific websites


## Configure policies for Recall

By default, Recall is removed on commercially managed devices. If you want to allow Recall to be available for users in your organization and allow them to choose to save snapshots, you need to configure both the **Allow Recall to be enabled** and **Turn off saving snapshots for Windows** policies. Policies for Recall fall into the following general areas:

- [Allow Recall and snapshots policies](#allow-recall-and-snapshots-policies)
- [Storage policies](#storage-policies)
- [App and website filtering policies](#app-and-website-filtering-policies)


### Allow Recall and snapshots policies

The **Allow Recall to be enabled** policy setting allows you to determine whether the Recall optional component is available for end users to enable on their device. By default, Recall is disabled and removed for managed devices. Recall isn't available on managed devices by default, and individual users can't enable Recall on their own. If you disable this policy, the Recall component will be in disabled state and the bits for Recall will be removed from the device. If snapshots were previously saved on the device, they will be deleted when this policy is disabled. Removing Recall requires a device restart. If the policy is enabled, end users will have Recall available on their device. Depending on the state of the DenyAIDataAnalysis policy (Turn off saving snapshots for use with Recall), end users will be able to choose if they want to save snapshots of their screen and use Recall to find things they've seen on their device.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[AllowRecallEnablement](mdm/policy-csp-windowsai.md#allowrecallenablement) |
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Allow Recall to be enabled** |


The **Turn off saving snapshots for Windows** policy allows you to give the users the choice to save snapshots of their screen for use with Recall. Administrators can't enable saving snapshots on behalf of their users. The choice to enable saving snapshots requires individual user opt-in consent. By default, snapshots won't be saved for use with Recall. If snapshots were previously saved on a device, they'll be deleted when this policy is enabled. If you set this policy to disabled, end users will have a choice to save snapshots of their screen and use Recall to find things they've seen on their device.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[DisableAIDataAnalysis](mdm/policy-csp-windowsai.md#disableaidataanalysis) </br> </br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[DisableAIDataAnalysis](mdm/policy-csp-windowsai.md#disableaidataanalysis)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Turn off saving snapshots for Windows** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **Turn off saving snapshots for Windows** |

### Storage policies

You can define how much disk space Recall can use by using the **Set maximum storage for snapshots used by Recall** policy. You can set the maximum amount of disk space for snapshots to be 10, 25, 50, 75, 100, or 150 GB. When the storage limit is reached, the oldest snapshots are deleted first. When this setting isn't configured, the OS configures the storage allocation for snapshots based on the device storage capacity. 25 GB is allocated when the device storage capacity is 256 GB. 75 GB is allocated when the device storage capacity is 512 GB. 150 GB is allocated when the device storage capacity is 1 TB or higher.	

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[SetMaximumStorageSpaceForRecallSnapshots](mdm/policy-csp-windowsai.md#setmaximumstoragespaceforrecallsnapshots) </br> </br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[SetMaximumStorageSpaceForRecallSnapshots](mdm/policy-csp-windowsai.md#setmaximumstoragespaceforrecallsnapshots)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Set maximum storage for snapshots used by Recall** </br></br> User Configuration > Administrative Templates > Windows Components > Windows AI > **Set maximum storage for snapshots used by Recall** |

You can define how long snapshots can be retained on the device by using the **Set maximum duration for storing snapshots used by Recall** policy. You can configure the maximum storage duration to be 30, 60, 90, or 180 days. If the policy isn't configured, snapshots aren't deleted until the maximum storage allocation is reached, and then the oldest snapshots are deleted first.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[SetMaximumStorageDurationForRecallSnapshots](mdm/policy-csp-windowsai.md#SetMaximumStorageDurationForRecallSnapshots) </br></br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[SetMaximumStorageDurationForRecallSnapshots](mdm/policy-csp-windowsai.md#sSetMaximumStorageDurationForRecallSnapshots)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Set maximum storage for snapshots used by Recall** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **Set maximum duration for storing snapshots used by Recall** |


### App and website filtering policies

You can filter both apps and websites from being saved in snapshots. Users are able to add to these filter lists from the **Recall & Snapshots** settings page. Some remote desktop connection clients are filtered by default from snapshots. For more information, see the [Remote desktop connection clients filtered from snapshots](#remote-desktop-connection-clients-filtered-from-snapshots) section.

To filter websites from being saved in snapshots, use the **Set a list of URIs to be filtered from snapshots for Recall** policy. Define the list using a semicolon to separate URIs. Make sure you include the URL scheme such as `http://`, `file://`, `https://www.`. Sites local to a supported browser like `edge://`, or `chrome://`, are filtered by default. For example: `https://www.Contoso.com;https://www.WoodgroveBank.com;https://www.Adatum.com`

> [!NOTE]
> - Private browsing activity is filtered by default when using [supported web browsers](#supported-browsers). 
> - Be aware that websites are filtered when they are in the foreground or are in the currently opened tab of a supported browser. Parts of filtered websites can still appear in snapshots such as embedded content, the browser's history, or an opened tab that isn't in the foreground.
> - Filtering doesn't prevent browsers, internet service providers (ISPs), websites, organizations, or others from knowing that the website was accessed and building a history.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[SetDenyUriListForRecall](mdm/policy-csp-windowsai.md#setdenyurilistforrecall) </br></br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[SetDenyUriListForRecall](mdm/policy-csp-windowsai.md#setdenyurilistforrecall)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **>Set a list of URIs to be filtered from snapshots for Recall** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **>Set a list of URIs to be filtered from snapshots for Recall** |


**Set a list of apps to be filtered from snapshots for Recall** policy allows you to filter apps from being saved in snapshots. Define the list using a semicolon to separate apps. The list can include Application User Model IDs (AUMID) or the name of the executable file. For example: `code.exe;Microsoft. WindowsNotepad_8wekyb3d8bbwe!App;ms-teams.exe`

> [!Note]
>	Like other Windows apps, such as the Snipping Tool, Recall won't store digital rights management (DRM) content.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./Device/Vendor/MSFT/Policy/Config/WindowsAI/[SetDenyAppListForRecall](mdm/policy-csp-windowsai.md#setdenyapplistforrecall) </br></br> ./User/Vendor/MSFT/Policy/Config/WindowsAI/[SetDenyAppListForRecall](mdm/policy-csp-windowsai.md#setdenyapplistforrecall)|
| **Group policy** | Computer Configuration > Administrative Templates > Windows Components > Windows AI > **Set a list of apps to be filtered from snapshots for Recall** </br></br>User Configuration > Administrative Templates > Windows Components > Windows AI > **Set a list of apps to be filtered from snapshots for Recall**|


#### Remote desktop connection clients filtered from snapshots

Snapshots won't be saved when some remote desktop connection clients are used. The following remote desktop connection clients are filtered by default from snapshots:<!--9119193-->

   - [Remote Desktop Connection (mstsc.exe)](/windows-server/administration/windows-commands/mstsc)
   - [VMConnect.exe](/windows-server/virtualization/hyper-v/learn-more/hyper-v-virtual-machine-connect) 
      - [Microsoft Remote Desktop from the Microsoft Store](/windows-server/remote/remote-desktop-services/clients/windows) is saved in snapshots. To prevent the app from being saved in snapshots, add it to the app filtering list.
   - [Azure Virtual Desktop (MSI)](/azure/virtual-desktop/users/connect-windows) 
      - [Azure Virtual Desktop apps from the Microsoft Store](/azure/virtual-desktop/users/connect-remote-desktop-client) are saved in snapshots. To prevent these apps from being saved in snapshots, add then to the app filtering list.
  - [Remote applications integrated locally (RAIL)](/openspecs/windows_protocols/ms-rdperp/485e6f6d-2401-4a9c-9330-46454f0c5aba) windows




## Information for developers

If you're a developer and want to launch Recall, you can call the `ms-recall` protocol URI. When you call this URI, Recall opens and takes a snapshot of the screen, which is the default behavior for when Recall is launched. For more information about using Recall in your Windows app, see [Recall overview](/windows/ai/apis/recall) in the Windows AI API documentation.

## Microsoft's commitment to responsible AI

Microsoft has been on a responsible AI journey since 2017, when we defined our principles and approach to ensuring this technology is used in a way that is driven by ethical principles that put people first. For more about our responsible AI journey, the ethical principles that guide us, and the tooling and capabilities we've created to assure that we develop AI technology responsibly, see [Responsible AI](https://www.microsoft.com/ai/responsible-ai).

Recall uses optical character recognition (OCR), local to the PC, to analyze snapshots and facilitate search. For more information about OCR, see [Transparency note and use cases for OCR](/legal/cognitive-services/computer-vision/ocr-transparency-note). For more information about privacy and security, see [Privacy and control over your Recall experience](https://support.microsoft.com/windows/privacy-and-control-over-your-recall-experience-d404f672-7647-41e5-886c-a3c59680af15).

## Related links
- [Policy CSP - WindowsAI](/windows/client-management/mdm/policy-csp-windowsai)
- [Update on Recall security and privacy architecture](https://blogs.windows.com/windowsexperience/2024/09/27/update-on-recall-security-and-privacy-architecture/)
- [Retrace your steps with Recall](https://support.microsoft.com/windows/aa03f8a0-a78b-4b3e-b0a1-2eb8ac48701c)
- [Privacy and control over your Recall experience](https://support.microsoft.com/windows/d404f672-7647-41e5-886c-a3c59680af15)
- [<PLACEHOLDER WIP BLOG>](https://aka.ms/wip)
