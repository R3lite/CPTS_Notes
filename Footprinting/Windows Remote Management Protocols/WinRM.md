The Windows Remote Management is a simple Windows integrated remote management protocol base on the command line.
- Uses Simple Object Access Protocol (SOAP)
- Ports TCP 5985 5986

Windows remote Shell (WinRS) lets us execute arbitrary commands on the remote system.

## Footprinting the Service
```shell
nmap -sV -sC 10.129.201.248 -p5985,5986 --disable-arp-ping -n
```
The [Test-WsMan](https://docs.microsoft.com/en-us/powershell/module/microsoft.wsman.management/test-wsman?view=powershell-7.2) cmdlet is responsible for this, and the host's name in question is passed to it. In Linux-based environments, we can use the tool called [evil-winrm](https://github.com/Hackplayers/evil-winrm), another penetration testing tool designed to interact with WinRM.
```shell
evil-winrm -i 10.129.201.248 -u Cry0l1t3 -p P455w0rD!
```
