## Directory Enumeration
```
gobuster dir -u http://10.129.228.112:50000/ -w /usr/share/wordlists/dirb/common.txt -c -ic
```
If nothing was found with the common.txt dictionary please try with big.txt or with /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt
## Page Fuzzing
### Extension Fuzzing
Determine which type of pages the website uses, like .html, .aspx, .php
We use the wordlist web-extensions.txt
```
ffuf -w /opt/useful/seclists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://SERVER_IP:PORT/blog/indexFUZZ
```
### Page Fuzzing
```
ffuf -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt -u http://SERVER_IP:PORT/blog/FUZZ.php
```

## Parameter Fuzzing
```
ffuf -w /home/sara/Documents/Wordlists/burp-parameter-names.txt  -u http://10.129.96.75/firewall.php?FUZZ=test -c
```
## Vhost Fuzzing
```
ffuf -w /home/sara/Documents/HTB/HTBAcademy/Attacking_Common_Applications/subdomains-top1million-5000.txt -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb'
```

https://github.com/danielmiessler/SecLists/blob/master/Discovery/DNS/subdomains-top1million-5000.txt

```
curl -s -O https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/Common-Credentials/2023-200_most_used_passwords.txt
```

