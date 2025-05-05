
#  Internet Network Discovery

---

##  Google Dorking

Attackers use advanced search operators to gather publicly available information from websites.

[Google Advanced Search](https://www.google.com/advanced_search)

### Common Google Dorks:

- `intext:`  
  - Example: `intext:password filetype:xlsx` → Shows pages with "password" in the text and of type `.xlsx`

- `intitle:`  
  - Example: `intitle:"index of /backup"` → Pages with the phrase in their title

- `inurl:`  
  - Example: `inurl:admin` → Pages with "admin" in the URL

- `filetype:`  
  - Example: `filetype:pdf intext:confidential` → PDF files containing the word "confidential"

- `site:`  
  - Example: `site:example.com intext:login` → Results only from `example.com`

- **Contact Enumeration:**  
  Use keywords like `"mail"`, `"tel"`, `"fax"` in quotes to find contact information

---

## Shodan

Shodan is a search engine for Internet-connected devices and services. It provides information such as hostnames, open ports, services, and banners.

###  Common Filters:

| Filter     | Example                             | Description                                      |
|------------|-------------------------------------|--------------------------------------------------|
| `city`     | `city:"london"`                     | Sendmail servers in London                       |
| `country`  | `country:DE nginx`                  | Nginx servers in Germany                         |
| `geo`      | `geo:32.8,-117,50 apache`           | Apache servers within 50km of San Diego          |
| `hostname` | `hostname:sslvpn`                   | Hostnames containing "sslvpn"                    |
| `net`      | `net:216.219.0.0/16`                | Data for the specified IP range                  |
| `os`       | `os:linux jboss`                    | JBoss running on Linux                           |
| `port`     | `port:5060 avaya`                   | Avaya SIP VoIP endpoints                         |
| `before`   | `before:18/1/2010 nginx`            | Found before January 18, 2010                    |
| `after`    | `after:22/3/2010 before:4/6/2010`   | Found between March 22 and June 4, 2010          |

---

##  DomainTools

DomainTools provides intelligence about domains and IPs.

- **Reverse IP WHOIS:** See all IP ranges owned by an entity  
- **Domain WHOIS History:** View historical registrants of a domain  
- **Reverse IP Lookup:** Find domains hosted on a given IP  
- **Reverse NS Lookup:** Find domains using a specific name server  
- **Reverse MX Lookup:** Discover domains using a particular mail server  

---

##  Manual WHOIS Querying

Use `whois` command to query domain registrars and get registration data.

```bash
whois <target_site>
```

Additional options:

```bash
whois -a "z / <target>"
whois -A "<target>"
```

---

##  DNS Querying

DNS queries reveal key infrastructure data. Tools like `dig`, `nslookup`, and `nmap` are commonly used.

###  Common DNS Record Types:

| Record | Description          | Reveals                                         |
|--------|----------------------|-------------------------------------------------|
| SOA    | Start of authority   | Primary source of the DNS zone                  |
| NS     | Name server          | Authoritative DNS servers                       |
| A      | IPv4 address         | IPv4 addresses of a hostname                    |
| AAAA   | IPv6 address         | IPv6 addresses of a hostname                    |
| PTR    | Pointer              | Reverse mapping from IP to hostname             |
| CNAME  | Canonical name       | Alias of another hostname                       |
| MX     | Mail exchange        | Mail servers used by a domain                   |
| HINFO  | Host info            | Operating system or hardware details            |
| SRV    | Service locator      | Services like LDAP, Kerberos, SIP, XMPP         |
| TXT    | Text                 | SPF, DKIM, and security policies                |

###  Useful Commands:

- General info:
```bash
nslookup
> set querytype=any
> <target>
```

- Automated enumeration:
```bash
dnsenum <target>
```

- Nmap DNS SRV enum:
```bash
nmap --script dns-srv-enum --script-args dns-srv-enum.domain=<target>
```

- Zone Transfer Attempt:
```bash
dig whois.net ns +short
dig @<nameserver> whois.net axfr
```

- Dictionary Attack with Fierce:
```bash
fierce -dns <target>
```

- Detect private addresses using `dig`:
```bash
dig @ns3.isc-sns.info -f /tmp/paypal.txt +noall +answer | awk '{printf("%s %s\n",$5,$1);}' | grep -E '^(10\.)'
```

- Reverse DNS Sweeping with `nmap`:
```bash
nmap -sL <target_ip> | grep "(" | awk '{printf("%s %s\n",$5,$6);}'
```

---

##  Recon Automation Tools

For advanced reconnaissance, consider using tools like:

- [`theHarvester`](https://github.com/laramies/theHarvester)
- [`Amass`](https://github.com/OWASP/Amass)
- [`Spiderfoot`](https://github.com/smicallef/spiderfoot)
- [`Recon-ng`](https://github.com/lanmaster53/recon-ng)

---


