Internet Message Access Protocol enables access to email from a mail server. It also allows online management of email directly on a server and supports folder structure.
Post Office Protocol also allows access to email from a mail server but doesn't provide as many functionalities as IMAP.
The client establishes the connection to the server via port 143, for communication it uses test-based commands in `ASCII` format. Several commands can be send in succession without waiting for confirmation from the server. Later confirmations from the server can be assigned to the individual commands using the identifiers sent along with the commands.
User is authenticated by username and password.
Access to a desired mailbox is only possible after successful authentication.
IMAP works unencrypted, usually SSL/TLS is used to prevent unauthorised access to the mailboxes.
### Configuration
In the documentation of Dovecot, we can find the individual [core settings](https://doc.dovecot.org/settings/core/) and [service configuration](https://doc.dovecot.org/configuration_manual/service_configuration/) options that can be utilised for our experiments.

|**Setting**|**Description**|
|---|---|
|`auth_debug`|Enables all authentication debug logging.|
|`auth_debug_passwords`|This setting adjusts log verbosity, the submitted passwords, and the scheme gets logged.|
|`auth_verbose`|Logs unsuccessful authentication attempts and their reasons.|
|`auth_verbose_passwords`|Passwords used for authentication are logged and can also be truncated.|
|`auth_anonymous_username`|This specifies the username to be used when logging in with the ANONYMOUS SASL mechanism.|
## Commands

### IMAP

| **Command**                     | **Description**                                                                                               |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `1 LOGIN username password`     | User's login.                                                                                                 |
| `1 LIST "" *`                   | Lists all directories.                                                                                        |
| `1 CREATE "INBOX"`              | Creates a mailbox with a specified name.                                                                      |
| `1 DELETE "INBOX"`              | Deletes a mailbox.                                                                                            |
| `1 RENAME "ToRead" "Important"` | Renames a mailbox.                                                                                            |
| `1 LSUB "" *`                   | Returns a subset of names from the set of names that the User has declared as being `active` or `subscribed`. |
| `1 SELECT INBOX`                | Selects a mailbox so that messages in the mailbox can be accessed.                                            |
| `1 UNSELECT INBOX`              | Exits the selected mailbox.                                                                                   |
| `1 FETCH <ID> all`              | Retrieves data associated with a message in the mailbox.                                                      |
| `1 CLOSE`                       | Removes all messages with the `Deleted` flag set.                                                             |
| `1 LOGOUT`                      | Closes the connection with the IMAP server.                                                                   |
### POP3

| **Command**     | **Description**                                             |
| --------------- | ----------------------------------------------------------- |
| `USER username` | Identifies the user.                                        |
| `PASS password` | Authentication of the user using its password.              |
| `STAT`          | Requests the number of saved emails from the server.        |
| `LIST`          | Requests from the server the number and size of all emails. |
| `RETR id`       | Requests the server to deliver the requested email by ID.   |
| `DELE id`       | Requests the server to delete the requested email by ID.    |
| `CAPA`          | Requests the server to display the server capabilities.     |
| `RSET`          | Requests the server to reset the transmitted information.   |
| `QUIT`          | Closes the connection with the POP3 server.                 |
## Footprinting the service

By default, ports `110`, `143`, `993`, and `995` are used for IMAP and POP3.
-  993, 995 used for TLS/SSL

```shell
sudo nmap 10.129.14.128 -sV -p110,143,993,995 -sC
```

### We can get access to a mailbox using
```shell
 curl -k 'imaps://10.129.14.128' --user user:p4ssw0rd
```

### For TLS encrypted POP3
```shell
openssl s_client -connect 10.129.14.128:pop3s
```
### For TLS encrypted IMAP
```shell
openssl s_client -connect 10.129.14.128:imaps
```
