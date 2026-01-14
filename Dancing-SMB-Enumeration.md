# 🚩 Hack The Box: Dancing (Writeup)

**Machine Name:** Dancing  
**Difficulty:** Very Easy (Tier 0)  
**Platform:** Hack The Box Starting Point  

---

## 📝 Introduction
Dancing is a Tier 0 machine that introduces the **SMB (Server Message Block)** protocol. SMB is primarily used for sharing access to files, printers, and serial ports on a network, commonly found on Windows systems.

## 🔍 Step 1: Enumeration
The first step was to identify open ports and services running on the target machine using Nmap.

- **Command:** `nmap -sV {TARGET_IP}`
- **Findings:** The scan showed that **Port 445/tcp** is open, which is the default port for the SMB service.



## 🚀 Step 2: Exploitation (SMB Enumeration)
To interact with the SMB shares, I used a tool called `smbclient`. I attempted to list the available shares without providing a valid password to check for anonymous access.

1. **List Shares:**
   - **Command:** `smbclient -L {TARGET_IP}`
   - **Action:** When prompted for a password, I simply pressed **Enter**.
   - **Results:** I found four shares: `ADMIN$`, `C$`, `IPC$`, and `WorkShares`.

2. **Accessing the Share:**
   I attempted to connect to the `WorkShares` directory as it appeared to be a custom share.
   - **Command:** `smbclient \\\\{TARGET_IP}\\WorkShares`
   - **Password:** (Blank)

**Result:** Access Granted!

## 🏆 Step 3: Finding the Flag
Once inside the SMB shell (`smb: \>`), I explored the directories:

1. **Navigation:**
   - Found two folders: `Amy.J` and `James.P`.
   - Used `cd` to enter `James.P`.
2. **Retrieving the Flag:**
   - Identified `flag.txt`.
   - Used the `get` command to download it: `get flag.txt`.
3. **Reading the Flag:**
   - Exited the SMB session and read the file on my local machine using `cat flag.txt`.

**Flag:** [Flag Successfully Captured]

---

## 💡 Key Learnings
- **SMB Shares:** Custom shares (like `WorkShares`) are often more prone to misconfigurations than administrative ones.
- **Anonymous Access:** Security best practices require disabling guest/anonymous login for sensitive network shares.
- **Tooling:** Learned how to use `smbclient` for listing and interacting with remote Windows shares.

---
*Follow my journey as I explore more HTB machines!* 🚀
