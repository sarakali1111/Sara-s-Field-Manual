## Enum4linux
Without valid credentials - anonymous enumeration.
```
enum4linux-ng 10.129.95.210 -U | grep 'username:' | awk '{print $2}' > users.txt
```

Get-ADPrincipalGroupMembership -Identity "Username" | Select-Object Name, GroupCategory, GroupScope

## Enumerate users by bruteforcing RID
```
sudo nxc smb manager.htb -u 'guest' -p '' --rid-brute
```

## LDAP
```
ldapsearch -H ldap://windcorp.htb -b "dc=windcorp,dc=htb" > ldap.out
```

```
grep -i samaccountname ldap.out |awk '{print $2}'|sort -u|grep -v \$
```
