# Target: 
```
10.129.127.209
```

## Q1: Enumerate the SNMP service and obtain the email address of the admin. Submit it as the answer.
```sh
nmap -sV -sC -p161,162 10.129.127.209 -oA initial_scan
```
Ports closed
```sh
snmpwalk -v2c -c public 10.129.127.209
```
![[Pasted image 20240518174354.png]]
Ans: `devadmin@inlanefreight.htb`
## Q2: What is the customised version of the SNMP server?
Ans: `InFreight SNMP v0.91`

## Q3: Enumerate the custom script that is running on the system and submit its output as the answer.
![[Pasted image 20240518174715.png]]
Ans: `HTB{5nMp_fl4g_uidhfljnsldiuhbfsdij44738b2u763g}`

[[snmp_log]]