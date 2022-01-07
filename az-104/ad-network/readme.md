# Azure network solutions

## Virtual network (VNet)

It is a virtual network defined in the Azure cloud. IP address range have to be defined.

For DNS servers, either the Azure-provided ones can be used or custom ones.

A VNet can be seen as an extension of an on-prem network, with the help of a VPN.

Each VNet consists of one ore more subnets and each subnet needs its own ip range (which is a subset of the ip range of the VNet).

## Manage network via the cli

Create a vnet with a subnet in it:

```
az network vnet create -g Rg1 -n Vnet1 --address-prefix 11.0.0.0/16 --subnet-name Subnet1 --subnet-prefix 11.0.1.0/24
```

Add a second subnet:
```
az network  vnet subnet create -g Rg1 --vnet-name Vnet1 -n Subnet2 --address-prefix 11.0.2.0/24
```

```
az network list --queryp[].name
```

## Manage network via powershell

```
$subnet = New-AzVirtualNetworkSubnetConfig -Name Subnet1 -AddressPrefix 30.0.1.0/24
New-AzVirtualNetwork -ResourceGroupName Rg1 -Location CanadaEast -Name VNet3 -AddressPrefix 30.0.0.0/16 -Subnet $subnet
```

AzVirtualNetworkSubnetConfig - to add a new subnet to an existing vnet

## IP addresses

Can be dynamic or static. A DNS name is optional.

```
az network public-ip create -g Rg1 -n PubIP1 -l CanadaEast
```

```
new-azpublicipaddress -name Pubip1 -resourcegroupname Rg1 -allocationmethod static -location CanadaEast
```

## Network interfaces

E.g. if a virtual machine needs more network interfaces (one is created when the VM is created).

## Routing 

Route table can be created insite a resource group.

E.g. route traffic to a firewall appliance for inspection.

0.0.0.0/0 default route - applies for all ips in a subnet

'Next hop address' is the routing destination

Can be associcated to a subnet.

The routing table is in a specific location/region.

## Peering

## ExpressRoute

Private dedicated network circuit, links to on-premises networks to Azure. 

The traffic does not go through the internet!

Billing options:
- Metered (pay per GB)
- Unlimited

Multiple cicrcuits can be provisioned

## DNS

Name resolution service.

DNS zones can be hosted in azure, can be private or public.

Azure DNS Options:
- Azure provided
  - Default configuration
  - Resolves public DNS names
  - Virtual machine name resolution with a VNet
  - DNS servers configuration
    - Virtual networks
    - Network interfaces
- Custom
  - virtual machine name resolution acress VNets
  - IaaS virtual machines as AD domain controllers
  - DNS forwarding to Azure is supported

DNS is set within a VNet.

## DNS Zones

Created with a subscription and resource group. 

NS - name server.

SOA - Startup Authority

A new record (dns name -> ip address) can be created inside the DNS Zone.

## Customer DNS servers

For a VNet, a list of custom DNS servers can be provided.

## Network security group

- It's a layer 4 firewall.
- Allow rules
- Deny rules
- Default rules

Can be associated to a:
- VM network adapter (NIC)
- Subnet

The rules of the NSG are important, the order is defined by the priority.

## Security rule trouble-shooting

On VM level, the security group rules are visible. It's important to see those as they can come from the VM and from the subnet level so there can be even conflicts.

## VPN

- Encrypted point-to-point network tunnel
- Point-to-site (p2S) - home office
- Site-to-Site (S2S)
- Express Route

Site-to-Site requires a local network gateway, on Azure side an Azure virtual network gateway is required.

VPN client as well requires n Azure side an Azure virtual network gateway is required.

## Azure virtual WAN

Can connect:

- VPN links to Azure
- Express
- VNet

Two types:
- Standard
  - Point-to-point VPN
  - Site-to-site VPN
  - ExpressRoute
  - Virtual WAN hub interconnectivity
  - VNets

- Basic
  - Site-to-site VPN

## Azure firewall

- Managed service
- Stateful firewall (understand sessions)

It can look at the payload as well, rules can be built based on those.

- Has a static public ip address
- Rules control traffic flow
- Thread intelligence can alert on and deny traffic


Three types of rules:
- network rules (like NSG): protocols, ip adresses, port
- application rules: outbound connectivity, specify fully qualified domain names like *.com, protocol port
- NAT rules:
  - Source network address translation (SNAT)
  - Destination network address translation

It's a separate resource type (within a resource group), has to be associated to a VNet and a subnet with a pre-defined name (AzureFirewallSubnet). It has to have a static public ip address.

On the subnet level, a routing can be created to route the traffic via the firewall.

## Azure bastion

Remote management of VMs (via SSH or RDP).

Like a jump-box to get into VMs, which have private IP addresses. Helps to minimize the amount of VMs, wihch are exposed to the internet.

It requires a specific subnet called AzureBastionSubnet.

