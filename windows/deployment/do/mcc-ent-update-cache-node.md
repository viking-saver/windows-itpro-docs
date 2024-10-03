---
title: Update MCC cache nodes
description: Details on how Microsoft Connected Cache for Enterprise and Education (MCC) cache nodes are updated by Microsoft.
ms.service: windows-client
ms.subservice: itpro-updates
ms.topic: how-to
ms.author: andyriv
author: chrisjlin
manager: naengler
appliesto: 
- ✅ <a href=https://learn.microsoft.com/windows/release-health/supported-versions-windows-client target=_blank>Windows 11</a>
- ✅ Supported Linux distributions
- ✅ <a href=https://learn.microsoft.com/windows/deployment/do/waas-microsoft-connected-cache target=_blank>Microsoft Connected Cache for Enterprise and Education</a> 
ms.date: 09/27/2024
---
# Configure container update frequency for Microsoft Connected Cache for Enterprise and Education (MCC)

Microsoft Connected Cache for Enterprise and Education (MCC) caching software is deployed to host machines as a container. The container OS and any software component within the container will need to be updated for security vulnerabilities or quality issues, or performance improvements required to successfully operate the caching software. These Microsoft-published container updates are called "MCC updates" in this article.

Microsoft silently deploys MCC updates to your cache nodes based on the Update Ring setting you configure for each cache node.

## Update rings

MCC cache nodes can be configured to either the "Fast" or "Slow" update ring. If configured to update as part of the Fast ring, the cache node will be silently updated by Microsoft soon after the update is made available. If configured to update as part of the Slow ring, the cache node is silently updated by Microsoft within five weeks of the update becoming available.

In other words, configuring cache nodes to update as part of the Slow ring provides users with the option to delay the update process until they have validated that the latest MCC update works within their environment. For example, a user could configure a test cache node to update as part of the Fast ring and validate that clients can successfully interact with the test cache node after the latest MCC update has been applied. This builds confidence that service won't be interrupted when the production cache nodes are updated as part of the Slow ring.

### Update ring options

>[!IMPORTANT]
>In the event of a critical security patch, Microsoft may elect to initiate an MCC update to your cache node as soon as possible (even if the cache node has been set to the Slow Ring).

#### Fast Ring
All MCC cache nodes are configured to update as part of the Fast ring by default. MCC cache nodes in the Fast ring will be updated soon after an update is made available. Microsoft will silently update cache nodes at a time of day when update traffic is likely to be minimal, such as 3:00 AM (local time) on Saturday.

#### Slow Ring
Configuring an MCC cache node to update as part of the Slow ring provides users with the option to delay MCC software updates until the update can be validated. There are three settings that control when MCC updates will be applied to MCC cache nodes. All update ring settings can be managed from the Azure portal or through Azure CLI.

| Setting | Description |
| --- | --- |
| Week of the month | 1st to 4th week can be selected. There are three to four months in a year that could have a 5th week. If there's a 5th week, the update could be applied during that 5th week if the day of the week falls near the last day of the month.|
| Day of the week | Monday through Sunday can be selected. |
| Time of day | Time of day is based on UTC and a 24 hour clock. |

## Update process

When Microsoft publishes an MCC update, the MCC service attempts to update all MCC cache nodes based on their Update Ring membership. If a cache node can't complete the silent MCC update within 6 hours of starting, an error message is surfaced in the Azure portal.

## Update terminology, criteria, and SLA

MCC updates will be released based on need instead of on a set cadence.

| Update type | Criteria and SLA |
| --- | --- |
| Security | Security updates are the highest priority and will be released based on the severity rating of the vulnerability. [Critical and High](https://nvd.nist.gov/vuln-metrics/cvss) vulnerabilities will be released by Microsoft within 60 days of discovery. [Medium and Low](https://nvd.nist.gov/vuln-metrics/cvss) vulnerabilities will be released by Microsoft within 120 days |
| Quality | Quality updates fix a specific problem and addresses a noncritical, non-security-related bug. Quality updates could include performance fixes for a specific problem or changes related to cache efficiency or maximum egress for example. Quality updates will be released along with security updates or when necessary to ensure proper functioning of the Microsoft Connected Cache software. |

For information on all released Microsoft Connected Cache updates see the [MCC release notes](mcc-ent-release-notes.md).
