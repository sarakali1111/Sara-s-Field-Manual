Anonymous login
```
nxc smb <target> -u '' -p '' --shares
```

Guest login
```
nxc smb <target> -u 'guest' -p '' --shares
```

Anonymous login with 'anonymous' username
```
nxc smb <target> -u 'anonymous' -p '' --shares
```

### Smbclient
```
smbclient -L <target-IP> -U username%password
```
Connect to a valid share with username and password
```
smbclient //<target>/<share$> -U username%password
```


