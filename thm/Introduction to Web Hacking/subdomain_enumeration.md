Subdomain Enumeration
==

Types of subdomain enumeration
--
- brute force
- osint
- virtual hosts

OSINT - SSL/TLS Certificates
--
- SSL: Secure Sockets Layer
- TLS: Transport Layer Security
- CA: Certificate Authority
- CT: Certificate Transparency
  - CT logs: publicly accessible logs of every SSL/TLS certficate crated for a domain
    - [crt.sh](https://crt.sh/)
    - [Certificate Transparency Search Tool](https://ui.ctsearch.entrust.com/ui/ctsearchui)
  
OSINT - Search Engines
--
Example to find tryhackme.com subdomains on Google: 

    -site:www.tryhackme.com  site:*.tryhackme.com

DNS Bruteforce
---
- Bruteforce DNS (Domain Name System) enumeration is the method of trying tens, hundreds, thousands or even millions of different possible subdomains from a pre-defined list of commonly used subdomains. 
- Tool: dnsrecon

OSINT - [Sublis3r](https://github.com/aboul3la/Sublist3r)
--
To speed up the process of OSINT subdomain discovery, we can automate the above methods with the help of tools like Sublist3r.

Virtual Hosts
--
Some subdomains aren't always hosted in publically accessible DNS results, such as development versions of a web application or administration portals. Instead, the DNS record could be kept on a private DNS server or recorded on the developer's machines in their /etc/hosts file (or c:\windows\system32\drivers\etc\hosts file for Windows users) which maps domain names to IP addresses.

Because web servers can host multiple websites from one server when a website is requested from a client, the server knows which website the client wants from the Host header. We can utilise this host header by making changes to it and monitoring the response to see if we've discovered a new website.

Example:

    ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://x.x.x.x

    ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://x.x.x.x -fs {size}