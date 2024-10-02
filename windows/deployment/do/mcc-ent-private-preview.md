---
title: MCCE Private Preview
description: Details on Microsoft Connected Cache for Enterprise (MCCE) Private Preview
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: conceptual
manager: naengler
ms.author: lichris
author: chrisjlin
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise</a>	
ms.date: 06/03/2024
---

<<<<<<< HEAD

# Microsoft Connected Cache for Enterprise and Education (early preview)

> [!NOTE]
> Microsoft Connected Cache for Enterprise and Education is now in public preview.
> To know more about the program, visit [MCC program overview](mcc-ent-edu-overview.md).

<br>

Microsoft Connected Cache for Enterprise and Education is now in public preview. To get started, visit [Create MCC resource and cache node](mcc-ent-create-resource-and-cache.md)

>[!IMPORTANT]
> If you are using the early preview version on MCC, please uninstall and delete the early preview cache node and the associated MCC resource and create a new one. To create a new MCC resource, visit [Create MCC resource and cache node](mcc-ent-create-resource-and-cache.md)

<br>
## Enterprise requirements for MCC

1. **Azure subscription**: MCC management portal is hosted within Azure and is used to create the Connected Cache [Azure resource](/azure/cloud-adoption-framework/govern/resource-consistency/resource-access-management) and IoT Hub resource. Both are free services.

    Your Azure subscription ID is first used to provision MCC services, and enable access to the preview. The MCC server requirement for an Azure subscription costs you nothing. If you don't have an Azure subscription already, you can create an Azure [pay-as-you-go](https://azure.microsoft.com/offers/ms-azr-0003p/) account, which requires a credit card for verification purposes. For more information, see the [Azure Free Account FAQ](https://azure.microsoft.com/free/free-account-faq/).

    The resources used for the preview and in the future when this product is ready for production will be free to you, like other caching solutions.
1. **Hardware to host MCC**: The recommended configuration serves approximately 35,000 managed devices, downloading a 2-GB payload in 24-hour timeframe at a sustained rate of 6.5 Gbps.<br>
For more information, visit [Hardware Requirments](mcc-ent-prerequisites.md)
  
=======
# Microsoft Connected Cache for Enterprise and Education (MCCE) Private Preview

If you participated in the MCCE early preview, thank you for your collaboration and feedback.

To continue using MCCE, we strongly recommend that you upgrade your existing cache nodes to the Public Preview release. Cache nodes created and deployed during early preview should still function but can no longer be managed or monitored remotely via the MCCE Azure service.

As such, we strongly recommend you [recreate your existing cache nodes in Azure](mcc-ent-create-resource-and-cache.md) and then [redeploy the MCCE caching software to your host machines](mcc-ent-deploy-to-windows.md) using the latest OS-specific installer. You don't need to re-create your MCC Azure resource.

## Next step

> [!div class="nextstepaction"]
> [View documentation for MCCE Public Preview](mcc-ent-edu-overview.md)
>>>>>>> baff7906fe02b76b4a3649d7e6c3acdac9534e66
