---
title: 'Configuration deployments in Azure Virtual Network Manager (Preview)'
description: Learn about how configuration deployments work in Azure Virtual Network Manager.
author: mbender-ms    
ms.author: mbender
ms.service: virtual-network-manager
ms.topic: conceptual
ms.date: 07/06/2022
ms.custom: template-concept, ignite-fall-2021
---

# Configuration deployments in Azure Virtual Network Manager (Preview)

In this article, you'll learn about how configurations are applied to your network resources. You'll also explore how updating a configuration deployment is different for each membership type. Then we'll go into details about *Deployment status* and *Goal state model*.

## Deployment

*Deployment* is the method Azure Virtual Network Manager uses to apply configurations to your virtual networks in network groups. Configurations won't take effect until they are deployed. When a deployment request is sent to Azure Virtual Network Manager, it will calculate the [goal state](#goalstate) of all resources under your network manager in that region as a combination of deployed configurations and network group membership. Network manager will then apply the necessary changes to your infrastructure.

When committing a deployment, you select the region(s) to which the configuration will be applied. This allows you to gradually roll out changes on a per-region granularity to promote a safe deployment practice. The deployed configuration is also static. Once deployed, you can edit your configurations freely without imacting your deployed setup. Applying any of these new changes will take another deployment.

The changes reprocess the entire region and can take a few minutes depending on how large the configuration is. Changes to network groups, however, will take effect without the need for re-deployment. This includes adding or removing group members directly, or configuring an Azure Policy resource.

## Deployment status

When you commit a configuration deployment, the API does a POST operation. Once the deployment request has been made, Azure Virtual Network Manager will calculate the goal state of your networks in the deployed regions and request the underlying infrastructure to make the changes. You can see the deployment status on the *Deployment* page of the Virtual Network Manager.

:::image type="content" source="./media/tutorial-create-secured-hub-and-spoke/deployment-in-progress.png" alt-text="Screenshot of deployment in progress in deployment list.":::

## <a name = "goalstate"></a> Goal state model

When you commit a deployment of configuration(s), you're describing the goal state of your network manager in that region. This goal state is an atomic unit that is upserted upon next deployment. For example, when you commit configurations named *Config1* and *Config2* into a region, these two configurations get applied  and become the goal of this region. If you decided to commit configuration named *Config1* and *Config3* into the same region, *Config2* would then be removed and *Config3* would be added. To remove all configurations, you would deploy a **None** configuration against the region(s) you no longer wish to have any configurations applied.

## Next steps

Learn how to [create an Azure Virtual Network Manager instance](create-virtual-network-manager-portal.md).
