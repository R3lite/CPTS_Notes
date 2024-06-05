Network File System is a network file system developed by Sun Microsystems and has the same purpose as [[SMB]]. Its purpose is to access file systems over a network as if they were local. However, it uses an entirely different protocol. NFS is used between Linux and Unix systems. This mean that NFS clients cannot communicate directly with [[SMB]] servers. NFS is an Internet standard. NFS protocol version 3.0 (NFSv3) authenticates the client computer.

| **Version** | **Features**                                                                                                                                                                                                                                                         |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `NFSv2`     | It is older but is supported by many systems and was initially operated entirely over UDP.                                                                                                                                                                           |
| `NFSv3`     | It has more features, including variable file size and better error reporting, but is not fully compatible with NFSv2 clients.                                                                                                                                       |
| `NFSv4`     | It includes Kerberos, works through firewalls and on the Internet, no longer requires portmappers, supports ACLs, applies state-based operations, and provides performance improvements and high security. It is also the first version to have a stateful protocol. |
It uses only one UDP or TCP port `2049`.
NFS is based on the [Open Network Computing Remote Procedure Call](https://en.wikipedia.org/wiki/Sun_RPC) (`ONC-RPC`/`SUN-RPC`) protocol exposed on `TCP` and `UDP` ports `111`, which uses [External Data Representation](https://en.wikipedia.org/wiki/External_Data_Representation) (`XDR`) for the system-independent exchange of data. The NFS protocol has `no` mechanism for `authentication` or `authorization`.
The most common authentication is via UNIX `UID`/`GID` and `group memberships`, which is why this syntax is most likely to be applied to the NFS protocol.
NFS  should only be used with this authentication method in  trusted networks.

### Settings

```sh
cat /etc/exports 
```

| **Option**         | **Description**                                                                                                                             |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `rw`               | Read and write permissions.                                                                                                                 |
| `ro`               | Read only permissions.                                                                                                                      |
| `sync`             | Synchronous data transfer. (A bit slower)                                                                                                   |
| `async`            | Asynchronous data transfer. (A bit faster)                                                                                                  |
| `secure`           | Ports above 1024 will not be used.                                                                                                          |
| `insecure`         | Ports above 1024 will be used.                                                                                                              |
| `no_subtree_check` | This option disables the checking of subdirectory trees.                                                                                    |
| `root_squash`      | Assigns all permissions to files of root UID/GID 0 to the UID/GID of anonymous, which prevents `root` from accessing files on an NFS mount. |
Creating an entry
```sh
echo '/mnt/nfs  10.129.14.0/24(sync,no_subtree_check)' >> /etc/exports
systemctl restart nfs-kernel-server
exportfs
```

### Dangerous settings
| **Option**       | **Description**                                                                                                      |
| ---------------- | -------------------------------------------------------------------------------------------------------------------- |
| `rw`             | Read and write permissions.                                                                                          |
| `insecure`       | Ports above 1024 will be used.                                                                                       |
| `nohide`         | If another file system was mounted below an exported directory, this directory is exported by its own exports entry. |
| `no_root_squash` | All files created by root are kept with the UID/GID 0.                                                               |

### Footprinting the Service
When footprinting NFS, the TCP ports `111` and `2049` are essential.

Nmap scanning:
```sh
sudo nmap <IP> -p111,2049 -sV -sC
```
The `rpcinfo` NSE script retrieves a list of all currently running RPC services, their names and descriptions, and the ports they use.
Nmap scanning running nfs scripts:
```sh
sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049
```

Show available NFS Shares
```sh
showmount -e 10.129.14.128
```
Mountings NFS Share
```sh
mkdir target-NFS
sudo mount -t nfs <IP>:/ ./target-NFS/ -o nolock
```
List Contents with Usernames & Group Names
```sh
ls -l /mnt/nfs
```
List Contents with UIDs & GUIDs
```sh
ls -n mnt/nfs/
```
We can also use NFS for further escalation. For example, if we have access to the system via SSH and want to read files from another folder that a specific user can read, we would need to upload a shell to the NFS share that has the `SUID` of that user and then run the shell via the SSH user.

Unmounting 
```sh
sudo unmount ./target-NFS
```

[[NFS Exercises]]
