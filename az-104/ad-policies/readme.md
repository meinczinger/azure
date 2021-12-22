# Azure policies

## Azure policies overview

They are about controlling access to azure resources.

Built-in or custom policies can be used, the policy is technically a json file.

Policies are more granular then RBAC (Role based access control).

Policies can accept parameter values, this ensures reusability.

Azure policy effects:
- Audit
- AuditIfNotExists
- DeployIfNotExists
- Deny

Azure policy initiatives is grouping policies:
- Policies are organized into groups
- The policy groups are assigned

Example: 

Harden regional Azure resources
- Ensure VM disk encryption is enabled
- Ensure endpoint protection is enabled

## Policy assignment via the portal

Policy -> Definitions lists the existing (Built-in and custom) policies.

Policies can be set on the subscription, a management group level or a resource group.

Exclusions can be created, where the policy will not apply.

The compliance shows the status of the policies.

## Policy assignment with the cli and powershell

az policy definition list

get-azpolicydefinition

## Custom policies

Policy -> Definitions -> Add policy definition. The policy rule needs to be defined in JSON.

## Policy compliance

Policies can be used not just for enforcing rules, but as well for compliance. Compliance provides reports. E.g. after a policy gets assigned to existing resources, it will take time before all resources are checked, the complience report will show potential issues/defenders.

## Policy remediation

Remediation tasks can be created to handle non-compliance.