🚩 Hack The Box: Crocodile (Writeup)
Machine Name: Crocodile

Difficulty: Very Easy (Tier 1)

Platform: Hack The Box Starting Point

📝 Introduction
Crocodile is a Tier 1 machine that builds upon basic FTP skills but adds a layer of Web Enumeration. The objective is to use insecure FTP access to find hidden credentials and then use those to access a protected web admin panel.

🔍 Step 1: Enumeration
I began by scanning the target machine to identify open ports and the specific versions of services running.

Command: nmap -sC -sV {TARGET_IP}

Findings: - Port 21: FTP (vsftpd 3.0.3) - Anonymous login allowed.

Port 80: HTTP (Apache httpd 2.4.41).

Concept: The -sC switch runs default scripts, which automatically detected that we could enter the FTP server without a private account.

🚀 Step 2: Exploitation (FTP Data Extraction)
Since the FTP server allowed anonymous access, I logged in to see if any sensitive configuration files were left behind.

I connected to the FTP service:

ftp {TARGET_IP}

Username: anonymous | Password: [Blank]

Download Files: I found two interesting files and downloaded them:

get allowed.userlist

get allowed.userlist.passwd

Result: I now had a list of potential usernames and passwords to use against the web server.

🌐 Step 3: Web Directory Brute-forcing
The web server on Port 80 looked like a standard landing page. I used Gobuster to find hidden directories or login pages.

Command: gobuster dir -u http://{TARGET_IP}/ -w /usr/share/wordlists/dirb/common.txt -x php

Finding: The scan discovered a hidden page: /login.php.

🏆 Step 4: Capturing the Flag
With the login page found and credentials in hand, I proceeded to gain access.

Access Login Page: Opened http://{TARGET_IP}/login.php in the browser.

Credential Stuffing: Tried the admin username and the corresponding password r3uS3d_Pr0t0c0l from the downloaded files.

Success: The login worked, redirecting me to the admin dashboard.

Flag: ********************************

💡 Key Learnings
Credential Reuse: Often, credentials found in one service (like FTP) are reused for others (like Web Admin panels).

Hidden Directories: Web developers often hide admin pages instead of properly securing them; tools like Gobuster are essential to find them.

Service Cross-Referencing: Information gathered from Port 21 was the "key" to unlocking the service on Port 80.

3rd machine down, moving towards the target of 10! 🚀🐊
