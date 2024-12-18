**Configure Name Resolution**

The final piece in network configuration is typically name resolution. In other words, does the local system have the information required to translate domain names such as mheducation.com to IP addresses such as 52.7.41.60?

- Name resolution was easy when Unix was first being developed. When the predecessor to the Internet was first put into use, the worldwide computer network had four hosts, one computer at each of four different universities. It was easy to set up a static file with a list of each of their names and corresponding addresses. That file has evolved into what is known in Linux as /etc/hosts.
- But now the Internet is more complex. Although you could try to set up a database of every domain name and IP address on the Internet in the /etc/hosts file, that would take almost forever and would not be a scalable solution. That’s why most users set up connections to DNS servers. On RHEL 9, that’s still documented in the /etc/resolv.conf configuration file.
- But if you’ve configured a connection to a DNS server and systems in /etc/hosts, what’s searched first? That’s the purpose of the /etc/nsswitch.conf configuration file, which specifies the search order for various name-service databases, including hostnames.

**Hostname Configuration Files

RHEL 9 includes at least four hostname configuration files of interest: **/etc/hostname, /etc/hosts, /etc/resolv.conf, and /etc/nsswitch.conf**.

These four files, taken together, contain the local hostname, the local database of hostnames and IP addresses, the IP address of one or more DNS servers, and the order in which these databases are searched.

**/etc/nsswitch.conf

The /etc/nsswitch.conf file specifies database search priorities for everything from authentication to name services. As the name server switch file, it includes the following entry, which determines what database is searched first:

![[Pasted image 20241210110825.png]]

When a system gets a request to search for a hostname such as tester1.example.com, the preceding directive means the /etc/hosts file is searched first. If that name is not found in /etc/hosts, the next step is to search available configured DNS servers, normally using those configured in the /etc/resolv.conf file. If the name is still not found, the system looks at its hostname.

The resolver library also uses information in the /etc/host.conf file. The entry in this file is simply

`multi on`

which tells the system to return all IP addresses in /etc/hosts that are mapped to the same hostname, instead of returning only the first entry.

**Viewing and Adjusting Name Resolution Sources and Order**

The _nsswitch.conf_ file under _/etc_ directs the lookup utilities to the correct source to get hostname information. In the presence of multiple sources, this file also identifies the order in which to consult them and an action to be taken next.

There are four keywords—success, notfound, unavail, and tryagain—that oversee this behavior

| **Keyword** | **Meaning**                                                       | **Default Action**                  |
| ----------- | ----------------------------------------------------------------- | ----------------------------------- |
| success     | Information found in source and provided to the requester         | return (do not try the next source) |
| notfound    | Information not found in source                                   | continue (try the next source)      |
| unavail     | Source down or not responding; service disabled or not configured | continue (try the next source)      |
| tryagain    | Source busy, retry later                                          | continue (try the next source)      |

Example:

The following example entry shows the syntax of a relevant entry from the nsswitch.conf file. It shows two sources for name resolution: files (/etc/hosts) and DNS (/etc/resolv.conf).
hosts:	files	dns

Based on the default behavior, the search will terminate if the requested information is found in the hosts table. However, you can alter this behavior and instruct the lookup programs to return if the requested information is not found there. The modified entry will look like:

hosts:	files \[notfound=return\]	dns

This altered entry will ignore the DNS.

**/etc/hosts**

The /etc/hosts file is a static database of hostnames/FQDNs and IP addresses. It’s suitable for small, relatively static networks However, using it for networks where there are frequent changes can be a pain. Every time a system is added or removed, you’ll have to change this file—not only on the local system but also on every other system on that network.

The /etc/hosts file is well suited to the local virtual machines. A simple version of the file might include the following entries:

In some cases, you may want to set up multiple entries for an IP address. For example, the following entries could be added to specify the IP addresses for web and FTP servers:

![Images](https://learning.oreilly.com/api/v2/epubs/urn:orm:book:9781260462081/files/f0110-03.jpg)

- Setting up an /etc/hosts file is easy; just make sure that it contains at least two columns. The first column has the IP address of the specific host, and the second column specifies the hostname The hostname can be provided as a short name (like server1) or as an FQDN. In an FQDN, the hostname as well as the complete DNS name are included, as in server1.example.com.
- If a host has more than one name, like a short name and a fully qualified DNS name, you can specify both of them in /etc/hosts. In that case, the second column must contain the FQDN, and the third column can contain the

The _nsswitch.conf_ file under _/etc_ directs the lookup utilities to the correct source to get hostname information. In the presence of multiple sources, this file also identifies the order in which to consult them and an action to be taken next. alias.

![[Pasted image 20241210112149.png]]

**Hostnames**

Because hostnames are used to access servers and the services they’re offering, it is important to know how to set the system hostname.
- A hostname typically consists of different parts.
- These are the name of the host and the Domain Name System (DNS) domain in which the host resides. These two parts together make up the fully qualified domain name (FQDN), which looks like server1.example.com.
- It is good practice to always specify an FQDN, and not just the hostname, because the FQDN provides a unique identity on the Internet.

There are different ways to change the hostname:

- Use **nmtui** and select the option **Change Hostname**.
- Use **hostnamectl set-hostname**.
- Edit the contents of the configuration file /etc/hostname.

To configure the hostname with **hostnamectl**, you can use a command like **hostnamectl set-hostname myhost.example.com**. After setting the hostname, you can use **hostnamectl status** to show the current hostname.

![[Pasted image 20241210113934.png]]

When using **hostnamectl status**, you see not only information about the hostname but also information about the Linux kernel, virtualization type, and much more.

Alternatively, you can set the hostname using the **nmtui** interface.

![[Pasted image 20241210114014.png]]
