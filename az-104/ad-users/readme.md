# Microsoft Azure Administrator - Manage Azure Users

## Overview 

Azure Active Directory (Azure AD)

AD instance in the cloud, no need to install anything - it provides a centralized identity provider. It can contain:

- Users
- Groups
- Applications
- Security principals (to ensure that software components have the necessary permissions to cloud resources)

AAD can be linked as well to on-prem AD.

Identity Access Management (IAM) is about authentication and authorization.

Authenticaiton is the the proof of identity, can be:

- Single-factor (e.g. username and password)
- Multi-factor (e.g. username, password and smartcard)

Authorization is the controlled access to resources, $after$ a successful authentication. It is achieved by assigning permissions or policies to groups.

RBAC - Role based access control.

Conditional access - policies are used to check before access is allowed.

Access reviews - can be scheduled regularly to check whether some permissions should be removed as they may be not needed anymore.

Privileged identity management (PIM) - only provide admin access to users if they really need it.

## Azure AD and the portal

An Azure AD tenent is essentially an instance of AD in the cloud. It can have one or more Azure subscriptions associated with it.

## Azure AD and the CLI

``` 
az account list

[
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "673d6a88-944b-476f-a35e-5f502bb15601",
    "id": "f3bbc222-205d-4370-ba2c-c4f831917a85",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Azure subscription 1",
    "state": "Enabled",
    "tenantId": "673d6a88-944b-476f-a35e-5f502bb15601",
    "user": {
      "cloudShellID": true,
      "name": "live.com#meinczinger@gmail.com",
      "type": "user"
    }
  }
]
```

```
az ad -h

Group
    az ad : Manage Azure Active Directory Graph entities needed for Role Based Access Control.

Subgroups:
    app            : Manage applications with AAD Graph.
    group          : Manage Azure Active Directory groups.
    signed-in-user : Show graph information about current signed-in user in CLI.
    sp             : Manage Azure Active Directory service principals for automation authentication.
    user           : Manage Azure Active Directory users and user authentication.

Examples
    Delete a group from the directory. (autogenerated)
        az ad group delete --group MyGroupDisplayName


    Create a service principal. (autogenerated)
        az ad sp create --id 00000000-0000-0000-0000-00000000000000000


    update an application's group membership claims to "All" (autogenerated)
        az ad app update --id 00000000-0000-0000-0000-00000000000000000 --set
        groupMembershipClaims=All


    Create a web application, web API or native application. (autogenerated)
        az ad app create --available-to-other-tenants true --display-name my-native --password
        {password}

```

To filter a complex result (alternative to grep), the --query option can be used:

```
az ad signed-in-user show --query userType

"Member"
```

## Azure AD Users and the portal

Create a user via the portal and test it via account.activedirectory.windowsazure.com

## Azure AD and the CLI

First check the new user which was created via the portal:

```
az ad user list --query [].displayName

[
  "Meinczinger",
  "Tibor Meinczinger"
]
```

Now let's delete this user:
```
First get the userPrincipalName

az ad user list --query [].userPrincipalName

Then delete the newly created user:

az ad user delete --id "meinczin2@meinczingergmail.onmicrosoft.com"
```

Now create a new user:
```
az ad user create --display-name "Test account" --user-principal-name meinczinger2@meinczingergmail.onmicrosoft.com --password "Humo4313"
```

## Azure guest users

Via the portal: AD -> Users -> Invite user

## Azure bulk user create

Via the portal: AD -> Users -> Bulk create or Bulk invite, the input is a CSV file

## Multi-factor authentication

Combines two or more categories:
 
- something you know + something you have
- something you know + something you are
- something you have + something you do

The Microsoft authenticator can be used as well.


## Azure user MFA

Can be easily done via the portal: AD -> USer -> Per-user MFA

## Azure MFA Block

Via Portal: AD -> Security -> MFA -> Block/unblock users

E.g. if user looses his smart phone and does not have the authenticator app.

## Azure self-service password reset

AD -> Users -> Password reset

In case MFA is set up, it would let you reset the password after authenticating with e.g. the authenticator app

## Deleting users

If a user gets deleted, it gets deleted logically and will be deleted permanently after 30 days. While logically deleted, the user can be restored. Group membership is also restored.

## Azure AD User license assignment

AD -> Users -> Select user -> Licenses -> Assignments

E.g. O365 license can be added

Usage location has to be set in order to assign a license as licensing can be different from location to location.

## Banned password lists

A list of passwords users are not allowed to use.

AD -> Security -> Authentications methods -> Password protection

1000 passwords can be added to the list

## Azure AD licensed features

Licenses on AD level: AD -> Licenses -> Managed your purchased licenses. After that a license can be assigned to users.


## Subscription assignment

Change the tenant of a subscription: Subscriptions -> Choose subscription -> Change directory

## Smart lockout

AD -> Security -> Authentiaiton methods -> Password protection -> 

- Custom smart lockout threshold: the number of password attempts
- Lockout duration in seconds: after how long the user can try again