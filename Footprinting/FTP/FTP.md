[FTP commands](https://www.smartfile.com/blog/the-ultimate-ftp-commands-list/)
[FTP status codes](https://en.wikipedia.org/wiki/List_of_FTP_server_return_codes)

## TFTP
Trivial File Transfer Protocol is simpler than FT Pand performs file transfers between client and server processes.  However, it does not provide user authentication and other valuable features supported by FTP. TFTP uses UDP, making it unreliable protocol.

### Commands of TFPT
| Commands | Description                                                                                                                            |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| get      | Transfers a file or set of files from the remote host to the local host.                                                               |
| put      | Transfers a file or set of files from the local host onto the remote host.                                                             |
| quit     | Exits tftp.                                                                                                                            |
| status   | Shows the current status of tfpt, including the current transfer mode (ascii or binary), connection status, time-out value, and so on. |
| verbose  | Truns verbose mode, which displays additional information during file transfer, on or off.                                             |
## Default configuration
One of the most used FTP servers on Linux-based distros is [vsFTPd](https://security.appspot.com/vsftpd.html)
Default config can be found is `/etc/vsftpd.conf`

## vsFTPd Config File
| Setting                                                     | Description                                                                                                                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| listen=NO                                                   | Run from inetd or as a standalone daemon?                                                                                                                           |
| listen=ipv6=YES                                             | Listen on IPv6?                                                                                                                                                     |
| anonymous_enable=NO                                         | Enable anonymous access?                                                                                                                                            |
| local_enable=YES                                            | Allow local users to login?                                                                                                                                         |
| dirmessage_enable=YES                                       | Display active directory messages when users go into certain directories?                                                                                           |
| use_localtime=YES                                           | Use local time?                                                                                                                                                     |
| xferlog_enable=YES                                          | Active logging of uploads/downloads?                                                                                                                                |
| connect_from_port_20=YES                                    | Connect from port 20?                                                                                                                                               |
| secure_chroot_dir=/var/run/vsftpd/empty                     | Name of an empty directory                                                                                                                                          |
| pam_service_name=vsftpd                                     | The string is the name of the [PAM](https://www.microsoft.com/en-us/security/business/security-101/what-is-privileged-access-management-pam) serice vsftpd will use |
| rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem          | The last three options specify the location of the RSA certificate to use for SSL encrypted connections.                                                            |
| rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key |                                                                                                                                                                     |
| ssl_enable=NO                                               |                                                                                                                                                                     |
There is also file called `/etc/ftpusers` that we also need to pay attention to.
This file is used to deny certain users access to the FTP service.

### Dangerous settings
| Setting                      | Description                                                                        |
| ---------------------------- | ---------------------------------------------------------------------------------- |
| anonymous_enable=YES         | Allowing anonymous login?                                                          |
| anon_upload_enable=YES       | Allowing anonymous to upload files?                                                |
| anon_mkdir_write_enable=YES  | Allowing anonymous to create new directories?                                      |
| no_anon_password=YES         | Do not ask anonymous for password?                                                 |
| anon_root=/home/username/ftp | Directory for anonymous                                                            |
| write_enable=YES             | Allow the usage of FTP commands: STOR, DELE, RNFR, RNTO, MKD, RMD, APPE, and SITE? |
### vsFTPd Detailed Output
| Setting                 | Description                                                                      |
| ----------------------- | -------------------------------------------------------------------------------- |
| dirmessage_enable=YES   | Show a message  when they first enter a new directory?                           |
| chown_uploads=YES       | Change ownership  of anonymously uploaded files?                                 |
| chown_username=username | User who is given ownership of  anonymously uploaded files.                      |
| local_enable=YES        | Enable local users to login?                                                     |
| chroot_local_user=YES   | Place local users into their home directory?                                     |
| chroot_list_enable=YES  | Use a list of local users that will be placed in their home directory?           |
| hide_ids=YES            | All user and group information in directory listings will be displayed as "ftp". |
| ls_recurse_enable=YES   | Allows the use of recurse listings.                                              |
[[FTP Exercise]]
