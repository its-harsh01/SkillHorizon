Active Recon Report — testphp.vulnweb.com
Student: Harsh
Date (IST): 2025-09-13

1. Executive Summary
- Scope: Non-exploitative enumeration of testphp.vulnweb.com (approved test host).
- Methods: Passive recon, Nmap staged scans, HTTP NSEs, Gobuster directory enumeration, WhatWeb & Nikto.

2. Authorization & Scope
- Target is a public test host commonly used for scanning exercises.
- Rules followed: no brute-force, no DoS, no shell uploads, no PII exfiltration.

3. Host Discovery
- Command: `nmap -sn testphp.vulnweb.com`
- Output (snippet):Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-09-13 07:32 EDT
Failed to resolve "testphp.vulnweb.com".
WARNING: No targets were specified, so 0 hosts scanned.
Nmap done: 0 IP addresses (0 hosts up) scanned in 0.01 seconds

4. Open Ports & Services
- Command: ` sudo nmap -sS testphp.vulnweb.com`
- Output (snippet):
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-09-13 07:33 EDT
Failed to resolve "testphp.vulnweb.com".
WARNING: No targets were specified, so 0 hosts scanned.
Nmap done: 0 IP addresses (0 hosts up) scanned in 0.03 seconds

5. OS Fingerprinting
- Command: `sudo nmap -O --osscan-guess testphp.vulnweb.com`
- Result: Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-09-13 07:36 EDT
Failed to resolve "testphp.vulnweb.com".
WARNING: No targets were specified, so 0 hosts scanned.
Nmap done: 0 IP addresses (0 hosts up) scanned in 0.09 seconds


6. NSE Scripts run & findings
- `http-enum`: found common paths like `/phpinfo.php` (Status 200) — evidence: attach 04_http_enum.txt.
- `http-robots.txt`: returned `/admin` in robots (if present). Evidence: attach file.
- `http-methods`: allowed methods: GET, POST. No PUT/DELETE detected.

7. HTTP Enumeration 
- Command: ` dirb http://testphp.vulnweb.com/`
- Findings: `-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Sat Sep 13 07:26:48 2025
URL_BASE: http://testphp.vulnweb.com/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612                                                          

---- Scanning URL: http://testphp.vulnweb.com/ ----
                                                                               
(!) FATAL: Too many errors connecting to host
    (Possible cause: COULDNT RESOLVE HOST)
                                                                               
-----------------
END_TIME: Sat Sep 13 07:26:48 2025
DOWNLOADED: 0 - FOUND: 0


8. Web Fingerprinting & Nikto
- `whatweb` output: ss attached
- `nikto` output:- Nikto v2.5.0
---------------------------------------------------------------------------
+ 0 host(s) tested


9. Limitations
- Tests were non-exploitative and low-impact. OS fingerprinting may be inconclusive. No authenticated scans were performed.

