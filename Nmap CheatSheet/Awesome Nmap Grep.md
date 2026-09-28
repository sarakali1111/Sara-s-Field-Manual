Output:
![[Pasted image 20260728113355.png]]
Use the script below locate at the Tools directory.
python3 ~/Documents/Tools/create_table_from_process_nmapScan.py nmap_process.txt

```
xmlstarlet sel -t \
                     -m "/nmaprun/host" \
                     -v "concat('Host: ',address/@addr,' Ports: ',count(ports/port[state/@state='open']))" -n \
                     -m "ports/port[state/@state='open']" \
                     -v "concat(state/@state,'|',@protocol,'/',@portid,'|',normalize-space(concat(service/@product,' ',service/@version,' ',service/@extrainfo)))" -n \
                     -b -b Administrator_allSvc.xml | \
                     awk -F'|' '
                 /^Host:/ {print; next}
                 {
                     printf "%-6s %-10s %s\n", $1, $2, $3
                 }' > nmap_process.txt
```

```
xmlstarlet sel -t \
                     -m "/nmaprun/host" \
                     -v "concat('Host: ',address/@addr,' Ports: ',count(ports/port[state/@state='open']))" -n \
                     -m "ports/port[state/@state='open']" \
                     -v "concat(state/@state,'|',@protocol,'/',@portid,'|',normalize-space(concat(service/@product,' ',service/@version,' ',service/@extrainfo)))" -n \
                     -b -b Administrator_allSvc.xml | \
                     awk -F'|' '
                 /^Host:/ {print; next}
                 {
                     printf "%-6s %-10s %s\n", $1, $2, $3
                 }'
```

Run the below command for a cool visualization of a .nmap scan:
```
batcat FindingsAuthority_service_allTCP.nmap -l ruby
```
