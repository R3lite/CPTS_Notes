[Rsync](https://linux.die.net/man/1/rsync) is a fast and efficient tool for locally and remotely copying files.

By default it uses port 873
Used for backup and  mirroring
Uses delta-transfer algorithm. The algorithm reduces the amount of data transmitted over the network when a version of the file already exists on the destination host. It does this by sending only the differences between the source files and the older version of the files that reside on the destination server.

This [guide](https://book.hacktricks.xyz/network-services-pentesting/873-pentesting-rsync) covers some of the ways Rsync can be abused, most notably by listing the contents of a shared folder on a target server and retrieving files.

Probing for accessible shares
```shell
nc -nv 127.0.0.1 873
```

Enumerating an Open Share
```shell
rsync -av --list-only rsync://127.0.0.1/dev
```

If Rsync is configured to use SSH to transfer files, we could modify our commands to include the `-e ssh` flag, or `-e "ssh -p2222"` if a non-standard port is in use for SSH. This [guide](https://phoenixnap.com/kb/how-to-rsync-over-ssh) is helpful for understanding the syntax for using Rsync over SSH.

