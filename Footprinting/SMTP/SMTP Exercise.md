# Target IP:
```
10.129.207.107
```

## Q1: Enumerate the SMTP service and submit the banner, including its version as the answer.

```sh
sudo nmap -A -T4 -p25 -oA smtp-initial_scan 10.129.207.107
```

![[Pasted image 20240518132101.png]]
```sh
telnet 10.129.207.107 25
```
![[Pasted image 20240518132506.png]]
Ans: `InFreight ESMTP v2.11`
## Q2: Enumerate the SMTP service even further and find the username that exists on the system. Submit it as the answer.
```sh
sudo nmap 10.129.207.107 -p25 --script smtp-open-relay -v
```
![[Pasted image 20240518133037.png]]
```sh
smtp-user-enum -M VRFY -U footprinting-wordlist.txt -t 10.129.207.107 -w 15
```
Ans: `robin`