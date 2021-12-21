# Manage Azure AD Groups and Devices

## Azure AD groups and the portal

AD -> Groups

Group type:

- Dynamic (rules determine whether users are part of the group)
- Assigned (members to the group are added manually)

Groups can be nested: a group can be added to another group.

User can be added to the owners of the group, those will be able to manage the group.

## Azure AD groups and the CLI

``` 
az ad group list

```
```
az ad group create --display-name "Team1" --mail-nickname "Team1"
```

```
az ad group member list -g Team1
```

## Azure AD groups and PowerShell

```
get-command new*group*
get-help new-azadgroup -detail

new-azadgroup -displayname "Team1" -mailnickname "Team1"
get-azadgroup
add-azadgroupmember -memberobjectid=id -targetgroupobjectid=id
get-azadgroupmember -groupobjectid=id
```

O365 type of group can be created as well, again either assigned or dynamic.

If deleted, the Security group will not show up under deleted groups, those get hard deleted. O365 groups get logically deleted and can be restored.

## Azure AD Windwows 10 Device join

AD -> Devices

From a Windows 10, one can connect to that AD, after that the windows 10 device will be listed under AD -> Devices

## Azure AD Device settings

After a windows 10 device connects, it is possible to login to the windows 10 system by Azure AD and cloud resources can be assigned to it.

## Azure AD Device Disable

E.g. if a laptop got stolen or if the laptop should not be able to access cloud-based resources.

## Azure AD Dynamic Groups

Automatic membership of users/devices in groups, based on user/device attributes.

Requires at least an AD Premium P1 license.

Evaluation occurs on user property change.

Licenses can be assigned to dynamic groups.

e.g. 
- user.type -eq "Guest"
- user.comoanyName -ne null
- user.department -eq "IT"
- user.accountEnabled -eq true
- (user.type -eq "Guest") and (user.comoanyName -ne null)
- user.city -in ['Chicago', 'Paris', 'Prague']
- regular expressions can be used as well
- device.OSType = "iPhone"

When creating a dynamic group, one has to choose either Dynamic user or Dynamic device.

## Azure AD Group licence assignment

AD -> Groups -> Select a group -> Licenses -> Assignments

## Azure AD Group ownership

Multiple owners can be added to a group.

## Azure AD Group self-service

AD -> Groups -> Select group -> Settings -> General

Options:
- Owners can manage group membership requests in the Access Panel
- Restrict access to groups in the Access Panel
- etc.

If the first is true, users can request to be added to the group and the owner gets notified and can approve or reject.

## Bulk add and remove of group members

Adding by uploading a csv template.

## Azure AD Android join

On Android, go Settings -> Accounts -> Join work account -> Email address of azure ad account -> Join -> Password

## Dynamic device groups

Membership type is Dynamic device, otherwise the same as Dynamic user

## Conditional access

AD -> Security -> Conditional access -> New policy

- Users/groups need to be selected, for which the condition will apply
- To which cloud apps the condition will apply
- The actual conditions, like Device platforms, Location, Client apps, Device status etc.

Policy status:
- On
- Off
- Report-only




