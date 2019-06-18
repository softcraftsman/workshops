# Hands on Azure Fundamentals Lab

## Introduction



## Pre-requisites

If you don't have an Azure subscription, create a [free account] now. (https://azure.microsoft.com/en-us/free/)

[Sign in] to the Azure portal.

## Syllabus

- Overview of Subscription, Resource Group, and ACL heirarchy
- Create a Storage Account
- Overiew of Virtual Networks
- Create a Virtual Machine
- Create a Network Security Group
- Create a File Share
- Backup VM

## Create a Storage Account

Using the Portal, create a V2 storage account in South Central US

1) Using the portal go to Create a Resource
2) Search for Storage Account
3) Provide account name, Location = South Central, Standard Performance, Replication LRS, Hot Tier.

## Setup Cloud Shell

Using the storage account created in the last section, setup the cloud shell.

1) Navigate to shell.azure.com
2) Select Advanced Settings
3) Select your Resource Group
4) Click on Use Existing Storage Account
5) Type in cloudshell in the fileshare
6) Create storage

## Setup Virtual Networks for the Class [Instructor]
Every virtual machine needs to sit within a virtual network. Each virtual network is specific to a region, so we need to create a vnet for each region.

1) Create a Resouce Group for the Networks - ITS-NETWORKS
-   show how each network can be in a different region, yet in the same resource group.
2) Create a vnet in each region
```
az network vnet create --name vnet-eus --resource-group ITS-NETWORKS --subnet-name FrontEnd 
az network vnet create --name vnet-eus2 --resource-group ITS-NETWORKS --subnet-name FrontEnd 
az network vnet create --name vnet-wus --resource-group ITS-NETWORKS --subnet-name FrontEnd 
az network vnet create --name vnet-wus2 --resource-group ITS-NETWORKS --subnet-name FrontEnd 
az network vnet create --name vnet-cus --resource-group ITS-NETWORKS --subnet-name FrontEnd 
```

3) Peer the vnets
* `az network vnet peering create -g ITS-NETWORKS --vnet-name vnet-eus -n EUS-HUB --remove-vnet CUS-HUB-vNET`
* `az network vnet peering create -g ITS-NETWORKS --vnet-name CUS-HUB-vNET -n EUS-HUB --remove-vnet vnet-eus`

## Create a Virtual Machine

```
az vm image list
```

```
az vm create 
    -g msft-johnbrown 
    -n jsb2-demo
    --image UbuntuLTS 
    --size Standard_DS2_v3
    --admin-username brownjohn 
    --admin-password Azure4Research! 
    --vnet msft-demo
```
