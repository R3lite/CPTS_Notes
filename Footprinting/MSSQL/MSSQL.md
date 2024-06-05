Microsoft SQL is Microsoft's SQL-based relational database management system.
It's closed source and was initially written to run on Windows operating systems.
Uses T-SQL (Transact-SQL).

### SSMS
SQL Server Management Studio comes as a feature that can be installed with the MSSQL.

We can come across a vulnerable system with SSMS with saved credentials that allows us to connect to the database.
Other clients can be used too:

| [mssql-cli](https://docs.microsoft.com/en-us/sql/tools/mssql-cli?view=sql-server-ver15) | [SQL Server PowerShell](https://docs.microsoft.com/en-us/sql/powershell/sql-server-powershell?view=sql-server-ver15) | [HeidiSQL](https://www.heidisql.com) | [SQLPro](https://www.macsqlclient.com) | [Impacket's mssqlclient.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/mssqlclient.py) |
| --------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | -------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
For pentesters Impacket's mssqlclient.py may be most useful because it is usually installed on many pentesting distrubutions.


| Default System Database | Description                                                                                                                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `master`                | Tracks all system information for an SQL server instance                                                                                                                                               |
| `model`                 | Template database that acts as a structure for every new database created. Any setting changed in the model database will be reflected in any new database created after changes to the model database |
| `msdb`                  | The SQL Server Agent uses this database to schedule jobs & alerts                                                                                                                                      |
| `tempdb`                | Stores temporary objects                                                                                                                                                                               |
| `resource`              | Read-only database containing system objects included with SQL server                                                                                                                                  |
By default encryption is not enforced when attempting to connect.

This is not an extensive list because there are countless ways MSSQL databases can be configured by admins based on the needs of their respective organizations. We may benefit from looking into the following:

- MSSQL clients not using encryption to connect to the MSSQL server
    
- The use of self-signed certificates when encryption is being used. It is possible to spoof self-signed certificates
    
- The use of [named pipes](https://docs.microsoft.com/en-us/sql/tools/configuration-manager/named-pipes-properties?view=sql-server-ver15)
    
- Weak & default `sa` credentials. Admins may forget to disable this account

## Footprinting the Service
Default port is TCP port 1433.

From the script below we can see the `hostname`, `database instance name`, `software version of MSSQL` and `named pipes are enabled`.

```shell
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248
```

We can also use Metasploit to run auxiliary scanner called mssql_ping.

### Connecting with mssqlclient.py

```shell
python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth
```


