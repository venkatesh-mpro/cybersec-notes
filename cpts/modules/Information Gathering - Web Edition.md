## Reconnaissance Techniques

### Active Reconnaissance

In active reconnaissance, the attacker directly interacts with the target system to gather information. This interaction can take various forms:

| Technique              | Description                                                                                   | Example                                                                                                                               | Tools                                                      | Risk of Detection                                                                                                  |
| :--------------------- | :-------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------ | :--------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------- |
| Port Scanning          | Identifying open ports and services running on the target.                                    | Using Nmap to scan a web server for open ports like 80 (HTTP) and 443 (HTTPS).                                                        | Nmap, Masscan, Unicornscan                                 | High: Direct interaction with the target can trigger intrusion detection systems (IDS) and firewalls.              |
| Vulnerability Scanning | Probing the target for known vulnerabilities, such as outdated software or misconfigurations. | Running Nessus against a web application to check for SQL injection flaws or cross-site scripting (XSS) vulnerabilities.              | Nessus, OpenVAS, Nikto                                     | High: Vulnerability scanners send exploit payloads that security solutions can detect.                             |
| Network Mapping        | Mapping the target's network topology, including connected devices and their relationships.   | Using traceroute to determine the path packets take to reach the target server, revealing potential network hops and infrastructure.  | Traceroute, Nmap                                           | Medium to High: Excessive or unusual network traffic can raise suspicion.                                          |
| Banner Grabbing        | Retrieving information from banners displayed by services running on the target.              | Connecting to a web server on port 80 and examining the HTTP banner to identify the web server software and version.                  | Netcat, curl                                               | Low: Banner grabbing typically involves minimal interaction but can still be logged.                               |
| OS Fingerprinting      | Identifying the operating system running on the target.                                       | Using Nmap's OS detection capabilities (-O) to determine if the target is running Windows, Linux, or another OS.                      | Nmap, Xprobe2                                              | Low: OS fingerprinting is usually passive, but some advanced techniques can be detected.                           |
| Service Enumeration    | Determining the specific versions of services running on open ports.                          | Using Nmap's service version detection (-sV) to determine if a web server is running Apache 2.4.50 or Nginx 1.18.0.                   | Nmap                                                       | Low: Similar to banner grabbing, service enumeration can be logged but is less likely to trigger alerts.           |
| Web Spidering          | Crawling the target website to identify web pages, directories, and files.                    | Running a web crawler like Burp Suite Spider or OWASP ZAP Spider to map out the structure of a website and discover hidden resources. | Burp Suite Spider, OWASP ZAP Spider, Scrapy (customisable) | Low to Medium: Can be detected if the crawler's behaviour is not carefully configured to mimic legitimate traffic. |

### Passive Reconnaissance

In contrast, passive reconnaissance involves gathering information about the target without directly interacting with it. This relies on analysing publicly available information and resources, such as:

| Technique             | Description                                                                                                                     | Example                                                                                                                                           | Tools                                                                   | Risk of Detection |
| :-------------------- | :------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------------- | :---------------- |
| Search Engine Queries | Utilising search engines to uncover information about the target, including websites, social media profiles, and news articles. | Searching Google for "[Target Name] employees" to find employee information or social media profiles.                                             | Google, DuckDuckGo, Bing, and specialised search engines (e.g., Shodan) | Very Low          |
| WHOIS Lookups         | Querying WHOIS databases to retrieve domain registration details.                                                               | Performing a WHOIS lookup on a target domain to find the registrant's name, contact information, and name servers.                                | whois command-line tool, online WHOIS lookup services                   | Very Low          |
| DNS                   | Analysing DNS records to identify subdomains, mail servers, and other infrastructure.                                           | Using dig to enumerate subdomains of a target domain.                                                                                             | dig, nslookup, host, dnsenum, fierce, dnsrecon                          | Very Low          |
| Web Archive Analysis  | Examining historical snapshots of the target's website to identify changes, vulnerabilities, or hidden information.             | Using the Wayback Machine to view past versions of a target website to see how it has changed over time.                                          | Wayback Machine                                                         | Very Low          |
| Social Media Analysis | Gathering information from social media platforms like LinkedIn, Twitter, or Facebook.                                          | Searching LinkedIn for employees of a target organisation to learn about their roles, responsibilities, and potential social engineering targets. | LinkedIn, Twitter, Facebook, specialised OSINT tools                    | Very Low          |
| Code Repositories     | Analysing publicly accessible code repositories like GitHub for exposed credentials or vulnerabilities.                         | Searching GitHub for code snippets or repositories related to the target that might contain sensitive information or code vulnerabilities.        | GitHub, GitLab                                                          | Very Low          |

## Additional Information

### History of WHOIS Records

* [https://whoisfreaks.com/](https://whoisfreaks.com/)

### Hosts File Locations

The `hosts` file is located in:
* `C:\Windows\System32\drivers\etc\hosts` on Windows
* `/etc/hosts` on Linux and MacOS.

`127.0.0.1       localhost 192.168.1.10    devserver.local`


**Example entries:**

| DNS Concept               | Description                                                                      | Example                                           |
| ------------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------- |
| Domain Name               | A human-readable label for a website or other internet resource.                 | www.example.com                                   |
| IP Address                | A unique numerical identifier assigned to each device connected to the internet. | 192.0.2.1                                         |
| DNS Resolver              | A server that translates domain names into IP addresses.                         | Your ISP's DNS server or Google DNS (8.8.8.8)     |
| Root Name Server          | The top-level servers in the DNS hierarchy.                                      | 13 root servers named A-M: a.root-servers.net     |
| TLD Name Server           | Servers responsible for specific top-level domains (e.g., .com, .org).           | Verisign for .com, PIR for .org                   |
| Authoritative Name Server | The server that holds the actual IP address for a domain.                        | Managed by hosting providers or domain registrars |
| DNS Record Types          | Different types of information stored in DNS.                                    | A, AAAA, CNAME, MX, NS, TXT, etc.                 |

| Record Type | Full Name                 | Description                                                         | Zone File Example                                                                          |
| ----------- | ------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| A           | Address Record            | Maps a hostname to its IPv4 address.                                | www.example.com. IN A 192.0.2.1                                                            |
| AAAA        | IPv6 Address Record       | Maps a hostname to its IPv6 address.                                | www.example.com. IN AAAA 2001:db8:85a3::8a2e:370:7334                                      |
| CNAME       | Canonical Name Record     | Creates an alias for a hostname, pointing it to another hostname.   | blog.example.com. IN CNAME webserver.example.net.                                          |
| MX          | Mail Exchange Record      | Specifies the mail server(s) responsible for handling email.        | example.com. IN MX 10 mail.example.com.                                                    |
| NS          | Name Server Record        | Delegates a DNS zone to a specific authoritative name server.       | example.com. IN NS ns1.example.com.                                                        |
| TXT         | Text Record               | Stores arbitrary text info, often for domain verification/security. | example.com. IN TXT "v=spf1 mx -all"                                                       |
| SOA         | Start of Authority Record | Specifies admin info about a DNS zone.                              | example.com. IN SOA ns1.example.com. admin.example.com. 2024060301 10800 3600 604800 86400 |
| SRV         | Service Record            | Defines the hostname and port number for specific services.         | _sip._udp.example.com. IN SRV 10 5 5060 sipserver.example.com.                             |
| PTR         | Pointer Record            | Used for reverse DNS lookups, mapping IP to hostname.               | 1.2.0.192.in-addr.arpa. IN PTR www.example.com.                                            |


