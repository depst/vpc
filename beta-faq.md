---

copyright:
  years: 2018
lastupdated: "2018-06-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# FAQs

## What are the costs for participating in this Beta release program, if any, beyond my usual account costs?

IBM Cloud VPC and the related network and compute services are free during the Beta release phase, except for the bandwidth used through a public gateway, for which bandwidth charges may apply.

## During Floating IP assignment, the customer must specify the vNIC of VSI, is that correct?

Yes, and in fact, it must be the primary network interface of a server.

However, if we add an "address" resource in the API under the networking area, we could very well change the association of the floating IP to the address rather than the interface.

## Can vNIC have both floating IP and private IP?
 
Yes.

## In the UI, there is only a ”toggle" for each subnet to attach or detach to or from the Public Gateway. Who creates the PGW? Will the PGW default to be ready when the customer wants to attach the subnet to the PGW in the UI?

The PGW needs to be created explicitly through the API as it stands now, because the API requires an explicit association of a subnet to a particular public gateway.

## Imagine that VSI1 has only vNIC1 and it is attached to Subnet1. Subnet1 is attached to a Public Gateway (PGW). Can the customer still assign a Floating IP to VSI1?

Yes, a server can be on a subnet attached to a public gateway and also have a floating IP. The assignment of floating IP to a VSI is not related to whether there is a public gateway attached to the subnet. A floating IP associated to a VSI will take precedence over the public gateway attached to the subnet.

## VSI1 has 2 vNICs, called vNIC1 and vNIC2. Can these two vNICs be attached to the same subnet? 
 
Yes, there is no limitation on having multiple network interfaces on the same server attached to the same subnet. However, I don't know when multiple NICs on a VSI will be supported.

## Can a VSI be created without a subnet - just with Floating IP?

No.

## Can a VSI attached to multiple VPCs?

No.

## Can a subnet size be changed after it is created?

No.

## During the PGW creation, does customer need to reserve the FIP, or does the system automatically reserve the FIP? Will customer see that Floating IP when he queries all of his Floating IPs?

As the spec is currently defined, RIAS automatically creates a floating IP along with the public gateway if an existing floating IP is not specified. And yes, that floating IP will show up in the list.

A Floating IP is created if none is provided. Yes, it will show up in the list of floating IPs. As it stands now, the PGW would have a floating IP that would be charged. We could have a policy to not bill for floating IPs attached to a PGW.


## Who enforces that there must be only 1 Public Gateway per Zone? 

The Regional Infrastructure API Service (RIAS) enforces this limit.

## How does VRF affect my other networking capabilities and my subnets?

Caveats for VLANS and VRF:

* Inter-account VLAN spanning is not allowed in the VRF environment.
* IPSec VPN service is limited.

**Note:** VRF does not prevent SSL or PPTP VPN access, but its behavior changes. Without VRF, one VPN connection is enough to see all servers on your account. With VRF, you can only access resources in the market associated with your VPN. So if you connect to the DAL VPN, you can only connect to DAL servers.
