Intelligent Platform Management Interface is a set of standardized specifications for hardware-based host management system and monitoring. It acts as an autonomous subsystem and works independently of the  host's BIOS, CPU, firmware, and underlying operating system. Gives ability to manage and monitor systems even if they are powered off or in an unresponsive state. Does not require access  to the operating system via a login shell. Is typically used in three ways:
- Before the OS has booted to modify BIOS settings
- When the host is fully powered down
- Access to a host after a system failure
Requires a power source and a LAN connection to work correctly.
To function, IPMI requires the following components:

- Baseboard Management Controller (BMC) - A micro-controller and essential component of an IPMI
- Intelligent Chassis Management Bus (ICMB) - An interface that permits communication from one chassis to another
- Intelligent Platform Management Bus (IPMB) - extends the BMC
- IPMI Memory - stores things such as the system event log, repository store data, and more
- Communications Interfaces - local system interfaces, serial and LAN interfaces, ICMB and PCI Management Bus
## Footprinting the Service
- Port `623 UDP`
- Systems that use the IPMI protocol are called Baseboard Management Controllers (BMCs)
- Typically implemented as embedded ARM systems running Linux, and connected directly to the host's motherboard.
- Most common during internal pentest are HP iLO, Dell DRAC, and Supermicro IPMI
	- They often expose a web-based management console

```shell
sudo nmap -sU --script ipmi-version -p 623 ilo.inlanfreight.local
```

We can also use the Metasploit scanner module [IPMI Information Discovery (auxiliary/scanner/ipmi/ipmi_version)](https://www.rapid7.com/db/modules/auxiliary/scanner/ipmi/ipmi_version/).

### Default passwords

| Product Name                                        | Default Username | Default Password                        |
| --------------------------------------------------- | ---------------- | --------------------------------------- |
| **HP Integrated Lights Out (iLO)**                  | Administrator    | <factory randomized 8-character string> |
| **Dell Remote Access Card (iDRAC, DRAC)**           | root             | calvin                                  |
| **IBM Integrated Management Module (IMM)**          | USERID           | PASSW0RD (with a zero)                  |
| **Fujitsu Integrated Remote Management Controller** | admin            | admin                                   |
| **Supermicro IPMI (2.0)**                           | ADMIN            | ADMIN                                   |
| **Oracle/Sun Integrated Lights Out Manager (ILOM)** | root             | changeme                                |
| **ASUS iKVM BMC**                                   | admin            | admin                                   |

[Flaw](http://fish2.com/ipmi/remote-pw-cracking.html) in the RAKP protocol in IPMI 2.0 - Can be used to obtain password hash for ANY valid user account on the BMC
- Can be cracked using for example `Hashcat` mode `7300`
- In the event of an HP iLO using a factory default password, we can use this Hashcat mask attack command `hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u` which tries all combinations of upper case letters and numbers for an eight-character password.
To retrieve IPMI hashes, we can use the Metasploit [IPMI 2.0 RAKP Remote SHA1 Password Hash Retrieval](https://www.rapid7.com/db/modules/auxiliary/scanner/ipmi/ipmi_dumphashes/) module.