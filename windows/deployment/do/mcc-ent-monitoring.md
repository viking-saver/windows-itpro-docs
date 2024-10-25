---
title: Monitor usage of Microsoft Connected Cache nodes
description: Details on how to monitor the usage of Microsoft Connected Cache for Enterprise cache nodes.
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

# Monitor cache node usage

Tracking the status of your Connected Cache node is essential to making sure you are getting the most out of the service.

For basic monitoring, navigate to the "Overview" tab. Here you will be able to view a cache node summary dashboard and charts for key metrics. No additional work is necessary, all the monitoring in this section will function right after your Connected Cache node has been installed.

For advanced monitoring, navigate to the "Metrics" section under the "Monitoring" tab. Here you will be able to access more sampled metrics (hits, misses, inbound traffic) and specify different aggregations (count, avg, min, max, sum). You can then use this data to create customized dashboards and configure alerts. Overall, this section is designed to cater to your specific monitoring needs and preferences.

Between the two monitoring sections, you will be able to gather essential insights into the health, performance, and efficiency of your Connected Cache nodes.

## Basic Monitoring

### Cache node summary

The preset monitoring data for Connected Cache is displayed on the Overview page in the Azure portal. Below are the metrics you will find in the "Cache Node Summary" dashboard, along with their descriptions. Please take note that this dashboard only reflects data from all cache nodes the last 24 hours. The filters that are displayed below the dashboard only affect the data shown in the "Key Metrics" charts.

<!-- Add Cache node summary picture here -->
![Screenshot of cache node summary in the Azure portal interface.](../images/mcc-ent-cache-node-summary.png)

| Metric | Description |
| --- | --- |
| Healthy nodes | Your Connected Cache node will frequently send heartbeat messages to our backend. If your node has responded in the last 24 hours, it will be labeled as healthy. |
| Unhealthy nodes | If your node has not sent a heartbeat message in the last 24 hours, it will be labeled as unhealthy. |
| Max in | The maximum ingress in Mbps (Megabits per second) that your node has pulled from CDN in the last 24 hours. |
| Max out | The minimum egress in Mbps that your node has pushed out to devices in your network over the last 24 hours. |
| Average in | The average ingress in Mbps that your node has pulled from CDN in the last 24 hours. |
| Average out | The average egress in Mbps that your node has pushed out to devices in your network over the last 24 hours. |
| Cache efficiency | The percentage of all content requests your Connected Cache node receives that are ultimately delivered by your Connected Cache node. An well-performing node should have an efficiency > 90%. |

### Key Metrics

The two monitoring charts on the Overview page more visually represent the usage of your Connected Cache node, as well as the types cached content delivered by your node over various time intervals.

<!-- Add Charts picture here -->
![Screenshot of key metric charts in the Azure portal interface.](../images/mcc-ent-key-metric-charts.png)

#### Filters

Both filters displayed will only impact the data shown in the 2 charts below.

      - By time: View data from the last 1 hour to 30 days
      - By cache node: View data from individual cache nodes or the sum of all your active Connected Cache nodes.

#### Outbound Traffic Chart

This chart displays the egress in Mbps that your Connected Cache node was delivering at specific timestamps. The value in the chart's key represents the average egress over the specified time period.  

#### Volume by Content Type

This chart displays the amount (in GB) of each supported content type that your Connected Cache node is delivering at specific timestamps. You can find the complete list of supported content types here: [Microsoft Connected Cache content and services endpoints | Microsoft Learn](https://learn.microsoft.com/en-us/windows/deployment/do/delivery-optimization-endpoints)

The content types in the key are sorted from highest to lowest volume an each have a distinct color. The bar chart is stacked such that you can visually compare total volume being delivered at different timestamps

## Advanced Monitoring

To expand upon the metrics shown in the Overview tab, navigate to the "Metrics" tab in the left side toolbar of Azure Portal.

Listed below are the additional metrics you can access in this section:

| Metric | Description |
| --- | --- |
| Inbound | The number of content requests your Connected Cache node receives over a specified period of time. |
| Hits | The number of times your Connected Cache node fulfills a content request by pulling from its cache. |
| Misses | The number of times your Connected Cache node is not able to fulfill a content request by pulling from its cache |

### Customizable Dashboards

Once you select the charts you would like to track, you can save them over to a personalized dashboard. This dashboard enables you to configure the chart title, filters, range, legend, and more. You can also use this personalized dashboard to set up alerts that will notify you if your Connected Cache node dips in performance.

Some scenarios where you would want to set up these alerts:
      • My Connected Cache node is being shown as unhealthy and I want to know exactly when it stopped egressing last.
A new Xbox update just released last night and I want to know if my Connected Cache node is helping deliver this content to my client machines.

## Additional Metrics

Once the content has left the Connected Cache node, the node cannot track whether the content has successfully been delivered to the requesting Windows client. To access client-side data, you can refer to this page: [Monitor Delivery Optimization | Microsoft Learn](https://learn.microsoft.com/en-us/windows/deployment/do/waas-delivery-optimization-monitor)