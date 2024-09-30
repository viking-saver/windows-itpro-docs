---
title: Monitor usage of MCCE cache nodes
description: Details on how to monitor the usage of Microsoft Connected Cache for Enterprise (MCCE) cache nodes.
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
ms.date: 09/04/2024
---

# Monitor MCCE cache node usage

Tracking the status and performance of your MCCE cache node is essential to making sure that you're getting the most out of the service.

<!-- Add standard metrics

      Add scenarios for creating custom metrics -->

## Cache node summary

The Cache Node Summary box on your Azure portal 

| Metric | Description |
| --- | --- |
| Healthy nodes | The MCCE service will periodically request heartbeat messages from your MCC node to determine if it is functioning as expected. |
| Unhealthy nodes | If the cache node does not respond, it will be labeled as unhealthy. |
| Max in | The maximum egress (in Mb/sec.) that your node has pulled in at any given time. This statistic is not dependent on the time filter near the charts. |
| Max out | The minimum egress (in Mb/sec.) that your node has pushed out at any given time. |
| Average in | The average ingress (in Mb/sec.) that your node has pulled in over its lifetime. This statistic is not dependent on the time filter near the charts. |
| Average out | The average egress (in Mb/sec.) that your node has pushed out over its lifetime. |
| Cache efficiency | The percentage of all requests that your MCC node receives that are ultimately delivered by your MCC node. An effective node is generally expected to have an efficiency >95%. |

## Charts

### Filters

- Will only filter the data shown in the 2 charts, scalable from 1 hour to 30 days
- Can view data by individual cache nodes or the average of all your active MCC nodes.

### Outbound traffic

- The egress (in Mb/sec) that your MCC node is pushing out at specific time intervals

### Volume by Content Type

- The volume of content that your MCCE cache node is distributing, broken down by the hostname used to download said content

## Additional metrics

### Custom metrics

- Navigate to the "Metrics" tab in the left-hand toolbar
- Configure chart as desired using the provided metrics

<!-- ### Windows Update for Business (WUfB) reports -->