---
title: Frequently asked questions about Azure Virtual Network Manager
description: Find answers to frequently asked questions about Azure Virtual Network Manager.
services: virtual-network-manager
author: mbender-ms
ms.service: virtual-network-manager
ms.topic: article
ms.date: 4/18/2022
ms.author: mbender
ms.custom: references_regions, ignite-fall-2021
---

# Azure Virtual Network Manager FAQ

## General

### What are common use cases for using Azure Virtual Network Manager?

* As an IT security manager you can create different network groups to meet the requirements of your environment and its functions. For example, you can create network groups for Production and Test network environments, Dev teams, Finance department, etc. to manage their connectivity and security rules at scale. 

* You can apply connectivity configurations to create a mesh or a hub-and-spoke network topology for a large number of virtual networks across your organization's subscriptions. 

* You can deny high-risk traffic: As an administrator of an enterprise, you can block specific protocols or sources that will override any NSG rules that would normally allow the traffic.   

* Always allow traffic: You want to permit a specific security scanner to always have inbound connectivity to all your resources, even if there are NSG rules configured to deny the traffic.   

## Technical

### Can a virtual network belong to multiple Azure Virtual Network Managers?

Yes, a virtual network can belong to more than one Azure Virtual Network Manager.

### What is a global mesh network topology?

A global mesh allows for virtual networks across different regions to communicate with one another. The effects are similar to how global virtual network peering works.

### Is there a limit to how many network groups can be created?

There's no limit to how many network groups can be created.

### How do I remove the deployment of all applied configurations?

You'll need to deploy a **None** configuration to all regions that have you have a configuration applied.

### Can I add virtual networks from another subscription not managed by myself?

Yes, you'll need to have the appropriate permissions to access those virtual networks.

### What is dynamic group membership?

For more information, see [dynamic membership](concept-network-groups.md#dynamic-membership).

### How does the deployment of configuration differ for dynamic membership and static membership?

For more information, see [deployment against membership types](concept-deployments.md#deployment).

### How do I delete an Azure Virtual Network Manager component?

For more information, see [remove components checklist](concept-remove-components-checklist.md).

### How can I see what configurations are applied to help me troubleshoot?

You can view Azure Virtual Network Manager settings under **Network Manager** for a virtual network. You can see both connectivity and security admin configuration that are applied. For more information, see [view applied configuration](how-to-view-applied-configurations.md).

### Can a virtual network managed by Azure Virtual Network Manager be peered to a non-managed virtual network?

Yes, you can choose to override and delete an existing peering already created, or allow them to coexist with those created by Azure Virtual Network Manager.

### Can an Azure Virtual WAN hub be part of a network group? 

No, an Azure Virtual WAN hub can't be in a network group at this time.


### Can an Azure Virtual WAN be used as the hub in AVNM's hub and spoke topology configuration? 

No, an Azure Virtual WAN hub isn't supported as the hub in a hub and spoke topology at this time.

### My Virtual Network is not getting the configurations I am expecting.

#### Have you deployed your configuration to the vnets region?
Configurations in Azure Virtual Network Manager do not take effect until they are deployed. Make a deployment to the virtual networks region with the appropiate configurations.

#### Is your network group setup properly?
Check that both your virtual network is part of the network group, and that your configuration is properly applied to that same network group. Also, adding resources via Azure Policy can take some time to take effect. Check here for verifing [network group membership](concept-network-groups.md#network-group-membership).

#### Is your virtual network in scope?
A network manager is only delegated enough access to apply configurations to virtual networks within your scope. Even if a resource is in your network group, it if is out of scope, it will not recieve any configurations

#### Are you applying security rules to a SQL MI Vnet

Azure SQL Managed Instance has some network requirements. These are enforced through high priority Network Intent Policies, whos purpose conflicts with Security Admin Rules. By default, the application of Admin rules will be skipped on vnets containing any of these Intent Policies. Since allow rules pose no risk of conflict, you can opt to apply Allow Only rules by setting the If you only wish to use Allow rules, you can set AllowOnlyRules on securityConfiguration.properties.applyOnNetworkIntentPolicyBasedServices.


## Limits

### What are the service limitation of Azure Virtual Network Manager?

* A connected group can have up to 250 virtual networks. Virtual networks in a mesh topology are in a connected group, therefore a mesh configuration has a limit of 250 virtual networks.

* You can have network groups with or without direct connectivity enabled in the same hub-and-spoke configuration, as long as the total number of virtual networks peered to the hub **doesn't exceed 500** virtual networks.
    * If the network group peered with the hub **has direct connectivity enabled**, these virtual networks are in a *connected group*, therefore the network group has a limit of 250 virtual networks. 
    * If the network group peered with the hub **doesn't have direct connectivity enabled**, the network group can have up to the total limit for a hub-and-spoke topology.

* A virtual network can be part of up to two connected groups. 

    **Example:**
    * A virtual network can be part of two mesh configurations.
    * A virtual network can be part of a mesh topology and a network group that has direct connectivity enabled in a hub-and-spoke topology.
    * A virtual network can be part of two network groups with direct connectivity enabled in the same or different hub-and-spoke configuration.

* You can have virtual networks with overlapping IP spaces in the same connected group. However, communication to an overlapped IP address will be dropped.

* The maximum number of IP prefixes in all admin rules combined is 1000. 

* The maximum number of admin rules in one level of Azure Virtual Network Manager is 100. 

* Azure Virtual Network Manager doesn't have cross-tenant support in the public preview.

## Next steps

Create an [Azure Virtual Network Manager](create-virtual-network-manager-portal.md) instance using the Azure portal.
