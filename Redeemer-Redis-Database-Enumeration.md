# 🚩 Hack The Box: Redeemer (Writeup)

**Machine Name:** Redeemer  
**Difficulty:** Very Easy (Tier 0)  
**Platform:** Hack The Box Starting Point  

---

## 📝 Introduction
Redeemer is a Tier 0 machine that explores **Redis**, an open-source, in-memory NoSQL key-value data store. Unlike traditional databases that store data on disks, Redis keeps data in RAM for extremely fast retrieval. The goal is to enumerate the Redis server and dump the database to find the flag.



## 🔍 Step 1: Enumeration
As always, the process begins with connectivity testing and port scanning.

- **Connectivity:** `ping {TARGET_IP}`
- **Service Scan:** `nmap -sV {TARGET_IP}`
- **Findings:** The scan revealed **Port 6379/tcp** is open, running a **Redis server**.

## 🚀 Step 2: Exploitation (Redis Interaction)
To interact with the target, I used the `redis-cli` utility.

1. **Installation:** If not installed: `sudo apt install redis-tools`
2. **Connecting to Server:** `redis-cli -h {TARGET_IP}`
3. **Information Gathering:** Once connected, I used the `info` command to see server statistics.
   - **Key Section:** The `Keyspace` section showed that only one database exists (**index 0**).

## 🏆 Step 3: Capturing the Flag
After identifying the database, I performed the following steps to extract the data:

1. **Select Database:** `select 0`
2. **List All Keys:** `keys *`  
   *(This command listed all keys stored in the database, including one that looked like the flag).*
3. **Retrieve Value:** `get flag`  

**Flag:** [Flag Successfully Captured]

---

## 💡 Key Learnings
- **In-Memory Databases:** Learned how Redis stores data as key-value pairs in RAM.
- **Unauthorized Access:** Redis servers should be password-protected and not exposed to the public internet without proper authentication.
- **Redis CLI:** Gained experience using `redis-cli` commands like `info`, `select`, `keys`, and `get`.

---
*Follow my journey as I document every step of my Cyber Security path!* 🚀
