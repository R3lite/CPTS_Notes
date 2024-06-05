Target IP: 
```
10.129.159.154
```
Q1: Enumerate the NFS service and submit the contents of the flag.txt in the "nfs" share as the answer.
Q2: Enumerate the NFS service and submit the contents of the flag.txt in the "nfsshare" share as the answer.

### Exercise 1
```sh
nmap -sV -T4 -p111,2049 10.129.159.154
```
![[Pasted image 20240516170440.png]]

```sh
nmap -sV --script nfs* -T4 -p111,2049 10.129.159.154
```
![[Pasted image 20240516170548.png]]
```sh
mkdir targetNfs
sudo mount -t nfs 10.129.159.154:/ ./targetNfs -o nolock
```

![[Pasted image 20240516171545.png]]
```
HTB{hjglmvtkjhlkfuhgi734zthrie7rjmdze}
```

![[Pasted image 20240516171700.png]]
```
HTB{8o7435zhtuih7fztdrzuhdhkfjcn7ghi4357ndcthzuc7rtfghu34}
```
