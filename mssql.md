# MSSQL

```shell-session
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248
```

```shell-session
msf6 auxiliary(scanner/mssql/mssql_ping)
```

```shell-session
 python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth
```

```shell-session
sqsh -S 10.129.20.13 -U username -P Password123
```

```cmd-session
C:\htb> sqlcmd -S 10.129.20.13 -U username -P Password123
```
