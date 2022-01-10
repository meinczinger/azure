# Azure app service & batch

## Overview

Deploy web apps as a managed service

Can be:
- code based
- or docker based

## Azure App service planning

### Web app

- Custom DNS domains
- Deployment slots (staging)
- TSL settings (transport layer security)
- Vertical scaling
- Horizontal scaling
- WebJobs (script to perform maintanence)

### App service plan

- Determines wihch resources are available to a web app
- Can support multiple web apps
- View performance metrics
- File-system usage per app

## App service plan pricing tiers

- Azure compute units (ACUs) - CPU performance
- Dev/Test
- Produciton
- Isolated

## Runtime stack support

- .NET, ASP.Net
- Java
- PHP
- Ruby
- etc.

## Azure Marketplace Appa

Existing apps, which can be re-used.

## Azure App service management

- Portal
- ARM template 
- CLI/PowerShell
- Microsoft Visual Studio or other IDE


## Code Web App Deployment

Create a resource of the type 'Web App'. It needs to be linked to an app service plan.

The underlying OS cannot be selected/influenced.

Monitoring can be enabled by enabling Application Insights.

Authentication provider can be set.

Database connection string can be set.

## Docker web app deployment

Just needs an image, the app runtime needs to be in the image.

It can be a single container or a docker-compose.

The Azure container regisgtry has to be provided (or some other container registry).

## App services custom domains

There is a default DNS suffix. A custom DNS name can be set, Azure validates that you really own the name.

## Service plan

It has a size in ACUs (Azure compute units)

## App service TLS bindings

A key vault is required and a certificate needs to be created inside.

On the Web app, go to TLS/SSL settings, pick Private key certificate and import the one from the vault. Then go to Custom domains and add binding (link the domain with the certificate)

## App service deployment slots

Choose an existing web app and select Deployment slots, there is a default one called Production. Another one can be added e.g. for Testing, the app settings can be cloned when creating the second slot.

A different dns name is used for the second slot.

Slots can be swapped, e.g. after testing is done, the testing slot can become the production slot - without downtime!

## App service scaling

Done on the app servic plan level. Scale up and scale out are both possible.

For scale out, can be done manually (increasing the number of underlying VMs) or automatically (baed on the metric it would add VM nodes, with some min and max amount of VMs).

## App service backup

Can be done for a web app. A storage account has to be selected and a container has be created there. A schedule can be set up. A backup frequency has to be done (once a day). The Retention period has to be defined in days. Kepp at least one backup can be selected. DB backup can be included.

The backup can be triggered manually.

## Azure batch

It is used for automation and job scheduling.

- Requires an azure batch account
- Pool - OS details for the VMs
- Job creation and association with a pool

Azure batch workflow:
- Upload scrtipts
  - Create job
    - Add job tasks
      - Add job schedule

## Batch account

Is required. Once created, a storage account has to be associcated with it. 

There is an local app called Batch explorer.

Applications - some executable can be added. Supports versioning.

## Batch pools

Defines the VM nodes. Can be fixed size or autoscale.

There can be a start task when the VM joins the pool.

Application package can be selected to be available on the VMs.

## Jobs and schedules

Jobs have to be created, the job is associated with the pool. Inside the job, at least one task needs to be added with the executable, which is in an application package. The application package is associcated with the job as well.

Job schedules are done separatly, after the job is created.

## Azure container solutions

AKS

## Azcure container instance

Can be used for a single container.