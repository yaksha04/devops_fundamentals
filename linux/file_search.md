Linux File Search: find and locate

This document explains how to search files and directories in Linux using the find and locate commands.
File searching is a core skill for Linux users, DevOps engineers, and system administrators.

📌 Why File Search Matters

On real servers:

You don’t know where files are

Logs are spread across directories

Config files are everywhere

If you can’t search files properly → you waste time and look inexperienced.

🔎 find Command
Purpose:

Searches files and directories in real time by walking the filesystem.

Syntax:
find <path> <condition> <action>

🔹 Find File by Name
find /home -name file.txt


📌 Case-sensitive search.

Case-Insensitive Search
find /home -iname file.txt

🔹 Find by File Type
find . -type f

Type	Meaning
f	Regular file
d	Directory
l	Symbolic link
🔹 Find Files by Size
find /var/log -size +100M


📌 Finds files larger than 100MB.

🔹 Find Files by Permission
find . -perm 755

🔹 Find and Delete (⚠️ Dangerous)
find . -name "*.log" -delete


🚨 Always test first without -delete.

🔹 Find and Execute Command
find . -name "*.sh" -exec chmod +x {} \;


📌 Very common in DevOps workflows.

⚡ locate Command
Purpose:

Searches files using a prebuilt database (much faster than find).

Syntax:
locate filename

Example:
locate nginx.conf


📌 Returns all paths matching the name.

🔄 Update locate Database
sudo updatedb


📌 Required after creating new files.

🆚 find vs locate
Feature	find	locate
Speed	Slower	Very fast
Accuracy	Real-time	Database-based
Permissions	Respects permissions	May show restricted paths
Use case	Precise searches	Quick lookups

💡 Rule of thumb:

Use find → accuracy matters

Use locate → speed matters
