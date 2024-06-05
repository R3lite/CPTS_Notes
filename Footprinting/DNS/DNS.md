Domain Name System is a system for resolving computer names into IP addresses, and it does not have a central database. There are several types of DNS servers that are used worldwide:

| **Server Type**                | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `DNS Root Server`              | The root servers of the DNS are responsible for the top-level domains (`TLD`). As the last instance, they are only requested if the name server does not respond. Thus, a root server is a central interface between users and content on the Internet, as it links domain and IP address. The [Internet Corporation for Assigned Names and Numbers](https://www.icann.org/) (`ICANN`) coordinates the work of the root name servers. There are `13` such root servers around the globe. |
| `Authoritative Nameserver`     | Authoritative name servers hold authority for a particular zone. They only answer queries from their area of responsibility, and their information is binding. If an authoritative name server cannot answer a client's query, the root name server takes over at that point.                                                                                                                                                                                                            |
| `Non-authoritative Nameserver` | Non-authoritative name servers are not responsible for a particular DNS zone. Instead, they collect information on specific DNS zones themselves, which is done using recursive or iterative DNS querying.                                                                                                                                                                                                                                                                               |
| `Caching DNS Server`           | Caching DNS servers cache information from other name servers for a specified period. The authoritative name server determines the duration of this storage.                                                                                                                                                                                                                                                                                                                             |
| `Forwarding Server`            | Forwarding servers perform only one function: they forward DNS queries to another DNS server.                                                                                                                                                                                                                                                                                                                                                                                            |
| `Resolver`                     | Resolvers are not authoritative DNS servers but perform name resolution locally in the computer or router.                                                                                                                                                                                                                                                                                                                                                                               |
DNS is mainly unencrypted. 
Devices on the local WLAN and Internet providers can therefore hack in and spy on DNS queries. 
To solve this we can use: 
- `DNS over TLS` (`DoT`)
- `DNS over HTTPS` (`DoH`)
- `DNSCrypt`
![[Pasted image 20240517173446.png]]

| **DNS Record** | **Description**                                                                                                                                                                                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `A`            | Returns an IPv4 address of the requested domain as a result.                                                                                                                                                                                      |
| `AAAA`         | Returns an IPv6 address of the requested domain.                                                                                                                                                                                                  |
| `MX`           | Returns the responsible mail servers as a result.                                                                                                                                                                                                 |
| `NS`           | Returns the DNS servers (nameservers) of the domain.                                                                                                                                                                                              |
| `TXT`          | This record can contain various information. The all-rounder can be used, e.g., to validate the Google Search Console or validate SSL certificates. In addition, SPF and DMARC entries are set to validate mail traffic and protect it from spam. |
| `CNAME`        | This record serves as an alias. If the domain www.hackthebox.eu should point to the same IP, and we create an A record for one and a CNAME record for the other.                                                                                  |
| `PTR`          | The PTR record works the other way around (reverse lookup). It converts IP addresses into valid domain names.                                                                                                                                     |
| `SOA`          | Provides information about the corresponding DNS zone and email address of the administrative contact.                                                                                                                                            |
The `SOA` record is located in a domain's zone file and specifies who is responsible for the operation of the domain and how DNS information for the domain is managed.

```sh
dig soa www.inlanefreight.com
```

All DNS servers work with three different types of configuration files:

1. local DNS configuration files
2. zone files
3. reverse name resolution files
Commonly used DNS server on Linux is [Bind9](https://www.isc.org/bind/) with local configuration file `named.conf`.

Used configuration files are usually:
- named.conf.local
- named.conf.options
- named.conf.log

In `named.conf.local` file we define different zones. These zones are divided into individual files, which in most cases are mainly intended for one domain only. Exception: ISP and public DNS servers.
In a `zone file` there must be precisely one `SOA` record and at least one `NS` record. If there's a syntax error in a `zone file` name server behaves as if this file did not exists and it would respond to DNS queries with `SERVFAIL` error.

For the IP address to be resolved from the `Fully Qualified Domain Name` (`FQDN`), the DNS server must have a reverse lookup file. In this file, the computer name (`FQDN`) is assigned to the last octet of an IP address, which corresponds to the respective host, using a `PTR` record. The `PTR` records are responsible for the reverse translation of IP addresses into names, as we have already seen in the above table.

Most popular DNS attacks [here](https://securitytrails.com/blog/most-popular-types-dns-attacks)

### Dangerous settings 

|**Option**|**Description**|
|---|---|
|`allow-query`|Defines which hosts are allowed to send requests to the DNS server.|
|`allow-recursion`|Defines which hosts are allowed to send recursive requests to the DNS server.|
|`allow-transfer`|Defines which hosts are allowed to receive zone transfers from the DNS server.|
|`zone-statistics`|Collects statistical data of zones.|
### Footprinting the Service

We do this using the NS record and the specification of the DNS server we want to query using the `@` character.
```shell
dig ns inlanefreight.htb @10.129.14.128
```

Sometimes it is also possible to query a DNS server's version using a class CHAOS query and type TXT. However, this entry must exist on the DNS server.

```shell
dig CH TXT version.bind 10.129.120.85
```

We can also use option any to view all available records.

```shell
dig any inlanefreight.htb @10.129.14.128
```

`Zone transfer` refers to the transfer of zones to another server in DNS, which generally happens over TCP port 53. This procedure is abbreviated `Asynchronous Full Transfer Zone` (`AXFR`).
Synchronisation between the servers is realised by zone  transfer. Using a secret key `rndc-key` the servers make sure that they communicate with their own master or slave.

- `primary` - DNS server with original data of a zone
- `secondary` - backup, for some TLDs it's mandatory to have a backup

```shell
dig axfr inlanefreight.htb @10.129.14.128
```

### Subdomain brute-forcing
```shell
for sub in $(cat /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.inlanefreight.htb @10.129.14.128 | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done
```
### Using a [DNSenum](https://github.com/fwaeytens/dnsenum) tool.
```shell
dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/fierce-hostlists.txt --threads 90 dev.inlanefreight.htb
```

## DNS lookup utility `host`

```sh
host -t ns zonetransfer.me
host -l zonetransfer.me nsztm1.digi.ninja
```

## Automated tool `dnsrecon`
```sh
dnsrecon -d zonetransfer.me -t axfr
```