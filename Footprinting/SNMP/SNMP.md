Simple Network Management Protocol was created to monitor network devices. Can also be used to handle configuration tasks and change settings remotely. SNMP-enabled  hardware includes routers, switches, servers, IoT devices.

Current  version is SNMPv3.
It uses UDP port 161.
SNMP enables the use of so-called `traps` over UDP port 162.

## MIB

Management Information Base (MIB) was created to ensure that SNMP access works across manufacturers and with different client-server combinations.

It is independent format for storing device information.

A MIB is a text file in which all queryable SNMP objects of a device are listed in a standardised tree hierarchy. It contains at least one `Object Identifier` (`OID`), which, in addition to the necessary unique address and a name, also provides information about the type, access rights, and a description of the respective object. MIB files are written in the `Abstract Syntax Notation One` (`ASN.1`) based ASCII text format. The MIBs do not contain data, but they explain where to find which information and what it looks like, which returns values for the specific OID, or which data type is used.

### OID
Represents a node in a hierarchical namespace.
We can look up many MIBs for the associated OIDs in the [Object Identifier Registry](https://www.alvestrand.no/objectid/).

### SNMPv1
It's the first version of the protocol and is still in use in many small networks.
Has no built-in authentication, does not support encryption

### SNMPv2
Existed in many version. The version that still exist today is v2c (community based).
### SNMPv3
Adds authentication using username and password and transmission encryption (via pre-shared key).

### Community Strings
Can be seen as passwords that are used to determine whether the requested information can be viewed or not. 
Many organisations still use SNMPv2, as the transition to SNMPv3 can be very complex.

## Default configuration
### SNMP Daemon Config
```shell-session
cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'
```
### Dangerous settings 
| **Settings**                                     | **Description**                                                                       |
| ------------------------------------------------ | ------------------------------------------------------------------------------------- |
| `rwuser noauth`                                  | Provides access to the full OID tree without authentication.                          |
| `rwcommunity <community string> <IPv4 address>`  | Provides access to the full OID tree regardless of where the requests were sent from. |
| `rwcommunity6 <community string> <IPv6 address>` | Same access as with `rwcommunity` with the difference of using IPv6.                  |

## Footprinting the Service

Tools:
- `snmpwalk` - used to query OIDs with their information
- `onesixtyone` - can be used to brute-force the names of  the community strings
- `braa` - used to brute-force the individual OIDs and enumerate the information behind them.

```shell
snmpwalk -v2c -c public 10.129.14.128
```

```shell
onesixtyone -c /opt/useful/SecLists/Discovery/SNMP/snmp.txt 10.129.14.128
```

```shell
braa <community string>@<IP>:.1.3.6.*
```
