# Target
```
10.129.210.114
```

## Q1: Enumerate the MySQL server and determine the version in use. (Format: MySQL X.X.XX) 
```sh
nmap -A --script mysql* -p3306 10.129.210.114
```
![[Pasted image 20240518212959.png]]
Ans: `MySQL 8.0.27`
## Q2: During our penetration test, we found weak credentials "robin:robin". We should try these against the MySQL server. What is the email address of the customer "Otto Lang"?

![[Pasted image 20240518213611.png]]

Ans: `ultrices@google.htb`