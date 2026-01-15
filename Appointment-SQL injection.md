🚩 HTB: Appointment - Tier 1
Date: 2026-01-15

Machine Type: Linux

Difficulty: Very Easy

Vulnerability: SQL Injection (Authentication Bypass)

OWASP Top 10: A03:2021-Injection

🔍 1. Enumeration
Nmap Scan
The process started with a service and version detection scan to identify open ports:

Bash

nmap -sC -sV <TARGET_IP>
Port 80 (HTTP): Open, running Apache httpd 2.4.38 ((Debian)).

Discovery: The scan confirmed a web application is hosted on this port.

🛡️ 2. Web Analysis
Upon navigating to the target IP in the browser, a Login Page was presented.

Attempted common credentials (admin:admin), but they failed.

Identified the potential for SQL Injection in the login fields due to a lack of input sanitization.

🚀 3. Exploitation (SQL Injection)
The goal was to bypass the authentication mechanism. By using a single quote (') to break the SQL query and a hashtag (#) to comment out the rest of the query, I bypassed the password check.

Payload Used:
Username: admin'#

Password: password (any random string)

The Logic:
The backend SQL query likely looked like this: SELECT * FROM users WHERE username='admin'#' AND password='...'

Everything after the # was ignored by the database, allowing me to log in as the admin user without a valid password.

🚩 4. Capture The Flag
After successful login, I was redirected to the dashboard which displayed:

Message: "Congratulations!"

Root Flag:e3d0796d002a446c0e622226f42e9672

🧠 5. Key Learnings
Security Misconfiguration: Discovered how failing to sanitize user input leads to critical vulnerabilities.

Nmap Scripting Engine (NSE): Utilized -sC to get deeper insights into the web server.

SQLi Prevention: Learned that developers should use Parameterized Queries to prevent this type of attack.
