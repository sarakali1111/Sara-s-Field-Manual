Port Forwarding
```
ssh -L 8000:172.16.0.10:80 user@172.16.0.5 -fN
```
-f Backgrounds the shell 
-N Tells SSH that it does not need to execute any commands, only set up the connection
However, I prefer to run it without the -fN and instead use verbose mode -vvv so we can troubleshoot.
#### Meterpreter Reverse Port Forwarding Rules
```
portfwd add -R -l 8081 -p 1234 -L 10.10.14.18
```


