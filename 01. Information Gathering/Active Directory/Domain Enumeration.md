#### Discover Modules
```
Get-Module
```

#### Load ActiveDirectory Module
```
Import-Module ActiveDirectory
```

### Get Domain Info
```
Get-ADDomain
```

#### Get-ADUser
```
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
```

#### Checking For Trust Relationships
```
Get-ADTrust -Filter *
```

#### Group Enumeration
```
Get-ADGroup -Filter * | select name
```

#### Detailed Group Info
```
Get-ADGroup -Identity "Backup Operators"
```

### Group Membership
Provides listing of users that belongs to group
```
Get-ADGroupMember -Identity "Backup Operators"
```

## PowerView
```
Import-Module .\PowerView.ps1
```

#### Domain User Information
```
Get-DomainUser -Identity mmorgan -Domain inlanefreight.local | Select-Object -Property name,samaccountname,description,memberof,whencreated,pwdlastset,lastlogontimestamp,accountexpires,admincount,userprincipalname,serviceprincipalname,useraccountcontrol
```

#### Recursive Group Membership
Returns users that belongs to the specified group.
```
Get-DomainGroupMember -Identity "Domain Admins" -Recurse
```

#### Trust Enumeration
```
Get-DomainTrustMapping
```

#### Testing for Local Admin Access
```
Test-AdminAccess -ComputerName ACADEMY-EA-MS01
```

#### Finding Users With SPN Set
```
Get-DomainUser -SPN -Properties samaccountname,ServicePrincipalName
```

