Linux File Operations: cp, mv, rm

This document explains how to copy, move, and delete files and directories in Linux using the cp, mv, and rm commands.
These commands are used daily by Linux users, DevOps engineers, and system administrators.

📌 File Operations in Linux

Linux provides simple yet powerful commands to manage files and directories from the terminal:

cp → Copy files/directories

mv → Move or rename files/directories

rm → Delete files/directories

⚠️ Important: Linux does not have a recycle bin for terminal deletes.

📄 cp Command (Copy)
Purpose:

Copies files or directories from one location to another.

Syntax:
cp source destination

Example:
cp file.txt backup.txt


📌 Creates a copy of file.txt named backup.txt.

📂 Copy Directories
cp -r project project_backup


📌 -r = recursive (required for directories)

🔧 Common cp Options
Command	Description
cp -r	Copy directories
cp -v	Verbose output
cp -i	Ask before overwrite
🚚 mv Command (Move / Rename)
Purpose:

Moves files/directories or renames them.

Syntax:
mv source destination

Move a File
mv file.txt /home/user/docs/


📌 File is moved to another directory.

Rename a File
mv old.txt new.txt


📌 No new file is created — name is changed.

Move a Directory
mv logs archive/


📌 Moves logs into archive.

❌ rm Command (Delete)
Purpose:

Deletes files or directories permanently.

Syntax:
rm filename

Example:
rm file.txt


📌 File is deleted permanently.

🗂️ Delete Directories
rm -r folder_name


📌 -r = recursive delete

⚠️ Dangerous but Common
rm -rf folder_name


-r → recursive

-f → force (no confirmation)

🚨 Reality check:
One wrong rm -rf can wipe production data.
This is how outages happen.

🔧 Common rm Options
Command	Description
rm -r	Delete directory
rm -f	Force delete
rm -i	Ask before delete
⚠️ Common Beginner Mistakes

Using rm -rf without checking path

Forgetting -r for directories

Overwriting files using cp or mv

Deleting files as root without thinking

💡 Pro habit:

ls
pwd


Before rm, always.

🧠 Key Takeaways

cp → copy files/directories

mv → move or rename

rm → delete permanently

Linux terminal deletes are not reversible

These commands are critical for DevOps & servers