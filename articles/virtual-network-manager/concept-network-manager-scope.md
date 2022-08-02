---
title: 'Understand and work with Azure Virtual Network Manager scopes'
description: Learn about Azure Virtual Network Manager scopes and the effects it has on managing virtual networks.
author: duongau
ms.author: duau
ms.service: virtual-network-manager
ms.topic: conceptual
ms.date: 11/02/2021
ms.custom: template-concept, ignite-fall-2021
---

# Understand and work with Azure Virtual Network Manager (Preview) scopes

In this article, you'll learn about how Azure Virtual Network Manager uses the concept of *scope* to enable management groups or subscriptions to use certain features of Virtual Network Manager. You'll also learn about *hierarchy* and how that can affect your users when using Virtual Network Manager. 

## Network Manager

*Network Manager* is the top-level object consist of child resources such as *network groups*, *configurations*, and *rules*. 

* **Network Groups** - a subset of the overall scope, to which specific connectivity or security admin policies can be applied to.

* **Configurations** - Azure Virtual Network Manager provides two types of configurations, a connectivity configuration and a security configuration. Connectivity configurations enables you to create network topologies, while security configurations enable you to create a collection of rules that you can apply across virtual networks.

* Rules - A rule collection, is a set of network security rules that can either allow or deny network traffic at the global level for your virtual networks. 

## Scope

A *scope* within Azure Virtual Network Manager represents the delegated access granted to a network manager, within which features can be applied to. When specifying a scope, you're limiting the access to which Network Manager can manage resources for. The value for the scope can be at the management group level or at the subscription level. See [Azure management groups](../governance/management-groups/overview.md), to learn how to manage your resource hierarchy. When you select a management group as the scope, all child resources are included within the scope. 

> [!NOTE]
> You can't create multiple Azure Virtual Network Manager instances with an overlapping scope of the same hierarchy and the same features selected.


### Scope Applicability
When deploying configurations, Network Manager will only apply features to resources within it's scope. Thus, if you attempt to add a resource to a network group which is out of scope, it will be added to the group to represent your intent, but the network manager will fail to apply configurations to it.

The Network Manager's scope can be updated to add or remove scopes from it's list, which will trigger an automatic, scope wide, reevaluation and potentially add features in the case of a scope addition, or remove them in the case of a removal.

## Features

Features are scope access that you allow the Azure Virtual Network Manager to manage. Azure Virtual Network Manager currently has two feature scopes, which are *Connectivity* and *SecurityAdmin*. You can enable both feature scopes on the same Virtual Network Manager instance. For more information about each feature, see [Connectivity](concept-connectivity-configuration.md) and [SecurityAdmin](concept-security-admins.md).


## Hierarchy

Azure Virtual Network Manager allows for management of your network resources in a hierarchy. A hierarchy means you can have multiple Virtual Network Manager instances manage overlapping scopes and the configurations within each Virtual Network Manager can also overlay one another. For example, you can have the top-level [management group](../governance/management-groups/overview.md) of one Virtual Network Manager and have a child management group as the scope for a different Virtual Network Manager. When you have a configuration conflict between different Virtual Network Manager instances that contains the same resource. The configuration from the Virtual Network Manager that has the higher scope will be the one that gets applied.

## Next steps

- Learn how to create an [Azure Virtual Network Manager](create-virtual-network-manager-portal.md) instance.
- Learn about [Network groups](concept-network-groups.md).
