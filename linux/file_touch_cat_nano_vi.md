Linux File Handling & Editors: touch, cat, nano, vi

This document explains basic file creation, viewing, and editing commands in Linux.
These commands are essential for Linux users, DevOps engineers, and system administrators.

📌 File Handling in Linux

In Linux, everything is treated as a file.
You create files, view their content, and edit them directly from the terminal.

✏️ touch Command
Purpose:

Creates an empty file or updates the timestamp of an existing file.

Syntax:
touch filename

Example:
touch app.py


📌 If the file does not exist → it is created
📌 If the file exists → timestamp is updated

📖 cat Command
Meaning:

Concatenate

Purpose:

Displays the content of a file on the terminal.

Syntax:
cat filename

Example:
cat README.md

Create File with Content:
cat > file.txt
Hello Linux
Ctrl + D

🔧 Useful cat Options
Command	Description
cat -n file.txt	Show line numbers
cat file1 file2	Combine files

📌 Best for small files.
❌ Not ideal for large files.

📝 nano Editor
Purpose:

Beginner-friendly terminal text editor.

Open a File:
nano file.txt

Common Nano Shortcuts:
Shortcut	Action
Ctrl + O	Save
Ctrl + X	Exit
Ctrl + K	Cut line
Ctrl + U	Paste line

📌 Easy
📌 Beginner-friendly
📌 Widely available

⚙️ vi Editor
Purpose:

Powerful, professional Linux text editor.

Open a File:
vi file.txt

🔁 Modes in vi
Mode	Purpose
Command Mode	Default mode
Insert Mode	Write text
Last Line Mode	Save / Exit
Common vi Commands
Command	Action
i	Insert mode
Esc	Back to command mode
:w	Save
:q	Quit
:wq	Save & quit
:q!	Force quit

📌 Reality check:
If you work on servers, you must know vi.
No GUI. No excuses.

⚠️ Common Beginner Mistakes

Forgetting to exit insert mode in vi

Using cat for large files

Not saving changes before exit

Editing system files without permission

🧠 Key Takeaways

touch → create files

cat → view file content

nano → beginner editor

vi → professional, unavoidable editor

Mastering these saves you from embarrassment in real servers