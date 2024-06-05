# Target: 10.129.133.174
## Q1: Figure out the exact organisation name from the IMAP/POP3 service and submit it as the answer.

```sh
nmap -sV -sC -p110,143,993,995 10.129.133.174
```
![[Pasted image 20240518152500.png]]
Ans: `InlaneFreight Ltd`
## Q2: What is the FQDN that the IMAP and POP3 servers are assigned to?
Ans: `dev.inlanefreight.htb`
## Q3: Enumerate the IMAP service and submit the flag as the answer. (Format: HTB{...})

```sh
openssl s_client -connect 10.129.133.174:imaps
```
![[Pasted image 20240518153054.png]]
Ans: `HTB{roncfbw7iszerd7shni7jr2343zhrj}`
## Q4: What is the customised version of the POP3 server?

```sh
openssl s_client -connect 10.129.133.174:pop3s
```
![[Pasted image 20240518155003.png]]
Ans: `InFreight POP3 v9.188`
## Q5: What is the admin email address?
![[Pasted image 20240518154523.png]]
Ans: `devadmin@inlanefreight.htb`

## Q6: Try to access the emails on the IMAP server and submit the flag as the answer. (Format: HTB{...})
```sh
openssl s_client -connect 10.129.133.174:imaps
```
![[Pasted image 20240518154429.png]]
Ans: `HTB{983uzn8jmfgpd8jmof8c34n7zio}`