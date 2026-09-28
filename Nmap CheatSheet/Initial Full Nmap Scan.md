First set the target IP address.
```
set target <IP>
```

```
ports=$(nmap -p- --min-rate=1000 -T4 10.10.11.42 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)
```
However, since I use a fish shell the adapted command is:
```
set ports (nmap -p- --min-rate=1000 -T4 10.129.79.224 | grep '^[0-9]' | cut -d '/' -f1 | tr '\n' ',' | sed 's/,$//')
```

```
nmap -p$ports -sC -sV 10.10.11.42
```

# Host Discovery
#### Scan Network Range
```
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```

This scanning method works only if the firewalls of the hosts allow it.

## Scan Single IP
Before we scan a single host for open ports and its services, we first have to determine if it is alive or not. For this, we can use the same method as before.

```
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace
```

![[Pasted image 20260702143153.png]]
Another way to determine why Nmap has our target marked as "alive" is with the "`--reason`" 
option.

# Host and Port Scanning
There are a total of 6 different states for a scanned port we can obtain:
![[Pasted image 20260702143447.png]]

## Discovering Open TCP Ports
We can define the ports one by one (`-p 22,25,80,139,445`), by range (`-p 22-445`), by top ports (`--top-ports=10`) from the `Nmap` database that have been signed as most frequent, by scanning all ports (`-p-`) but also by defining a fast port scan, which contains top 100 ports (`-F`).

```
sudo nmap 10.129.2.28 --top-ports=10
```





