Domain Name System is an OS- and hardware-independent network service employed for determining the IP address of a system when its hostname is known, and vice versa. This mechanism is implemented to map human-friendly hostnames to their assigned numeric IP addresses by consulting one or more servers offering the hostname resolution service.

This service has been used on the Internet and corporate networks as the de facto standard for this purpose. DNS clients use this service to communicate with remote systems. There are several lookup programs that use DNS to obtain information.

![[Pasted image 20241210114456.png]]

**DNS and Name Resolution**

_Domain Name System_ (DNS) is an inverted tree-like structure employed on the Internet and private networks (including home and corporate networks) as the de facto standard for resolving hostnames to their numeric IP addresses.
- DNS is platform-independent with support integrated in every operating system.
- DNS is also referred to as BIND, _Berkeley Internet Name Domain_, which is an implementation of DNS, and it has been the most popular DNS application in use.
- _Name resolution_ is the technique that uses DNS/BIND for hostname lookups.

**DNS Name Space and Domains**

- The DNS _name space_ is a hierarchical organization of all the domains on the Internet.
- The root of the name space is represented by a period (.). The hierarchy below the root (.) denotes the _top-level domains_ (TLDs) with names such as .com, .net, .edu, .org, .gov, .ca, and .de.
- A DNS _domain_ is a collection of one or more systems.
- Subdomains fall under their parent domains and are separated by a period (.). For example, redhat.com is a second-level subdomain that falls under .com, and bugzilla.redhat.com is a third-level subdomain that falls under redhat.com.

![[Pasted image 20241210125714.png]]

At the deepest level of the hierarchy are the _leaves_ (systems, nodes, or any device with an IP address) of the name space. For example, a network switch _net01_ in _.travel.gc.ca_ subdomain will be known as _net01.travel.gc.ca_. If a period (.) is added to the end of this name to look like _net01.travel.gc.ca._, it will be referred to as the _Fully Qualified Domain Name_ (FQDN) for _net01_.

**DNS Roles**

From a DNS perspective, a system can be configured to operate as a primary server, secondary server, or client. A DNS server is also referred to as a _nameserver_.

- A _primary server_ is responsible for its domain (or subdomain). It maintains a master database of all the hostnames and their associated IP addresses that are included in that domain. All changes in the database are done on this server. 
- Each domain must have one primary server with one or more optional _secondary_ servers for load balancing and redundancy.
- A secondary server also stores an updated copy of the master database, and it continues to provide name resolution service in the event the primary server becomes unavailable or inaccessible.

A _DNS client_ queries nameservers for name lookups. Every system with access to the Internet or other external networks will have the DNS client functionality configured and operational. Setting up DNS client on Linux involves two text files.

**Understanding Resolver Configuration File**

The _resolv.conf_ file under _/etc_ is the DNS resolver configuration file where information to support hostname lookups is defined. This file may be edited manually with a text editor. It is referenced by resolver utilities to construct and transmit queries. There are three key directives set in this file—domain, nameserver, and search.

| **Directive** | **Description**                                                                                                                                                                                                  |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| domain        | Identifies the default domain name to be searched for queries                                                                                                                                                    |
| nameserver    | Declares up to three DNS server IP addresses to be queried one at a time in the order in which they are listed. Nameserver entries may be defined as separate line items with the directive or on a single line. |
| search        | Specifies up to six domain names, of which the first must be the local domain. No need to define the domain directive if the search directive is used.                                                           |

A sample entry showing the syntax is provided below for reference:

| domain     | [example.com](http://example.com)                                                                                                       |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| search     | [example.net](http://example.net) [example.org](http://example.org) [example.edu](http://example.edu) [example.gov](http://example.gov) |
| nameserver | 192.168.0.1 8.8.8.8 8.8.4.4                                                                                                             |
How to configure DNS

**To specify which DNS server should be used, set the DNS server using nmcli or nmtui. The NetworkManager configuration stores the DNS information in the configuration file for the network connection, which is in /etc/sysconfig/network-scripts, and from there pushes the configuration to the /etc/resolv.conf file, which is used for DNS name server resolving. Do not edit /etc/resolv.conf directly, as it will be overwritten the next time you restart NetworkManager.**

It is recommended to always set up at least two DNS name servers to be contacted. If the first name server does not answer, the second name server is contacted. To specify which DNS name servers you want to use, you have a few different options:

- Use **nmtui** to set the DNS name servers.

![[Pasted image 20241210131742.png]]

- Use a DHCP server that is configured to hand out the address of the DNS name server.
- Use **nmcli con mod \<connection-id> \[+]ipv4.dns \<ip-of-dns>**.

Notice that if your computer is configured to get the network configuration from a DHCP server, the DNS server is also set via the DHCP server. If you do not want this to happen, use the following command: **nmcli con mod \<con-name> ipv4.ignore-auto-dns yes**.

To verify hostname resolution, you can use the **getent hosts \<servername>** command. This command searches in both /etc/hosts and DNS to resolve the hostname that has been specified.

**Performing Name Resolution with dig**

_dig_ (_domain information groper_) is a DNS lookup utility. It queries the nameserver specified at the command line or consults the _resolv.conf_ file to determine the nameservers to be queried. This tool may be used to troubleshoot DNS issues due to its flexibility and verbosity.

To get the IP for redhat.com using the nameserver listed in the resolv.conf file:

![[Pasted image 20241210132108.png]]

The output shows the total time (20 milliseconds) it took to get the result, the IP addresses (52.200.142.250 and 34.235.198.240) of redhat.com, the nameserver IPv6 (2001:1970:xxxxxx) used for the query, query timestamp, the size of the received message (71 bytes), and other information.

To perform a reverse lookup on the redhat.com IP (52.200.142.250), use the -x option with the command:

![[Pasted image 20241210132152.png]]
Reference the command’s manual pages for details and options.

**Performing Name Resolution with nslookup**

_nslookup_ queries the nameservers listed in the _resolv.conf_ file or specified at the command line. The following shows a few usage examples.

To get the IP for redhat.com using nameserver 8.8.8.8 instead of the nameserver defined in resolv.conf:

![[Pasted image 20241210132257.png]]

To perform a reverse lookup on the IP of _[redhat.com](http://redhat.com)_ using the nameserver from the resolver configuration file:

![](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781835887325/files/html/images/417_3.jpg)

Consult the command’s manual pages on how to use it in interactive mode.