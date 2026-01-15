🚩 Hack The Box: Synced (Writeup)
Machine Name: Synced

Difficulty: Very Easy (Tier 0)

Platform: Hack The Box Starting Point

📝 Introduction
Synced is a Tier 0 Linux machine that demonstrates how the rsync (Remote Sync) protocol can be exploited if misconfigured. The goal is to identify an rsync "module" that allows anonymous access and extract the flag stored within it.

🔍 Step 1: Enumeration
The first step was to identify open ports and services using Nmap.

Command: nmap -p- --min-rate=1000 -sV {TARGET_IP}

Findings: The scan showed that Port 873/tcp is open, which is the default port for the rsync service. The protocol version detected was 31.

🚀 Step 2: Exploitation (rsync Enumeration)
Since the rsync daemon often hosts "modules" (shared directories), I checked if any were accessible without credentials (anonymous login).

Listing Available Modules:

Command: rsync --list-only {TARGET_IP}::

Action: Using double colons :: allows direct interaction with the rsync daemon.

Result: Found a module named public with the label "Anonymous Share".

Listing Files Inside the Module:

Command: rsync --list-only {TARGET_IP}::public

Result: Successfully listed the contents and found a file named flag.txt.

🏆 Step 3: Finding the Flag
To get the flag, I used rsync to sync (download) the remote file to my local machine.

Downloading the File:

Command: rsync {TARGET_IP}::public/flag.txt flag.txt

Reading the Flag:

Command: cat flag.txt

Flag: 72eaf5344ebb84908ae543a719830519

💡 Key Learnings
Delta-Transfer: Learned that rsync is more efficient than FTP because it only sends the differences between files.

Anonymous Authentication: Understood that passing None as credentials (no username/password) is a common misconfiguration in rsync.

Daemon Interaction: Learned the syntax difference between a single colon (SSH-based) and double colons (Daemon-based) in rsync.

Tier 0 Completed! Ready for Tier 1. 🚀
