Secure Shell enables two computers to establish an encrypted and direct connection within a possibly insecure network on the standard port TCP 22. 
- Can be configured to accept connections from specific clients
- Runs on all common operating systems
- native on all Linux and MacOS
- [OpenBSD SSH](https://www.openssh.com/) (`OpenSSH`) is an open-source fork of the original and commercial SSH server from SSH Communication Security.
- There are two competing protocols:
	- SSH-1 - vulnerable to MITM attacks
	- SSH-2 is more advanced
In total, OpenSSH has six different authentication methods:

1. Password authentication
2. Public-key authentication
3. Host-based authentication
4. Keyboard authentication
5. Challenge-response authentication
6. GSSAPI authentication

The [sshd_config](https://www.ssh.com/academy/ssh/sshd_config) file, responsible for the OpenSSH server, has only a few of the settings configured by default.
The default configuration includes X11 forwarding which contained a command injection vulnerability in version 7.2p1 of OpenSSH 2016

### Dangerous settings
| **Setting**                  | **Description**                             |
| ---------------------------- | ------------------------------------------- |
| `PasswordAuthentication yes` | Allows password-based authentication.       |
| `PermitEmptyPasswords yes`   | Allows the use of empty passwords.          |
| `PermitRootLogin yes`        | Allows to log in as the root user.          |
| `Protocol 1`                 | Uses an outdated version of encryption.     |
| `X11Forwarding yes`          | Allows X11 forwarding for GUI applications. |
| `AllowTcpForwarding yes`     | Allows forwarding of TCP ports.             |
| `PermitTunnel`               | Allows tunneling.                           |
| `DebianBanner yes`           | Displays a specific banner when logging in. |
Some instructions and [hardening guides](https://www.ssh-audit.com/hardening_guides.html) can be used to harden our SSH servers.

## Footprinting the service
SSH-Audit
```shell
git clone https://github.com/jtesta/ssh-audit.git && cd ssh-audit
./ssh-audit.py 10.129.14.132
```

Change authentication method
```shell
ssh -v cry0l1t3@10.129.14.132
```
For potential brute-force attacks, we can specify the authentication method with the SSH client option 
```shell
ssh -v cry0l1t3@10.129.14.132 -o PreferredAuthentications=password
```
