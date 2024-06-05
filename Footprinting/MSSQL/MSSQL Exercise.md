# Target
```
10.129.85.136
```

## Q1: Enumerate the target using the concepts taught in this section. List the hostname of MSSQL server.
```sh
msfconsole mssql_ping
```
![[Pasted image 20240519080642.png]]
Ans: `ILF-SQL-01`
## Q2: Connect to the MSSQL instance running on the target using the account (backdoor:Password1), then list the non-default database present on the server.

```sh
python3 mssqlclient.py backdoor@10.129.85.136 -windows-auth
```
![[Pasted image 20240519081855.png]]
Ans: `Employees`
