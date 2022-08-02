---
title: "What is a network group in Azure Virtual Network Manager (Preview)?"
description: Learn about how Network groups can help you manage your virtual networks.
author: mbender-ms
ms.author: mbender
ms.service: virtual-network-manager
ms.topic: conceptual
ms.date: 07/11/2022
ms.custom: template-concept, ignite-fall-2021
---

# What is a network group in Azure Virtual Network Manager (Preview)?

In this article, you'll learn about *network groups* and how they can help you group virtual networks together for easier management. You'll also learn about *Static group membership* and *Dynamic group membership* and how to use each type of membership.

## Network group

A *network group* is a global container to which networking resources from any region can be added. Configurations can later be applied to target these network group abstractions, which in turn will apply the configuration to all members of the group.

## Group Membership

Group membership is a many-to-many relationship, such that one group holds many virtual networks and any given virtual network can participate in multiple network groups. When a part of a network group, the virtual network will recieve any configurations which were applied to the group and deployed to the virtual networks region.

### Sources
A virtual network can be set to join a network group in multiple ways. This membership is an at-least-one condition, so the group will remain in the group so long as there is anything adding it, and leave the group when these sources are gone.

#### Static Membership
Static membership allows you to explicitly add virtual networks to a group by manually selecting individual virtual networks. The list of virtual networks is dependent on the scope (management group or subscription) defined at the time of the Azure Virtual Network Manager deployment. This method is useful when you have a few virtual networks you want to add to the network group. Static membership also allows you to 'patch' the network group contents by individually addinng or removing a virtual network from the group.

#### Dynamic membership
Dynamic membership gives you the flexibility of selecting multiple virtual networks at scale if they meet the conditional statements you defined. Powered by Azure policy, this method is useful for scenarios where you have hundreds or thousands of virtual networks, or if membership is dictated by a condition instead of an explicit list. See [How can Azure Policy work with Network Groups](concepts-azure-policy) for more details about powering your network groups with Policy.

### Discoverability
All group membership is recorded in Azure Resource Graph and available for your use. Each virtual network recieves a single entry in the graph, which specifies both all the groups the virtual network is a member of, as well as what contributing sources are responsible for that membership, either static members or various policy resources. See our [Discoverability How-To](https://github.com/microsoft-miroos/azure-docs/blob/main/articles/virtual-network-manager/how-to-view-applied-configurations.md#network-group-memberhip) for mor information.

## Next steps

- Create an [Azure Virtual Network Manager](create-virtual-network-manager-portal.md) instance using the Azure portal
- Learn how to create a [Hub and spoke topology](how-to-create-hub-and-spoke.md) with Azure Virtual Network Manager
- Learn how to block network traffic with a [SecurityAdmin configuration](how-to-block-network-traffic-portal.md)
- Review [Azure Policy basics](../governance/policy/overview.md)
