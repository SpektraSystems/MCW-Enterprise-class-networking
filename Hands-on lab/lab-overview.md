# Enterprise-class networking in Azure hands-on lab step-by-step

## Abstract and learning objectives

In this hands-on lab, you will setup and configure virtual networks in a secure hub-and-spoke design. You will also learn how to secure virtual networks by implementing Azure Firewall, network security groups and application security groups, as well as configure route tables on the subnets in your virtual network. Additionally, you will set up access to the virtual network via a jump box and provision a site-to-site VPN connection from another virtual network, providing emulation of hybrid connectivity from an on-premises environment.

At the end of this hands-on lab, you will be better able to configure Azure networking components.

## Overview

You have been asked by Woodgrove Financial Services to provision a proof of concept deployment that will be used by the Woodgrove team to gain familiarity with a complex Virtual Networking deployment, including all of the components that enable the solution. Specifically, the Woodgrove team will be learning:

-   How to bypass system routing to accomplish custom routing scenarios.

-   How to capitalize on load balancers to distribute load and ensure service availability.

-   How to implement Azure Firewall to control hybrid and cross-virtual network traffic flow based on policies.

-   How to implement a combination of Network Security Groups (NSGs) and Application Security Groups (ASGs) to control traffic flow within virtual networks.

-   How to monitor network traffic for proper route configuration and trouble shooting.

The result of this proof of concept will be an environment resembling this diagram:

## Solution architecture

![This image represents an entire overview of an environment for the result of this proof of concept.](images/Hands-onlabstep-by-step-Enterprise-classnetworkinginAzureimages/media/image200.png "Solution Architecture")

## Requirements

You must have a working Azure subscription to carry out this hands-on lab step-by-step.

## Help references

|    |            |
|----------|:-------------:|
| **Description** | **Links** |
| IP Addressing and Subnetting for New Users   | http://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html  |
| CIDR / VLSM Supernet Calculator  | <http://www.subnet-calculator.com/cidr.php>  |
| Virtual Network documentation  | <https://azure.microsoft.com/en-us/documentation/services/virtual-network/>  |
| Network Security Group documentation  | <https://azure.microsoft.com/en-us/documentation/articles/virtual-networks-nsg/>  |
| IP addresses in Azure      |  https://azure.microsoft.com/en-us/documentation/articles/virtual-network-ip-addresses-overview-arm/ |
| User-Defined Routing and IP Forwarding   | <https://azure.microsoft.com/en-us/documentation/articles/virtual-networks-udr-overview/>  |
| Load Balancer       | <https://azure.microsoft.com/en-us/documentation/articles/load-balancer-overview/>  |
| Implementing a DMZ between Azure and your on-premises data center    |  <https://azure.microsoft.com/en-us/documentation/articles/guidance-iaas-ra-secure-vnet-hybrid/>  |
| What is Azure Firewall?    |  <https://docs.microsoft.com/en-us/azure/firewall/overview/>  |
| Security groups    |  <https://docs.microsoft.com/en-us/azure/virtual-network/security-overview/>  |

**Contents**

<!-- TOC -->

- Enterprise-class networking in Azure hands-on lab step-by-step
  - Abstract and learning objectives](#abstract-and-learning-objectives
  - Overview
  - Solution architecture
  - Requirements
  - Help references
  - Exercise 1: Create a Virtual Network and provision subnets
    - Task 1: Create a Virtual Network
    - Task 2: Configure subnets
  - Exercise 2: Create a Network Monitoring Solution
    - Task 1: Create a Log Analytics Workspace
    - Task 2: Configure Network Watcher
  - Exercise 3: Create route tables with required routes
    - Task 1: Create route tables
    - Task 2: Add routes to each route table
  - Exercise 4: Configure n-tier application and validate functionality
    - Task 1: Create a load balancer to distribute load between the web servers
    - Task 2: Configure the load balancer
  - Exercise 5: Build the management station
    - Task 1: Build the management VM
  - Exercise 6: Virtual Network Peering
    - Task 1: Configure VNet peering WGVNet1 to WGVNet2 and Vice Versa
  - Exercise 7: Provision and configure Azure firewall solution
    - Task 1: Provision the Azure firewall](#task-1-provision-the-azure-firewall
    - Task 2: Create Firewall Rules
    - Task 3: Associate route tables to subnets](#task-3-associate-route-tables-to-subnets)
  - Exercise 8: Configure Site-to-Site connectivity
    - Task 1: Create OnPrem Virtual Network
    - Task 2: Configure gateway subnets for on premise Virtual Network
    - Task 3: Create the first gateway
    - Task 4: Create the second gateway
    - Task 5: Connect the gateways
  - Exercise 9: Configure Network Security Groups and Application Security Groups
    - Task 1: Create application security groups
    - Task 2: Configure application security groups
    - Task 3: Create network security group
  - Exercise 10: Validate connectivity from 'on-premises' to Azure
    - Task 1: Create a virtual machine to validate connectivity
    - Task 2: Configure routing for simulated 'on-premises' to Azure traffic
  - Exercise 11: Using Network Watcher to Test and Validate Connectivity
    - Task 1: Configuring the Storage Account for the NSG Flow Logs](#task-1-configuring-the-storage-account-for-the-nsg-flow-logs)
    - Task 2: Configuring Diagnostic Logs
    - Task 3: Reviewing Network Traffic
    - Task 4: Network Connection Troubleshooting

<!-- /TOC -->

