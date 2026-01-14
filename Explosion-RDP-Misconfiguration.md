# 🚩 Hack The Box: Explosion (Writeup)

**Machine Name:** Explosion  
**Difficulty:** Very Easy (Tier 0)  
**Platform:** Hack The Box Starting Point  

---

## 📝 Introduction
Explosion is a Tier 0 machine that introduces **Remote Desktop Protocol (RDP)**. Unlike Telnet or SSH which provide a Command Line Interface (CLI), RDP allows for a Graphical User Interface (GUI) connection, essentially giving the user full control over the remote desktop.

## 🔍 Step 1: Enumeration
The process began with a service version scan to identify open ports and the underlying operating system.

- **Command:** `nmap -sV {TARGET_IP}`
- **Findings:** The scan revealed several open ports, but the most interesting one was **Port 3389/tcp**, which is the default port for **RDP**.



## 🚀 Step 2: Exploitation (RDP Access)
To connect to the Windows target from a Linux machine (Pwnbox/Kali), I used the `xfreerdp` utility.

1. **Tool Check:** Verified `xfreerdp` installation.
2. **Connection Attempt:** I tried connecting using the `Administrator` account, testing for blank password misconfigurations.
   - **Command:** `xfreerdp /v:{TARGET_IP} /u:Administrator /cert:ignore`
3. **Authentication:** When prompted for a password, I simply pressed **Enter** (leaving it blank).

**Result:** Successful login! A remote desktop window opened, providing full GUI access to the target machine.

## 🏆 Step 3: Capturing the Flag
Once the remote desktop loaded:
1. I navigated to the **Desktop**.
2. Found a file named `flag.txt`.
3. Opened the file to retrieve the flag hash.

**Flag:** [Flag Successfully Captured]

---

## 💡 Key Learnings
- **RDP vs CLI:** RDP provides a full graphical experience, which is different from the terminal-only access provided by Telnet or SSH.
- **Security Risks:** Native services like Windows Remote Desktop can be dangerous if left enabled with default accounts and no passwords.
- **xfreerdp:** Learned how to use `xfreerdp` switches like `/v` (target), `/u` (user), and `/cert:ignore` to bypass certificate warnings.

---
*My HTB journey continues!* 🚀
