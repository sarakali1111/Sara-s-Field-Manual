#### Bash one-liner to perform full ping sweep.
```
for i in {1..255}; do (ping -c 1 192.168.1.${i} | grep "bytes from" &); done
```
#### Port Scanning in Bash one-liner.
```
for i in {1..65535}; do (echo > /dev/tcp/192.168.1.1/$i) >/dev/null 2>&1 && echo $i is open; done
```

User **route** command to show available routes.
#### Ping Sweep For Loop Using CMD
```
for /L %i in (1 1 254) do ping 172.16.5.%i -n 1 -w 100 | find "Reply"
```

#### Ping Sweep Using PowerShell
```
1..254 | % {"172.16.5.$($_): $(Test-Connection -count 1 -comp 172.16.5.$($_) -quiet)"}
```

