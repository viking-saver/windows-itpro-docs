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

This article contains instructions on how to troubleshoot different issues you may encounter while using Connected Cache. These issues are categorized by the task in which they may be encountered. For example, this next section covers troubleshooting [Connected Cache Azure resource creation](mcc-ent-create-resource-and-cache.md).

## Steps to obtain an Azure subscription ID

<!--Using include file, get-azure-subscription.md, do/mcc-isp.md for shared content-->
[!INCLUDE [Get Azure subscription](includes/get-azure-subscription.md)]

## Troubleshooting Azure resource creation

Connected Cache Azure resource creation can be initiated using either the Azure portal or the Azure CLI command set. If you're encountering an error during resource creation, check that you have the necessary RPaaS permissions and have filled out all required fields.

## Troubleshooting cache node issue

If you're facing issues with your cache node, it could be due to cache node being on the early preview version of Connected Cache. Cache nodes belonging to early preview version will be under Connected Cache resource that will have 'early preview' in its name. Please delete these cache nodes and associated Connected Cache resource and create a new Connected Cache resource on the new version.
For detailed instructions on creating Connected Cache resource, see [Create Connected Cache Azure resources](mcc-ent-create-resource-and-cache.md)

## Troubleshooting cache node deployment

TODO: Add introduction sentence(s)
[Include a sentence or two to explain only what is needed to complete the procedure.]
TODO: Add ordered list of procedure steps

1. Step 1
1. Step 2
1. Step 3

## Troubleshooting cache node monitoring

TODO: Add introduction sentence(s)
[Include a sentence or two to explain only what is needed to complete the procedure.]
TODO: Add ordered list of procedure steps

1. Step 1
1. Step 2
1. Step 3

<!-- 5. Next step/Related content------------------------------------------------------------------------

Optional: You have two options for manually curated links in this pattern: Next step and Related content. You don't have to use either, but don't use both.
  - For Next step, provide one link to the next step in a sequence. Use the blue box format
  - For Related content provide 1-3 links. Include some context so the customer can determine why they would click the link. Add a context sentence for the following links.

-->

## Diagnose and Solve

If this article isn't resolving the issue you're facing with your cache node, you can use the **Diagnose and solve problems** functionality within your Connected Cache resource to continue troubleshooting. **Diagnose and solve problems** contains solutions to most common problems that users might face as they onboard.

You can find **Diagnose and solve problems** on the left pane within your Connected Cache resource.

Within **Diagnose and solve problems**, select **Troubleshoot** under the type of problem you're facing and follow the prompts that narrow down the solution to the issue.

## Filing a support request

TODO: Add steps for filling out a CSS ticket.
