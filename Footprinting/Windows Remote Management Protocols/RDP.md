The Remote Desktop Protocol is a protocol developed by Microsoft for remote access to a computer running Windows operating system. This protocol allows display and control commands to be transmitted via the GUI encrypted over IP networks.
RDP works at the application layer in the TCP/IP reference model. 
Usually runs on TCP port 3389.
FOR RDP to work both the network firewall and the firewall on the server must allow connections from the outside. If [Network Address Translation](https://en.wikipedia.org/wiki/Network_address_translation) (`NAT`) is used on the route between client and server, as is often the case with Internet connections, the remote computer needs the public IP address to reach the server. In addition, port forwarding must be set up on the NAT router in the direction of the server.
This service can be activated using the `Server Manager` and comes with the default setting to allow connections to the service only to hosts with [Network level authentication](https://en.wikipedia.org/wiki/Network_Level_Authentication) (`NLA`).

## Footprinting the Service

```shell
nmap -sV -sC 10.129.201.248 -p3389 --script rdp*
```
We can see that the `RDP cookies` (`mstshash=nmap`) used by Nmap to interact with the RDP server can be identified by `threat hunters` and various security services such as [Endpoint Detection and Response](https://en.wikipedia.org/wiki/Endpoint_detection_and_response) (`EDR`), and can lock us out as penetration testers on hardened networks.

A Perl script named [rdp-sec-check.pl](https://github.com/CiscoCXSecurity/rdp-sec-check) has also been developed by [Cisco CX Security Labs](https://github.com/CiscoCXSecurity) that can unauthentically identify the security settings of RDP servers based on the handshakes.

```shell
sudo cpan
```

```shell
git clone https://github.com/CiscoCXSecurity/rdp-sec-check.git && cd rdp-sec-check
./rdp-sec-check.pl 10.129.201.248
```

Initiate an RDP Session
```shell
xfreerdp /u:cry0l1t3 /p:"P455w0rd!" /v:10.129.201.248
```
