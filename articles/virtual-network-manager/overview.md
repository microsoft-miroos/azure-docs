---
title: 'What is Azure Virtual Network Manager (Preview)?'
description: Learn how Azure Virtual Network Manager can simplify management and scalability of your virtual networks.
services: virtual-network-manager
author: mbender-ms
ms.service: virtual-network-manager
ms.topic: overview
ms.date: 07/06/2022
ms.author: mbender
ms.custom: references_regions, ignite-fall-2021
#Customer intent: As an IT administrator, I want to learn about Azure Virtual Network Manager and what I can use it for.
---

# What is Azure Virtual Network Manager (Preview)?

Azure Virtual Network Manager is a management service that enables you to group, configure, deploy, and manage virtual networks globally across subscriptions. With Virtual Network Manager, you can define network groups to identify and logically segment your virtual networks. Then you can determine the connectivity and security configurations you want and apply them across all the selected virtual networks in network groups at once.

## How does Azure Virtual Network Manager work?

:::image type="content" source="./media/overview/management-group.png" alt-text="Diagram of management group in Virtual Network Manager.":::

During the creation process, you define the scope for what your Azure Virtual Network Manager will manage. Your Network Manager will only have the delegated access to apply configurations within this scope boundary. Defining a scope can be done directly on a list of subscriptions. However it is recommended to use management groups to define your scope, which can in turn provide hieararchical organization to your subscriptions. (../governance/management-groups/overview.md). After defining the scope, you enable features such as *Connectivity* and the *SecurityAdmin* role for your Virtual Network Manager.

After you deploy the Virtual Network Manager instance, you then create a *network group*, which serves as a logical container of networking resources to apply configurations to en-masse. You can select indivual virtual networks to be added to your network group (static membership). You can also use Azure Policy to define conditionals which will govern your group membership dynamically and at high-scale. For more information about Azure Policy initiatives, see [Azure Virtual Network Manager and Azure Policy](../virtual-network-manager/concepts/azure-policy.md).  You then create connectivity and/or security configuration(s) applied to those network groups based on your topology and security needs. 

A connectivity configuration enables you to create a mesh or a hub-and-spoke network topology. A security configuration allows you to define a collection of rules that you can apply to one or more network groups at the global level. Once you've created your desired network groups and configurations, you can deploy the configurations to any region of your choosing.

## Key benefits

* Centrally manage connectivity and security policies globally across regions and subscriptions.

* Enable direct connectivity between spokes in a hub-and-spoke configuration without the complexity of managing a mesh network.

* Highly scalable and highly available service with redundancy and replication across the globe.

* Ability to create network security rules that override network security group rules.

* Low latency and high bandwidth between resources in different virtual networks using virtual network peering.

* Roll out network changes through a specific region sequence and frequency of your choosing.

## Next steps

- Create an [Azure Virtual Network Manager](create-virtual-network-manager-portal.md) instance using the Azure portal.
- Learn more about [network groups](concept-network-groups.md) in Azure Virtual Network Manager.
- Learn what you can do with a [connectivity configuration](concept-connectivity-configuration.md).
- Learn more about [security admin configurations](concept-security-admins.md).
