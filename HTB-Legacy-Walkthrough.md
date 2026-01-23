🚀 HackTheBox: Legacy (Write-up)

**Date:** January 23, 2026
**Machine Name:** Legacy
**OS:** Windows XP
**Difficulty:** Easy (Classic)
**Focus:** SMB Vulnerabilities & Metasploit

---

## 🔍 Phase 1: Enumeration
The scan revealed that the machine was running a very old version of Windows (XP) with ports **139** and **445** open. This immediately pointed towards an SMB vulnerability.

- **Open Ports:** 139 (NetBIOS), 445 (SMB)
- **Nmap Command:** `nmap -sV -sC -O <Machine_IP>`

## 🛡️ Phase 2: Vulnerability Analysis
Using Nmap scripts, I identified that the target was vulnerable to **MS08-067** (NetAPI), a legendary vulnerability that allows Remote Code Execution (RCE).

## ⚔️ Phase 3: Exploitation
I used the Metasploit Framework to execute the attack. 

- **Module:** `exploit/windows/smb/ms08_067_netapi`
- **Payload:** `windows/meterpreter/reverse_tcp`
- **Challenge:** Encountered a session crash (Service unstable), resolved by restarting the machine and ensuring the `LHOST` was correctly mapped to the `tun0` interface.

## 🏁 Phase 4: Post-Exploitation
- **Privilege Level:** `NT AUTHORITY\SYSTEM` (Full Control)
- **Flags Captured:** - User: `John/Desktop/user.txt`
  - Root: `Administrator/Desktop/root.txt`
flag:e69af0e4f443de7e36876fda4ec7644f


## 🧠 Lessons Learned
1. **SMB is fragile:** Old services can crash if the exploit is not stable.
2. **Network Config:** Correctly setting `LHOST` (VPN IP) is crucial for a reverse shell.
3. **History of Exploits:** Learned about the connection between MS08-067 and the evolution of attacks like WannaCry (MS17-010).
