nmap -sV -T4 -p137,138,139,445 10.129.15.244
![[Pasted image 20240516084906.png]]
```sh
smbclient -N -L //10.129.15.244
```
![[Pasted image 20240516085144.png]]
```sh
smbclient //10.129.15.244/sambashare
```
![[Pasted image 20240516085513.png]]*That is not a correct flag*
![[Pasted image 20240516085657.png]]![[Pasted image 20240516085710.png]]
 ```sh
rpcclient -U "" 10.129.15.244
```
![[Pasted image 20240516085851.png]]
![[Pasted image 20240516085949.png]]
![[Pasted image 20240516090056.png]]
```sh
smbmap -H 10.129.15.244 -s sambashare
```
Couldn't find open ports
```sh
python3 enum4linux-ng.py -A 10.129.15.244
```
[[enum4linux-ng result]]
