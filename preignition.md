Sorry, my bad! Main ne mix kar diya tha. Ye raha bilkul wahi format jo aapne Dancing ke liye use kiya tha, lekin ab Preignition ke liye pure English mein:

🚩 Hack The Box: Preignition (Writeup)
Machine Name: Preignition

Difficulty: Very Easy (Tier 0)

Platform: Hack The Box Starting Point

📝 Introduction
Preignition is a Tier 0 machine that introduces the concept of Web Enumeration and Directory Brute-forcing. The goal is to discover hidden directories on a web server that are not publicly linked and exploit weak administrative credentials.

🔍 Step 1: Enumeration
The first step was to identify open ports and services running on the target machine using Nmap.

Command: nmap -sV {TARGET_IP}

Findings: The scan revealed that Port 80/tcp is open, running the nginx 1.14.2 web server.

🚀 Step 2: Exploitation (Directory Brute-forcing)
Upon visiting the IP in a browser, only a default nginx page was visible. To find hidden administrative pages, I used a tool called gobuster.

Running Gobuster:

Command: gobuster dir -u http://{TARGET_IP} -w /usr/share/wordlists/dirb/common.txt

Action: This tool tests thousands of common directory names against the web server.

Results: I discovered a hidden page: /admin.php (Status: 200).

Accessing the Page: I navigated to http://{TARGET_IP}/admin.php in the browser, which presented a login interface.

🏆 Step 3: Finding the Flag
Many administrative panels are left with their factory settings. I attempted to log in using Default Credentials.

Login Credentials:

Username: admin

Password: admin

Result: Access Granted!

Retrieving the Flag: The flag was displayed directly on the admin dashboard after the successful login.

Flag: [Flag Successfully Captured]

💡 Key Learnings
Directory Busting: Tools like gobuster are essential for finding "security through obscurity" paths that aren't linked on the homepage.

Default Credentials: Leaving default passwords like admin:admin on a production server is a critical security risk.

HTTP Status Codes: Learned that a 200 OK status confirms the existence of a file or directory.
