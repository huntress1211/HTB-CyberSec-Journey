🚩 Hack The Box: Mongod (Writeup)
Machine Name: Mongod

Difficulty: Very Easy (Tier 0)

Platform: Hack The Box Starting Point

📝 Introduction
Mongod is a Tier 0 machine that focuses on NoSQL database enumeration. The objective is to identify a misconfigured MongoDB instance that allows anonymous authentication, enabling an attacker to browse internal databases and extract sensitive information without any credentials.

🔍 Step 1: Enumeration
I started with a full port scan to identify all services running on the target machine.

Command: nmap -p- --min-rate=1000 -sV {TARGET_IP}

Findings: * Port 22/tcp: SSH (OpenSSH 8.2p1)

Port 27017/tcp: MongoDB (Version 3.6.8)

Note: Port 27017 is the default port for MongoDB. Detecting the version 3.6.8 was crucial for selecting the right connection tool.

🚀 Step 2: Exploitation (Database Access)
Since the server allows anonymous logins, I used the mongo shell to connect directly to the database.

Establishing Connection:

Command: mongo {TARGET_IP}:27017

Result: Successfully connected without a username or password. The terminal prompt changed to >.

Listing Available Databases:

Command: show dbs

Findings: I discovered a non-default database named sensitive_information.

🏆 Step 3: Data Extraction & Flag
After identifying the target database, I navigated through its structure to find the flag.

Selecting the Database:

Command: use sensitive_information

Listing Collections (Folders):

Command: show collections

Result: Found a collection named flag.

Dumping the Data:

Command: db.flag.find().pretty()

Action: This command retrieves all documents within the 'flag' collection in a readable format.

Flag: 1b6e6fb359e7c40241b6d431427ba6ea

💡 Key Learnings
NoSQL Structure: Learned the hierarchy of MongoDB: Database > Collections > Documents.

Anonymous Login Risk: Understood how dangerous it is to leave a database exposed to the public internet without authentication.

Version Compatibility: Realized that newer tools (mongosh) might have issues with older server versions, making the legacy mongo tool necessary.

Follow my journey as I explore more HTB machines! 🚀
