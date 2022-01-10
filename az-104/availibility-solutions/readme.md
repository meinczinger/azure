# Availibility solutions

## High availibility overview

RTO - Recovery time objective:
- Maximum tolarence for down-time
- Bring systems/data back asap
- Data recovery time
- Time to move operations to alternate site


RPO - Recovery point objective
- Maximum tolerance data loss
- How often data would be taken
- Finance servers VS file servers containing documentation

Disaster recovery plan document:
- Recovery objective
- Scope
- DRP team member responsibilities
- Contact information
- Escalation details

Incident response plan:
- Incident response plan must be in effect before breaches
- Effects of inadequate incident response:
  - Financial
  - Reputation
  - Business partnerships
- Annual review to keep up with changing threats

## Azure availibility zones

One zone can contain one or more data centers.

Availability zones provide:
- High availibility
- One more more data centers
- Fault domains (a RAC)
- Update domains (used for rolling updates)

## VM scale sets

A VM with scaling options, rolling updates etc. Health monitoring can be added.

## Azure load balancer

It deals with:
- Incoming app traffic
- Public load balancer
- Internal load balancer

Load balancer rules:
- Controls traffic distribution
- Session IP affinity (maintain a certain VM for the duration of a session)
- Inbound NAT rules
  - Port forwarding
    - Load balancer IP address
    - Frontend configured port
  - Connectivity to backend systems
    - Virtual machine management
    - Backend port

## Azure application gateway

- Web app load balancer
- HTTP routing decision
- End-to-end SSL/TLS encryption
- SSL/TLS gateway termination
- Autoscaling
- User session affinity
- Up to 100 websites per gateway

Azure application gateway contains a Web Application firewall:
- Based on OWASP rule sets
- Protects against common web app exploits:
  - Cross-site scripting
  - Injection
  - Directory traversal attacks

It supports URL-based routing.

## Internal load balancers

Frontend IP can be static or dynamic. A backend pool has to be added, which has to have VMs or a VM scale set.

Health probes: the load balancers needs to know which VMs are healthy.

Last: a load balancing rule needs to be added. Session persistence can be added.

Optionally inbound NAT rules can be added.

## Public load balancers

Same is internal, just that it has an external ip.


## Load balancer trouble-shooting

- Check backend pool:
  - Is the server/service down?
  - Is there a NSG blocking the traffic from the load balancer?

## Azure site recovery (DR as a Service)

- Fail over and fail back can be enabled between regions.
- Application snapshots can be enabled.

Supported server types:
- On-premise physical servers
- Azure VMs
- VMware VMs
- Microsoft Hyper-V VMs

## Site-to-site recovery

A recovery services vault is a pre-requisite.

E.g. a VM can be creplicated from one location to another. Failover for the VM can be tested by forcing the failover and check that everything works.

## Azure backup

On the servers, which needs backup, the Microsoft Azure Recovery Services Agent (MARS) needs to be installed.

Backup is possible for:
- Azure VMs
- Azure SQL DBs
- Azure File share

On-prem servers can be backed up to Azure.

Backup goes into a services recovery vault.

## Backup policies

It is set on the services recovery vault level. It can:
- set the backup frequency and timing
- for how many days the backups should be kept
- weekly, monthly and yearly backup points can be set (when to take and how long to keep)

## Restore

Can be restored into a new VM or can replace an existing one.

File recovery: will mount the backup as a local drive and from there one can cherry-pick what to restore.

## Azure VM Soft delete

If there is a backup for a server, after the VM gets deleted, it could be restored from the backup.

