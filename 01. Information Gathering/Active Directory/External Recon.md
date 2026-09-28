## What Are We Looking For?
IP Space, Domain Information, Schema Format, Data Disclosures and Breach Data.
## Initial Enumeration of the Domain
### Identifying Hosts

First, let's take some time to listen to the network and see what's going on. We can use `Wireshark` and `TCPDump` to "put our ear to the wire" and see what hosts and types of network traffic we can capture.

```
sudo -E wireshark
```

#### Tcpdump Output

```
sudo tcpdump -i ens224
```

#### Starting Responder

```
sudo responder -I ens224 -A
```

#### FPing Active Checks

```
fping -asgq 172.16.5.0/23
```

### Kerbrute - Internal AD Username Enumeration
We can use the following list https://github.com/insidetrust/statistically-likely-usernames

```
kerbrute userenum -d INLANEFREIGHT.LOCAL --dc 172.16.5.5 jsmith.txt -o valid_ad_users
```






