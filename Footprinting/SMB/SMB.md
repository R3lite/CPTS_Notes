Server Message Block is a client-server protocol that regulates access to files and entire directories and other network resources such as printers, routers, or interfaces  released for the network.
Used mainly for windows because of downward-compatibility.
Can you used on Linux and Unix distributions thanks to free software project Samba.
In IP networks, `SMB` uses TCP protocol.
Some examples: [Examples](https://winprotocoldoc.blob.core.windows.net/productionwindowsarchives/MS-SMB2/%5bMS-SMB2%5d.pdf#%5B%7B%22num%22%3A920%2C%22gen%22%3A0%7D%2C%7B%22name%22%3A%22XYZ%22%7D%2C69%2C738%2C0%5D)

### `SMB`
Access rights are defined by `Access Control Lists (ACL)`. They can be controlled in a fine-grained manner based on attributes such as execute, read, and full access for individual users or user groups. **They do not correspond to the rights assigned locally on the server**.
### Samba
Samba implements `Common Internet File System` ([`CIFS`](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-cifs/934c2faa-54af-4526-ac74-6a24d126724e)) network protocol. It's a "dialect" of `SMB`. `CIFS` allows to communicate with newer Windows systems. Therefore, it usually is referred to as `SMB / CIFS`. When we pass `SMB` commands to an older `NetBIOS` service, it usually connects to the Samba over TCP ports 137,138,139, but `CIFS` uses port 445 only.


| `SMB` Version | Supported                           | Features                                                               |
| ------------- | ----------------------------------- | ---------------------------------------------------------------------- |
| `CIFS`        | Windows NT 4.0                      | Communication via NetBIOS interface                                    |
| `SMB 1.0`     | Windows 2000                        | Direct connection via TCP                                              |
| `SMB 2.0`     | Windows Vista, Windows Server 2008  | Performance upgrades, improved message signing, caching features       |
| `SMB 2.1`     | Windows 7, Windows Server 2008 R2   | Locking mechanisms                                                     |
| `SMB 3.0`     | Windows 8, Windows Server 2012      | Multichannel connections, end-to-end encryption, remote storage access |
| `SMB 3.0.2`   | Windows 8.1, Windows Server 2012 R2 |                                                                        |
| `SMB 3.1.1`   | Windows 10, Windows Server 2016     | Integrity checking, AES-128 encryption                                 |

A `workgroup` is a group name that identifies an arbitrary collection of computers and their resources on an `SMB` network. There can be multiple `workgroups` on the network at nay given time. IBM developed an application programming interface (API) for networking computers called the Network Basic Input/Output System(`NetBIOS`). The `NetBIOS` API provided a blueprint for an application to connect and share data with other computers. In a `NetBIOS` environment, when a machine goes online, it needs a name, which is done through the so-called name registration procedure. Either each host reserves its `hostname` on the network, or the `NetBIOS` Name Server(`NBNS`) is used for this purpose. It also has been enhanced to Windows Internet Name Service (WINS). 

Samba settings [here](https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html)
To check current configuration
```bash
cat /etc/samba/smb.conf | grep -v "#\|\;" 
```

The `SMB` server daemon `smbd`. 
`NetBIOS` message block daemon `nmbd`.

### Samba settings

| **Setting**                    | **Description**                                                       |
| ------------------------------ | --------------------------------------------------------------------- |
| `[sharename]`                  | The name of the network share.                                        |
| `workgroup = WORKGROUP/DOMAIN` | Workgroup that will appear when clients query.                        |
| `path = /path/here/`           | The directory to which user is to be given access.                    |
| `server string = STRING`       | The string that will show up when a connection is initiated.          |
| `unix password sync = yes`     | Synchronize the UNIX password with the SMB password?                  |
| `usershare allow guests = yes` | Allow non-authenticated users to access defined share?                |
| `map to guest = bad user`      | What to do when a user login request doesn't match a valid UNIX user? |
| `browseable = yes`             | Should this share be shown in the list of available shares?           |
| `guest ok = yes`               | Allow connecting to the service without using a password?             |
| `read only = yes`              | Allow users to read files only?                                       |
| `create mask = 0700`           | What permissions need to be set for newly created files?              |
### Dangerous settings

| **Setting**                 | **Description**                                                                                                           |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `browseable = yes`          | Allow listing available shares in the current share?                                                                      |
| `read only = no`            | Forbid the creation and modification of files?                                                                            |
| `writable = yes`            | Allow users to create and modify files?                                                                                   |
| `guest ok = yes`            | Allow connecting to the service without using a password?                                                                 |
| `enable privileges = yes`   | Honor privileges assigned to specific SID?                                                                                |
| `create mask = 0777`        | What permissions must be assigned to the newly created files? [`mask`](https://linuxize.com/post/umask-command-in-linux/) |
| `directory mask = 0777`     | What permissions must be assigned to the newly created directories?                                                       |
| `logon script = script.sh`  | What script needs to be executed on the user's login?                                                                     |
| `magic script = script.sh`  | Which script should be executed when the script gets closed?                                                              |
| `magic output = script.out` | Where the output of the magic script needs to be stored?                                                                  |

Display a list of the server's shares:
```bash
smbclient -N -L //10.129.14.128
```
To log in:
```bash
smbclient //10.129.14.128/notes
```
To execute local system commands
```sh
!<cmd>
```
To check Samba Status:
```sh
smbstatus
```
*Apart from the Samba version, we can also see who, from which host, and which share the client is connected.*

With domain-level security, the samba server acts as a member of a Windows domain. Each domain has at least one domain controller, usually a Windows NT server providing password authentication. This domain controller provides the `workgroup` with a definitive password server. The domain controllers keep track of users and passwords in their own `NTDS.dit` and `Security Authentication Module (SAM)` and authenticate each user when they log in for the first time and wish to access another machine's share.

Handy tool to enumerate `SMB` is `rpcclient`. This is a tool to perform `MS-RPC` functions.
The Remote Procedure Call (`RPC`) is a concept and, therefore, also a central tool to realise operational and work-sharing structures in networks and client-server architectures. The communication process via `RPC` includes passing parameters and the return of a function value.

### Using `RPCclient`

```sh
 rpcclient -U "" 10.129.14.128
```

|**Query**|**Description**|
|---|---|
|`srvinfo`|Server information.|
|`enumdomains`|Enumerate all domains that are deployed in the network.|
|`querydominfo`|Provides domain, server, and user information of deployed domains.|
|`netshareenumall`|Enumerates all available shares.|
|`netsharegetinfo <share>`|Provides information about a specific share.|
|`enumdomusers`|Enumerates all domain users.|
|`queryuser <RID>`|Provides information about a specific user.|
Brute forcing user RIDs
```sh
for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.14.128 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```
An alternative would be a python script [samrdump.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/samrdump.py)
Other useful tools: [SMBMap](https://github.com/ShawnDEvans/smbmap), [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec), [enum4linux-ng](https://github.com/cddmp/enum4linux-ng)

[[SMB Exercises]]
