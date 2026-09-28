The SOA record is located in a domain's zone file and specifies who is responsible for the operation of the domain and how DNS information for the domain is managed.
```
dig soa www.inlanefreight.com @<IP>
```
There must be precisely one `SOA` record and at least one `NS` record.
## DIG Any Query
We can use the option `ANY` to view all available records. This will cause the server to show us all available entries that it is willing to disclose. It is important to note that not all entries from the zones will be shown.
```
dig any inlanefreight.htb @10.129.14.128
```

## DIG - AXFR Zone Transfer
```
dig axfr inlanefreight.htb @10.129.14.128
```

## DIG - AXFR Zone Transfer - Internal
If the administrator used a subnet for the `allow-transfer` option for testing purposes or as a workaround solution or set it to `any`, everyone would query the entire zone file at the DNS server. In addition, other zones can be queried, which may even show internal IP addresses and hostnames.
```
dig axfr internal.inlanefreight.htb @10.129.14.128
```

Synchronization between the servers involved is realized by zone transfer. Using a ==secret key== `rndc-key`, which we have seen initially in the default configuration. The secret can be found on /etc/bind/named.conf
## Making modification on DNS Zones
We can use the tool nsupdate. Example of adding an A record:
```
nsupdate -k rndc.key
> server <IP>
> zone example.com
> update add mail.example.com 60 A <IP>
> send
> quit
```
If we had a rndc.key.