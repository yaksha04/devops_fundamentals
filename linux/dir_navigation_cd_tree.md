Linux Directory Navigation: cd and tree

This document covers directory navigation in Linux using the cd command and directory visualization using the tree command.
These commands are fundamental for Linux users, DevOps engineers, and system administrators.

📌 Directory Navigation in Linux

Linux uses a hierarchical filesystem, starting from the root directory (/).
To move between directories, Linux provides the cd command.

📂 cd Command
Meaning:

Change Directory

Purpose:

Moves the user from one directory to another.

🔹 Basic Syntax
cd <directory_name>

Example:
cd projects


Moves into the projects directory from the current location.

🔁 Common cd Usage Patterns
1️⃣ Move to Home Directory
cd

cd ~


📌 Takes you directly to your home directory.

2️⃣ Move One Level Up
cd ..


📌 .. represents the parent directory.

3️⃣ Move to Root Directory
cd /


📌 Root is the top-most directory in Linux.

4️⃣ Absolute Path Navigation
cd /home/user/projects


📌 Starts from / (root).
📌 Safer and preferred in scripts.

5️⃣ Relative Path Navigation
cd ../logs


📌 Path relative to the current directory.

6️⃣ Go Back to Previous Directory
cd -


📌 Toggles between the last two directories.

⚠️ Common Beginner Mistakes

Using wrong directory names (Linux is case-sensitive)

Forgetting current location (pwd helps)

Confusing absolute and relative paths

🌳 tree Command
Purpose:

Displays directory structure in a tree-like format.

Syntax:
tree

Example Output:
project
├── app.py
├── Dockerfile
├── README.md
└── src
    ├── main.py
    └── utils.py


📌 Helps visualize large projects quickly.

🔧 Useful tree Options
Command	Description
tree -L 1	Show only one level
tree -L 2	Show two levels
tree -a	Include hidden files
tree -d	Show directories only
Example:
tree -L 2

📦 Installing tree (If Not Installed)
Debian / Ubuntu
sudo apt install tree

RedHat / CentOS / Rocky
sudo yum install tree

🧠 Key Takeaways

cd is used to navigate directories

.., /, ~ are navigation shortcuts

tree helps visualize project structure

These commands are used daily in real DevOps work