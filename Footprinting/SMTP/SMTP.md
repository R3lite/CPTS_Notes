The Simple Mail Transfer Protocol (SMTP) is a protocol for sending emails in an IP network.
Is often combined with the IMAP or POP3 protocols.
By default SMTP servers accept connection requests on port `25`, newer also use `587`.
SMTP works unencrypted but is used in conjunction with SSL/TLS encryption.

|Client (`MUA`)|`➞`|Submission Agent (`MSA`)|`➞`|Open Relay (`MTA`)|`➞`|Mail Delivery Agent (`MDA`)|`➞`|Mailbox (`POP3`/`IMAP`)|
|---|---|---|---|---|---|---|---|---|
SMTP has two disadvantages:
- does not return a usable delivery confirmation
- users are not authenticated when a connection is established, and the sender of an email is therefore unreliable.

The identification protocol [DomainKeys](http://dkim.org/) (`DKIM`), the [Sender Policy Framework](https://dmarcian.com/what-is-spf/) (`SPF`) are responsible for rejecting suspicious emails or moving them to spam folder.

Default configuration
```shell
cat /etc/postfix/main.cf | grep -v "#" | sed -r "/^\s*$/d"
```

|**Command**|**Description**|
|---|---|
|`AUTH PLAIN`|AUTH is a service extension used to authenticate the client.|
|`HELO`|The client logs in with its computer name and thus starts the session.|
|`MAIL FROM`|The client names the email sender.|
|`RCPT TO`|The client names the email recipient.|
|`DATA`|The client initiates the transmission of the email.|
|`RSET`|The client aborts the initiated transmission but keeps the connection between client and server.|
|`VRFY`|The client checks if a mailbox is available for message transfer.|
|`EXPN`|The client also checks if a mailbox is available for messaging with this command.|
|`NOOP`|The client requests a response from the server to prevent disconnection due to time-out.|
|`QUIT`|The client terminates the session.|
To interact with the SMTP server, we can use the telnet tool to initialise a TCP connection with the SMTP server.

```shell
telnet 10.129.14.128 25
```

A list of all SMTP response codes can be found [here](https://serversmtp.com/smtp-error/).

## User enumeration
```sh
smtp-user-enum -M VRFY -U footprinting-wordlist.txt -t 10.129.207.107
```
