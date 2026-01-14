# 🚩 Hack The Box: Fawn (Writeup)

**Machine Name:** Fawn  
**Difficulty:** Very Easy (Tier 0)  
**Platform:** Hack The Box Starting Point  

---

## 📝 Introduction
Fawn is a Tier 0 machine that focuses on the **File Transfer Protocol (FTP)**. The objective is to identify an insecure FTP configuration that allows unauthorized access to sensitive files.

## 🔍 Step 1: Enumeration
I started the process by verifying connectivity with a `ping` and then performed a service version scan using Nmap.

- **Command:** `nmap -sV {TARGET_IP}`
- **Findings:** The scan identified that **Port 21/tcp** is open, running the **FTP** service (vsftpd).

> **Concept:** Port 21 is the standard port for FTP control. Version detection (`-sV`) helps in identifying if the software is outdated or misconfigured.

## 🚀 Step 2: Exploitation (Anonymous FTP Login)
A common misconfiguration in FTP servers is allowing **Anonymous** login. This allows anyone to log in without a unique password.

1. I connected to the FTP service:  
   `ftp {TARGET_IP}`
2. When prompted for a username, I entered: `anonymous`
3. For the password, I left it blank and pressed **Enter**.

**Result:** `Login successful. (Logged in as anonymous)`

## 🏆 Step 3: Capturing the Flag
After gaining access to the FTP server, I navigated the file system to find the flag.

1. **List Files:** Used `ls` to view the directory contents.
2. **Found File:** `flag.txt` was visible in the directory.
3. **Download File:** Used the `get` command to transfer the file to my local machine.
   - **Command:** `get flag.txt`
4. **Read Flag:** Exited the FTP session and used `cat flag.txt` to read the hash.

Flag: ********************************

---

## 💡 Key Learnings
- **Insecure Protocols:** FTP sends data in plaintext, making it vulnerable to interception.
- **Access Control:** "Anonymous" login should be disabled on production servers to prevent unauthorized data access.
- **FTP Commands:** Learned how to interact with an FTP server using commands like `get`, `ls`, and `bye`.

---
*Continuing my journey on Hack The Box!* 🚀
