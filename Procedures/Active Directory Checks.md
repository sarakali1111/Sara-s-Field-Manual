## Live Host Enumeration
- [ ]  Conduct a ping sweep on the IP range
- [ ]  Use NetExec on the IP range (better information)
- [ ]  Use Responder to catch IP addresses
## User Enumeration
- [x]  Attempt to get user list via SMB Null Authentication
- [x]  Attempt to get user list via LDAP Anonymous Bind
- [x]  Attempt to get user list via RPCClient
- [x]  Attempt to get user list via RID brute-forcing
- [x]  Attempt to get user list via Kerbruting
## Get Foothold
- [x]  Find Kerberoastable users from the user list
- [x]  Find ASREProastable users from the user list
- [x]  Use Responder to catch credential hashes
- [x]  Try SMB Null Authentication to spider through SMB shares looking for credentials
- [ ]  Get `SYSTEM` / `root` on Domain connected host to get a Computer account
- [ ]  As a last resource, try password spraying with the user list
## Attacks
- [ ]  Use SharpHound to collect data to feed BloodHound
- [ ]  Check compromised hosts on BloodHound for outbound attack paths
- [ ]  Use NetExec to check for command execution via SMB, WinRM, and RDP for each compromised user.
- [ ]  Kerberoast
- [ ]  ASREProast
- [ ]  Look for credentials in GPOs (`gpp_password`, `autologin`)
- [ ]  For each compromised user, spider through readable SMB shares for sensitive information
- [ ]  For each compromised user, conduct SMB Hash Theft attacks on writable SMB shares
- [ ]  Look for passwords in user’s description fields
- [ ]  Check the DC’s SYSVOL SMB share for scripts containing credentials
- [ ]  [NoPac](https://github.com/cube0x0/CVE-2021-1675)
- [ ]  [PrintNightmare](https://github.com/m8sec/CVE-2021-34527)
- [ ]  [PetitPotam](https://github.com/topotam/PetitPotam)
- [ ]  Try compromised local administrator hashes on other hosts
- [ ]  Try Responder on different hosts
- [ ]  Look for users with the `PASSWD_NOTREQD` field
- [ ]  Password spray using previously found passwords



## Prime Rules[](https://divyeshs-organization-1.gitbook.io/cpts-cheatsheet/methodology/active-directory-methodology#prime-rules)

1. **Enumerate before you exploit.** Every AD box has a specific weak-cred / ACL / delegation path — find it before running exploits.
    
2. **BloodHound is your map** — collect early with any working cred, re-collect after every credential gain.
    
3. **Password reuse across every user, every service, every box** — highest-ROI move in AD.
    
4. **Timing matters** — Kerberos rejects tickets outside the 5-minute skew window. `sudo ntpdate <DC_IP>` before every ticket op.
    
5. **Cleanup is mandatory** — every SPN plant, every group add, every RBCD delegation must be reverted for OpSec (and OSCP report quality).
    
6. **Responder poisoning is EXAM-BANNED** — only analyse-only `-A` is EXAM-OK for LLMNR observation.



## The Attack Chain — Canonical Order

AskCopy

```
Zero creds
   ↓
enum4linux-ng / SAMR RID brute / anon LDAP → user list
   ↓
kerbrute userenum → valid usernames
   ↓
AS-REP roast (no-preauth users) OR spray weak/default passwords OR LAPS (if ExtendedRight) OR anon share cred leak
   ↓
FIRST CREDENTIAL
   ↓
BloodHound collection (bloodhound-ce-python -c All)
   ↓
Description / info field grep, LAPS check, gMSA dump, mailbox reads
   ↓
Kerberoast (offline crack) OR ACL abuse (ForceChangePassword / GenericAll)
   ↓
BloodHound path to next principal
   ↓
Lateral: PtH via nxc smb, PtT via kinit ccache, WinRM (evil-winrm), PsExec (impacket)
   ↓
BloodHound recollect — mark every new cred as Owned
   ↓
Path to DA revealed (usually via DCSync ExtendedRight → secretsdump)
   ↓
DA
   ↓
DCSync krbtgt → golden ticket for persistence (mandatory cleanup)
```