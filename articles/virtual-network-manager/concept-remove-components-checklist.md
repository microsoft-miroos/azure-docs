---
title: 'Removing Azure Virtual Network Manager Preview components checklist'
description: This article is a checklist for deleting components within Azure Virtual Network Manager.
author: duongau
ms.author: duau
ms.service: virtual-network-manager
ms.topic: conceptual
ms.date: 11/02/2021
ms.custom: ignite-fall-2021
---

# Remove and update Azure Virtual Network Manager Preview components checklist

In this article, you'll see a checklist of steps you need to complete to remove or update a configuration component of Azure Virtual Network Manager Preview.

## <a name="remove"></a>Remove components checklist

| Action | Steps | 
| ------ | ----- |
| Undeploy a connectivity configuration deployment | Deploy a **None** connectivity configuration to target regions. |
| Undeploy a security admin configuration deployment | Deploy a **None** connectivity configuration to target regions. |
| Remove a security admin rule | 1. Undeploy the security admin configuration deployment. </br> 2. Delete security admin rules associated with the security configuration. |
| Remove a security rule collection | 1. Undeploy the security admin configuration deployment. </br> 2. Delete security admin rules associated with the security configuration. </br> 3. Delete the rule collection. |
| Remove a security admin configuration | 1. Undeploy the security admin configuration deployment. </br> 2. Delete security admin rules associated with the security configuration. </br> 3. Delete the rule collection. </br> 4. Delete the security admin configuration. |
| Remove a connectivity configuration | 1. Undeploy connectivity configuration deployment. </br> 2. Delete the connectivity configuration. |
| Remove a network group | 1. Delete the connectivity configuration associated with this network group </br> 2. Delete all security rules associated with the network group. </br> 3. Delete any Policy resources attached to the network group. </br> 4. Delete the network group. |
| Delete the Azure Virtual Network Manager instance | 1. Delete all connectivity and security admin configurations. </br> 2. Delete all network groups. </br> 3. Delete the Azure Virtual Network Manager instance. |

## Update components checklist

The information presented in this table assumes you have a connectivity or security admin configuration deployed to a target region.

| Action | Steps |
| ------ | ----- |
| Add or remove a virtual network | 1. Add or delete the network group's child static member for the resource. |
| Add a virtual network using Azure Policy | Create/Update a Defintion with a conditional that includes your resource.  </br> Assign defintion to a scope that includes your resource |
| Remove a virtual network using Azure Policy | Update a Defintion with a conditional that includes your resource. OR deactivate the Policy Defintiion by deleting the Assignment resource.  </br> * Network Group membership is an At-Least-One relationship. If a virtual network is added to the network group by multiple soures, all must be removed before the virtual network can leave the network group. |
| Add, remove, or update configurations | Make the necessary changes to your configuration resources and then redeploy your entire regional goal state to each region. |

## Next steps

Create an [Azure Virtual Network Manager](create-virtual-network-manager-portal.md) instance using the Azure portal.
