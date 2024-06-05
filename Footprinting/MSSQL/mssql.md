sudo msfconsole
[sudo] password for kali: 
Metasploit tip: You can pivot connections over sessions started with the 
ssh_login modules
                                                  

MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMM                MMMMMMMMMM
MMMN$                           vMMMM
MMMNl  MMMMM             MMMMM  JMMMM
MMMNl  MMMMMMMN       NMMMMMMM  JMMMM
MMMNl  MMMMMMMMMNmmmNMMMMMMMMM  JMMMM
MMMNI  MMMMMMMMMMMMMMMMMMMMMMM  jMMMM
MMMNI  MMMMMMMMMMMMMMMMMMMMMMM  jMMMM
MMMNI  MMMMM   MMMMMMM   MMMMM  jMMMM
MMMNI  MMMMM   MMMMMMM   MMMMM  jMMMM
MMMNI  MMMNM   MMMMMMM   MMMMM  jMMMM
MMMNI  WMMMM   MMMMMMM   MMMM#  JMMMM
MMMMR  ?MMNM             MMMMM .dMMMM
MMMMNm `?MMM             MMMM` dMMMMM
MMMMMMN  ?MM             MM?  NMMMMMN
MMMMMMMMNe                 JMMMMMNMMM
MMMMMMMMMMNm,            eMMMMMNMMNMM
MMMMNNMNMMMMMNx        MMMMMMNMMNMMNM
MMMMMMMMNMMNMMMMm+..+MMNMMNMNMMNMMNMM
        https://metasploit.com


       =[ metasploit v6.4.5-dev                           ]
+ -- --=[ 2413 exploits - 1242 auxiliary - 423 post       ]
+ -- --=[ 1465 payloads - 47 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

msf6 > search mssql_ping

Matching Modules
================

   #  Name                                Disclosure Date  Rank    Check  Description
   -  ----                                ---------------  ----    -----  -----------
   0  auxiliary/scanner/mssql/mssql_ping  .                normal  No     MSSQL Ping Utility


Interact with a module by name or index. For example info 0, use 0 or use auxiliary/scanner/mssql/mssql_ping

msf6 > use 0
msf6 auxiliary(scanner/mssql/mssql_ping) > show options

Module options (auxiliary/scanner/mssql/mssql_ping):

   Name                 Current Setting  Required  Description
   ----                 ---------------  --------  -----------
   PASSWORD                              no        The password for the specified username
   RHOSTS                                yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   THREADS              1                yes       The number of concurrent threads (max one per host)
   USERNAME             sa               no        The username to authenticate as
   USE_WINDOWS_AUTHENT  false            yes       Use windows authentication (requires DOMAIN option set)


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/mssql/mssql_ping) > set RHOSTS 10.129.85.136
RHOSTS => 10.129.85.136
msf6 auxiliary(scanner/mssql/mssql_ping) > run

[*] 10.129.85.136:        - SQL Server information for 10.129.85.136:
[+] 10.129.85.136:        -    ServerName      = ILF-SQL-01
[+] 10.129.85.136:        -    InstanceName    = MSSQLSERVER
[+] 10.129.85.136:        -    IsClustered     = No
[+] 10.129.85.136:        -    Version         = 15.0.2000.5
[+] 10.129.85.136:        -    tcp             = 1433
[+] 10.129.85.136:        -    np              = \\ILF-SQL-01\pipe\sql\query
[*] 10.129.85.136:        - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/mssql/mssql_ping) >                                                                                                                                                                                                                                             
┌──(kali㉿kali)-[~]
└─$ python3 mssqlclient.py -p 1433 backdoor@10.129.85.136 -windows-auth
Impacket v0.12.0.dev1 - Copyright 2023 Fortra

Password:
[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(ILF-SQL-01): Line 1: Changed database context to 'master'.
[*] INFO(ILF-SQL-01): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (150 7208) 
[!] Press help for extra shell commands
SQL (ILF-SQL-01\backdoor  dbo@master)> show databases
ERROR: Line 1: Could not find stored procedure 'show'.
SQL (ILF-SQL-01\backdoor  dbo@master)> help

    lcd {path}                 - changes the current local directory to {path}
    exit                       - terminates the server process (and this session)
    enable_xp_cmdshell         - you know what it means
    disable_xp_cmdshell        - you know what it means
    enum_db                    - enum databases
    enum_links                 - enum linked servers
    enum_impersonate           - check logins that can be impersonated
    enum_logins                - enum login users
    enum_users                 - enum current db users
    enum_owner                 - enum db owner
    exec_as_user {user}        - impersonate with execute as user
    exec_as_login {login}      - impersonate with execute as login
    xp_cmdshell {cmd}          - executes cmd using xp_cmdshell
    xp_dirtree {path}          - executes xp_dirtree on the path
    sp_start_job {cmd}         - executes cmd using the sql server agent (blind)
    use_link {link}            - linked server to use (set use_link localhost to go back to local or use_link .. to get back one step)
    ! {cmd}                    - executes a local shell cmd
    show_query                 - show query
    mask_query                 - mask query
    
SQL (ILF-SQL-01\backdoor  dbo@master)> enum_db;
name        is_trustworthy_on   
---------   -----------------   
master                      0   

tempdb                      0   

model                       0   

msdb                        1   

Employees                   0   

