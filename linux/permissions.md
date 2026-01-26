🔐 Linux File Permissions: chmod and chown

This document explains Linux file permissions, ownership, and how to manage them using the chmod and chown commands.
These concepts are critical for Linux administration, DevOps, and production servers.

📌 Why Permissions Matter in Linux

Linux is a multi-user operating system.
Permissions control:

Who can read a file

Who can write/edit a file

Who can execute a file

Misconfigured permissions =
❌ security issues
❌ broken applications
❌ production outages

📄 Understanding ls -l Output

Run:

ls -l


Example output:

-rw-r--r-- 1 user devops 1024 app.py

Breakdown:
Part	Meaning
-	File type (d = directory)
rw-	Owner permissions
r--	Group permissions
r--	Others permissions
user	File owner
devops	Group
1024	File size (bytes)
app.py	File name
🔑 Permission Types
Symbol	Meaning
r	Read
w	Write
x	Execute
-	No permission
👥 Permission Categories
Category	Meaning
Owner	File creator
Group	Group members
Others	Everyone else
🔧 chmod Command (Change Mode)
Purpose:

Changes file or directory permissions.

🔹 Symbolic Mode
Syntax:
chmod <who><operation><permission> filename

Example:
chmod u+x script.sh


📌 Adds execute permission to the owner.

Common symbolic options:
Symbol	Meaning
u	User
g	Group
o	Others
a	All
+	Add
-	Remove

Example:

chmod a+r file.txt

🔢 Numeric (Octal) Mode (Very Important)
Number	Permission
4	Read
2	Write
1	Execute
Common Values:
Value	Meaning
7	rwx
6	rw-
5	r-x
4	r--
Example:
chmod 755 script.sh


Meaning:

Owner → rwx (7)

Group → r-x (5)

Others → r-x (5)

📌 755 is extremely common for scripts and apps.

👤 chown Command (Change Owner)
Purpose:

Changes file owner and group.

Syntax:
chown owner:group filename

Example:
chown user:devops app.py


📌 Owner becomes user, group becomes devops.

Change Only Owner
chown user file.txt

Change Only Group
chown :devops file.txt

Recursive Ownership Change
chown -R user:devops project/


📌 Common in deployments.

⚠️ Common Beginner Mistakes (Be Honest)

Giving 777 permissions everywhere ❌ (security nightmare)

Using chmod without understanding numbers

Forgetting -R for directories

Running chown without sudo

Breaking apps by changing ownership blindly

💡 Truth:
If you use chmod 777 in interviews → instant rejection.

🧠 Key Takeaways

Permissions define who can do what

chmod → change permissions

chown → change owner/group

Numeric mode (755, 644) is industry standard

Permissions mistakes cause real production failures