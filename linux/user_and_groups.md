Linux Users & Groups Management: useradd and groupadd

This document explains how users and groups are managed in Linux using the useradd and groupadd commands.
These commands are essential for system administration, DevOps, and server security.

📌 Users and Groups in Linux

Linux is a multi-user operating system.

Users → individual accounts

Groups → collection of users

Permissions are applied based on user + group

📌 Every process in Linux runs as some user.

👥 Why Users & Groups Matter

Access control

Security isolation

Application ownership

Production server safety

❌ Poor user management = security breaches
❌ Running everything as root = disaster waiting to happen

👤 useradd Command
Purpose:

Creates a new user account in the system.

Basic Syntax:
sudo useradd username


📌 This creates a user without home directory or password (not useful alone).

✅ Recommended Way to Create a User
sudo useradd -m -s /bin/bash username

Explanation:
Option	Meaning
-m	Create home directory
-s	Default shell
Set Password for User
sudo passwd username


📌 Mandatory step.

📂 User Information Location
File	Purpose
/etc/passwd	User account info
/etc/shadow	Encrypted passwords
/etc/group	Group info

⚠️ Do NOT edit these manually unless you know what you’re doing.

👨‍👩‍👧 groupadd Command
Purpose:

Creates a new group.

Syntax:
sudo groupadd groupname

Example:
sudo groupadd devops

➕ Add User to a Group
sudo usermod -aG groupname username

Example:
sudo usermod -aG devops kuala


📌 -aG is critical
❌ Forgetting -a removes user from other groups

🔍 Check User & Group Info
Check user ID and groups
id username

Check current user
whoami

List all users
cat /etc/passwd

List all groups
cat /etc/group

⚠️ Root User Reality Check

root = superuser

Can delete anything

No permission checks

📌 Best practice:

Create normal users

Use sudo only when required

⚠️ Common Beginner Mistakes (Honest Truth)

Creating users without passwords

Running apps as root

Forgetting -a in usermod -aG

Editing /etc/passwd manually

Not understanding group-based access

👉 These mistakes break servers, not just labs.

🧠 Key Takeaways

useradd → create users

groupadd → create groups

Groups control permissions

Never use root casually

Proper user management = secure systems