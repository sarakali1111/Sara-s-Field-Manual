### NetExec
```
nxc smb <DC> -u UserNAme -p 'PASSWORDHERE' --pass-pol
```
### SMB NULL Session
```
nxc smb <dc> --pass-pol
```
### PowerView
```
Get-DomainPolicy
```
### CMD
```
net accounts
```
### LDAP Anonymous Bind
```
ldapsearch -H ldap://<dc> -x -b "<domain-dn>" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength
```

### RPC
```
rpcclient -U "" -N <IP>
```

```
rpcclient $> querydominfo
```


