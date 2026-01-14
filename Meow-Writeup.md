# 🛡️ Hack The Box: Meow (Writeup)

**Machine Name:** Meow  
**Difficulty:** Very Easy (Tier 0)  
**Platform:** Hack The Box Starting Point

---

## 📝 Introduction
Meow is an entry-level machine designed to teach the basics of service enumeration and insecure protocols. The primary focus is on identifying and accessing the **Telnet** service.

## 🔍 Step 1: Enumeration
The first step was to verify connectivity and scan the target for open ports using Nmap.

- **Command:** `nmap -sV {TARGET_IP}`
- **Analysis:** The scan revealed that **Port 23/tcp** is open, running the **Telnet** service.

> **Observation:** Telnet is an unencrypted protocol used for remote management, often vulnerable if not properly secured with strong credentials.

## 🚀 Step 2: Exploitation (Foothold)
Since Telnet requires authentication, I attempted to log in using common administrative usernames with blank passwords (misconfiguration testing).

- **Usernames Tested:** `admin`, `administrator`, `root`
- **Successful Login:** Logging in as `root` with no password granted full access to the system.

**Connection Command:**
`telnet {TARGET_IP}`

## 🏆 Step 3: Extracting the Flag
Once the remote session was established:
1. Listed the directory contents using `ls`.
2. Found the target file: `flag.txt`.
3. Displayed the flag using the `cat` command.

**Flag:** `*******************************`

---

## 💡 Key Takeaways
- **Service Scanning:** Using Nmap to identify specific versions of running services.
- **Security Risk:** Leaving default accounts like `root` with no password is a critical security flaw.
- **Protocol Safety:** Preferring SSH over Telnet for secure remote management.

---
*Documenting my journey into Cyber Security.* 🚀
