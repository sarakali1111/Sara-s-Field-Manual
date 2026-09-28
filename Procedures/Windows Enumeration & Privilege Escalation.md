##### Enumeration
* Enumerate users and groups
* [x] List local users
* [x] List local groups
* Check membership of interesting groups
 - [ ] Local Administrator
 - [ ] Remote Desktop Users (RDP access)
 - [ ] Remote Management Users (WinRM access)
* Enumerate operating system information
 - [ ] Windows version and build number
 - [ ] Architecture (32 or 64 bit)
* Enumerate network information
 - [ ] IP addresses and network interfaces
 - [ ] List active connections and listening ports
* Enumerate program and processes information
 - [ ] List all installed applications and services
 - [ ] Look at processes for any running applications that are not installed
 - [ ] Enumerate security features

##### Privilege Escalation
- [ ] Try WinPEAS
- [ ] Run PowerUp
- [ ] Run PrivescCheck
* Look for vulnerable services
 - [ ] Services with weak executable permissions.
 - [ ] Services where we can alter the executable path.
 - [ ] Unquoted service paths.
 - [ ] Services prone to DLL hijacking.
 - [ ] Check if AlwaysInstallElevated is enabled.
 - [ ] Search for CVEs in installed programs.
 - [ ] See if there are known exploits for the Windows version.

##### Per User 
 - [x] Check user’s privileges
 - [x] Check which groups user belongs to
 - [ ] Look for secrets in shell environment variables
 -  Hunt for credentials
 - [ ] Check for Unattend.xml
 - [ ] Check in AppData\Roaming\Microsoft\Credentials
 - [ ] Look for Unquoted Service Paths
 - [ ] Look for exploitable Scheduled Tasks
 - [ ] Try planting malicious SCF and LINK files on writeable SMB shares.
