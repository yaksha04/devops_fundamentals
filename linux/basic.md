Linux Basics: Distributions, pwd, and ls

This document explains Linux distributions and two of the most fundamental Linux commands — pwd and ls.
It is intended for beginners, students, and DevOps aspirants who want a strong Linux foundation.

📌 What is a Linux Distribution?

A Linux distribution (distro) is a complete operating system built on top of the Linux kernel.

Components of a Linux Distro:

Linux Kernel (core of the OS)

System utilities (GNU tools)

Package manager

Desktop environment or server tools

Pre-installed software

Common Linux Distributions:
Distribution	Use Case
Ubuntu	Beginners, DevOps, Cloud
Debian	Stability-focused systems
Fedora	Latest features
Arch Linux	Advanced users
CentOS / Rocky Linux	Enterprise servers

🔹 Industry reality:
Most servers and cloud environments use Ubuntu or RHEL-based distributions.

📂 pwd Command
Meaning:

Print Working Directory

Purpose:

Displays the absolute path of the current directory you are working in.

Syntax:
pwd

Example Output:
/home/user/projects

Explanation:

/ → Root directory

home → User home directories

user → Username

projects → Current folder

✅ Use pwd whenever you are unsure about your current location in the filesystem.

📄 ls Command
Meaning:

List Directory Contents

Purpose:

Displays files and directories inside the current directory.

Basic Syntax:
ls

Example Output:
main.py  Dockerfile  README.md

🔧 Common ls Options (Very Important)
Command	Description
ls -l	Long listing (permissions, size, owner)
ls -a	Show hidden files (dot files)
ls -h	Human-readable file sizes
ls -lh	Combined detailed + readable output

Example:
ls -lh


Output:

-rw-r--r-- 1 user user 1.2K README.md


