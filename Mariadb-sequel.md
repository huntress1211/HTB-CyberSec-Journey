🚩 HTB: Sequel - Tier 1
Date: 2026-01-15

Machine Type: Linux

Difficulty: Very Easy

Vulnerability: Misconfigured Database (No Password for Root)

Service: MySQL / MariaDB

🔍 1. Enumeration
Nmap Scan
The goal was to identify open ports and services running on the target.

Bash

sudo nmap -sC -sV <TARGET_IP>
Port 3306 (MySQL): Open, running MariaDB.

Discovery: Unlike the previous machine "Appointment" which had a web interface, this machine exposes the database service directly to the internet.

🛡️ 2. Analysis & Foothold
The write-up suggested checking for common misconfigurations, specifically passwordless login for the administrative user (root).

Connecting to the Database:
Used the following command to attempt a direct connection:

Bash

mysql -h <TARGET_IP> -u root
-h: Specifies the host IP.

-u root: Specifies the username.

Result: Successfully logged into the MariaDB shell without being prompted for a password. This is a critical security flaw.

🚀 3. Database Navigation & Exploitation
Once inside the MySQL shell, I used standard SQL queries to navigate through the data:

Listing Databases: SHOW databases;

Identified a unique database named htb alongside default ones.

Selecting the Database: USE htb;

Listing Tables: SHOW tables;

Found two tables: config and users.

Extracting the Flag: SELECT * FROM config;

This command dumped the contents of the table, revealing the flag.

🚩 4. Final Result
The flag was successfully retrieved from the config table.

Root Flag: 

🧠 5. Key Learnings
Service Misconfiguration: Exposing a database port (3306) to the public without a strong password or firewall is extremely dangerous.

SQL Proficiency: Practiced basic database navigation commands like SHOW, USE, and SELECT.

Default Databases: Learned that information_schema, mysql, and performance_schema are standard, and hackers should look for unique/custom databases.
