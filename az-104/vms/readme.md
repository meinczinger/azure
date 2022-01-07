# Managing azure virtual machines

IaaS - you crete the VM
Managed - Azure cretas the VMs

IaaS:
- Which OS image to use
- Additional software on top of the OS
- Resource group and location
- Sizing: vCPUs, RAM, data disks, IOPS
- High availibility
- User credentials

## Azure VM User Credentials

Windows:
- USername
- Password
- RDP (port 3389)

Linux:
- Password-based
- SSH public key-based
- SSH (port 22)

Disk sizing:
- Standard HDD (for infrequently accessed data)
- Standard SSD (tesing and non-critical usage)
- Premium SSD (for production and peak performance usage)
- Ultra SSD (Highest performance, suitable for intensive database workloads)

Networking:
- Network security group
- VNet and subnet
- Network interfaces
- Public IP address
- Load balancing

VM scaling:
- Horizontal (adding VMs)
- Vertical (adding more CPU, RAM etc.)


Spot instance: for batch processing, not running all the time.

## Template deployments

ARM is like CloudFormation.

A manually created VM can be used to save it as a template.

## VM Redeployment

It has downtime, can be done if there are issues with the VM.

## Just-in time VM access

Ports are only open when management needs to be done.

JIT access can be requested by admins, VMs need to be configured for JIT access. A time range is specified when requesting.

## VM move

Move from one resource group to another within the same region/location.

## VHD deployment templates

Existing VHD files can be used to create templates.

## VM re-sizing

Vertical scaling.

For running VMs, resizing will cause down-time.

## VM Data disks

Managed disks can be cretead and then attached to a VM.

## Azure key vault

Store for secrets. Keys can be generated or imported. For the keys, activation and expiry date can be set.

PKI certificates can be created as well.

Access policies control who/what can access the secrets.

## VM Disk encryption

OS and data disks can be encrypted. A key from the Azure Key Vault can be used to encrypt. An access policy for data encryption is required in the key vault.

There is downtime for existing disks.