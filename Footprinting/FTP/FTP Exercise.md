IP Address: 10.129.63.201
```bash
nmap -sV 10.129.63.201
```
![[Pasted image 20240515101201.png]]
```
nc 10.129.63.201 21
```
![[Pasted image 20240515101310.png]]
220 InFreight FTP v1.1
```
ftp 10.129.63.201
```
Failed
```bash
nmap -sV -p21 -sC -A 10.129.63.201
```
![[Pasted image 20240515103306.png]]
Failed

```shell-session
openssl s_client -connect 10.129.63.201:21 -starttls ftp
```

```
nc -nv 10.129.63.201 21
```
Allows to get a banner but failed to get any more info

```shell-session
sudo nmap -sV -p21 -sC -A 10.129.63.201 --script-trace
```

Anonymous login
```bash
ftp 10.129.63.201
```
Login: anonymous
Password: email address

Flag: HTB{b7skjr4c76zhsds7fzhd4k3ujg7nhdjre}
