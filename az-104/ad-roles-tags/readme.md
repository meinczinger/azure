# Managing azure roles & tags

## Azure Role-based access control (RBAC)

It is a way to delegate access to others. There are built-in roles and custom roles can be created.

Examples of built-in roles:
- Owner: Full resource management control
- Contributor: Resource control other than granting RBAC access
- Reader: Read-only access
- CDN Endpoint reader: Read only access to content distribution network endpoints
- Cost Management Contributor: Read and write Azure cost configurations including budgets
- Virtual machine administrator login: Read VMs in the portal, login with admin credentials

Custom roles can be created from a JSON definition.

Roles can be assigned to:
- Users
- Groups
- Service principles (~ service account)
- Managed identities

Roles can be assigned on multiple levels:
- Subsription
- Resource group
- Resource

E.g. a role assigned to a group on the subscription level gets inherited to resource groups and resources within the given subsription.

## Azure AD Role CLI assignment

E.g. on the resource group level:

```
az role assigment create --role "SQL DB Contributor" --assigne bla@bla --resource-group Rg1
```

View the role assignment:
```
az role assignment list --resource-group Rg1
```

## Powershell

```
New-AzRoleAssignment -SignInName bla@bla -RoleDefinitionName "SQL DB Contributor" -ResourceGroupName Rg1
```

```
Get-AzRoleAssignment -ResourceGroupName Rg1 -SignInName bla@bla
```

```
Remove-AzRoleAssignment -SignInName bla@bla -RoleDefinitionName "SQL DB Contributor" -ResourceGroupName Rg1
```

## Custom roles

Can be defined in a JSON.

- Actions: a list of actions/permissions
- NotActions: list of restrictions

```
new-azroledefinition -inputfile something.json
```

This can be used to assign to resources based on its name, same as built-in roles.

## Resource locking

Resource lock can be set on the subscription, on the resource group or the resource level.

Resource lock levels:
- Read-only
- Prevent deletion

## Resource locks via the CLI

E.g. on the resource group level:

```
az lock create --name Lock2 --resource-group Rg1 --lock-type readonly
```

``` 
az lock list
```

## Powershell

```
get-azresourcelock
```

## Resource locking and templates

ARM (Azure Resource Management) templates can contain locks.

## Resource tagging

It's metadata, things like project, department, test/prod, cost center etc., it's a key-value pair.

Policies can be used to enforce tagging. Max. 50 tags per resource. 

Resource group tags are not inheritable!

## CLI
```
az tag list | grep "tagName"
```

```
az tag create --namne DeptId
az tag add-value --name DeptId --value 1234
```



