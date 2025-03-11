Content Discovery
===
Content Discovery Methods
- manually
- automated
- osint

Manually Discovery
--
- robots.txt
- favicon
  - md5sum
  - [OWASP Favicon DB](https://wiki.owasp.org/index.php/OWASP_favicon_database)
- sitemap.xml
- HTTP Headers
- Framework Stack
  - check source for hints to used framework
  - check framework docs for default credentials

OSINT
--
- [Google Hacking](https://en.wikipedia.org/wiki/Google_hacking) / Dorking
  - site:tryhackme.com
  - inurl:admin
  - filetype:pdf
  - intitle:admin
- Wappalyzer.com
- Wayback Machine
- Github
- S3 Buckets
  
Automated Discovery
--
- wordlists (e.g. https://github.com/danielmiessler/SecLists)
  - password
  - commonly used directory and file names
- automation tools
  - fuff
  - dirb
  - gobuster
  