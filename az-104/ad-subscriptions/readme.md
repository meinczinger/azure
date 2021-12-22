# Azure AD subscriptions and costs

## Subscription

One tenant can have many subscriptions, but one subscription belongs to one tenant only. 
Subscription is mainly for cost management.

Subscriptions have limits like number of storage accounts per region. Some limits can be increased with a customer
suppot request.

Billing occurs per subscription.

Subscription types:

- Pay-as-you-go
- Professional direct support
- Standard support
- Developer support

## CLI

az account list - list the available subscriptions in the account

az account set --subscription "subs name" - sets the context to the subscription, in case there are 
multiple subscriptions

## Powershell

Get-AzSubscription - shows the active subscription and the associated tenant

select-azurermsubscription 'subs name' - set the active subscription

get-azurermcontext - provides subscription and tenant


## Azure management groups

Centralized governance to help to organize subscriptions for policy and compliance reasons.

Root managment group
   |                               |
Management group 1           Management group 2
  |              |                 |
Subs 1       Subs 2           Subs 3


Subscriptions can be grouped and policies can be applied to those groups and those policies will apply to all 
subscription in that group.

Policy -> Assignments -> Assign policy -> Scope -> A management group can be selected

## Azure cost analysis


## Azure budgets

A budget can be created either for an entire subscription or as well for management groups or even for resource groups.

A cost threshold can be set.

Various actions can be triggered: email, sms etc.

## Azure invoices

Subscriptions -> Billing -> Invoices

Invoices can be downloaded in CSV or PDF.

Invoices can be set automatically via email.

## Resource groups

It is a way to organize related resources together, e.g. a resource group for a department or have a resource group for all the components of a web app.

Resource groups are within a subscription and are in a specific region.

Costs are visible per resource group.

Tags can be added to a resource group.

## Manage resource groups via the cli

az group list - lists resource groups

az group create -l region -n name - creates a new resource group

When removing a resource group, all resources inside are deleted as well.

## Manage resource groups with PowerShell

New-AzureRmResourceGroup -name name -location region

get-azurermresourcegroup - lists all the resource groups


## Moving azure resources

Resources can be moved from one resource group to another. It is as well possible to do that in one go for all the resources in one resource group.

## Resource group deployments

The creation (manual or automated) or move of resources.

A resource can be re-deployed (into a new resource group) from a past deployment.
 
## Cost and budget for resource groups

Budget can be set and the cost can be analyzed on the level of resource groups.

## Azure ARM (Azure resource manager) template editor

Provides infra as a code, it's in json.