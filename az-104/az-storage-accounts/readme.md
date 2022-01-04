# Managing azure storage accounts

## Overview

Storage accounts can accomodate:
- Blobs
- Storage queueus
- File shares (like SMB)
- Tables (no-sql storage [key-value])

It supports:
- Replication (LRS, GRS [Geo-Replication], RA-GRS [Read-access GRS])
- Static website
- Azure CDN (Content delivery network)
- Azure search (indexing)
- Blob lifecycle management (e.g. auto-archive after 60 days)

Azure Storage Account Hardening:
- RBAC Roles
- Stroge account keys (used for programmatic access)
- Shared access signature (limited access to content in the storage account, it can have an expiration date)
- Access policies
- Custom encryption keys

## Manage storage accounts with the cli

```
az storage account create -n storage_acct_name -g Rg1 -l canadaeast --sku Standard_LRS
```

```
az storage account list
```

## Powershell

```
new-azstorageaccount -resourcegroupname Rg1 -name storage_acct_name -location canadaeast -skuname 'standard_lrs"
```

```
get-azstorageaccount
```

```
get-azstorageaccountkey -resourcegroupname Rg1 -accountname storage_acc_name
```

```
get-azstorageaccount -resourcegroupname Rg1 -accountname storage_acc_name | select accesstier
```

## Storage account network access

On the portal: Storage account -> Firewall and virtual networks:

- All networks (accessible from the internet)
- Select networks (Virtual network can be selected, additionally public ip addresses or ranges can be whitelisted)



## Container

Containers can be created inside a storage account.

Files/objects can be added to a container.

Acquire lease - the object gets locked.

## Manage blobs via the cli

```
az storage account keys list --account-name acct_name --resource-group Rg1
```

```
az storage container create --name eastdata --account-name acct_name --account-key key
```

```
az storage blob upload --container-name cont_name --name blob_name --file local_file --account-name acct_name --account-key key
```

## Powershell

```
new-azstoragecontainer -name "some_container" -context storage_account
```

```
set-azstorageblobcontent -file some_local_file -container "some_container" -blob  blob_name -context=storage_account
```

## AzCopy

Works to, from and between storage accounts.

```
azcopy make "url of a new container"
```

```
azcopy copy local_file url_of_container
```

## Blob lifecycle management

E.g. move unused data into cool storage to save cost.

Storage acconts -> select account -> Lifecycle management -> Add a rule

- Move blob to cool storage after X days
- Move blob to archive storage after X days
- Delete blob or snapshots certain days after the blob was modified/created

A filter set specifies restrictions on which container or blob the rule should be applied.

## Blob container access levels

- Private (no anonymous access)
- Blob (anonymous read access for blobs only)
- Container (anonymous read access for containers and blobs)

## Storage account queues

Queues can be created within a storage account. Messages put intot the queue have an expiration time.

Access policy can be created for queues.

## Storage account AD authentication

Role assignement can be added to storage accounts.

## Storage account access keys

Each account has two keys so that the keys can be refreshed periodically.

## Shared access signatures

SAS is a way to allow limited access to a storage account opposed to access keys, which provide full access to the storage account.

E.g. SAS can be created to provide read-only access only to blobs and expiration time can be set. Returns:
 - connectiont string
 - SAS token
 - BLOB Service SAS URL

## Storage account replication

- Locally redundant storage (LRS) - three copies of data within an Azure location
- Geo-redundant storage (GRS) - failover needs to be initiated
- Read-access GRS - automatic failover


## Azure storage explorer connectivity

Connection by:
- AD
- Connection string
- Shared access signature
- Storage account name and key

## Storage account blob soft delete

Objects don't get physically deleted, just logically and so they can be restored. By default it is disabled. If enabled, there is a retention policy, e.g. 7 days.

## Storage account encryption

"Encryption at rest"

It is enabled by default and uses keys from Microsoft. One can have his own keys, the key vault can be used to manage the keys.

## BLOB SAS Token

## Azure blob types

- Block (for smaller files)
- Append (e.g. log files)
- Page (large files to support random access)

Azure files are shared folders, OS must support SMB v3.0

Azure table storage  is no-sql based, unstructured schema (key-value store).

## File shares

File share is like a storage container, but can be mounted remotely.

```
az storage share create --account-name store_acct --account-key key --name share_name --quota 5 
```

```
New-AzStorageShare -name share_name -context storage_account
```

## Azure file synch

Azure files share can be synchronized with an on-prem file server.