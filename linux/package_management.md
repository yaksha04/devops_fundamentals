Linux Package Management: apt and yum

This document explains Linux package management using apt and yum.
Package managers are used to install, update, remove, and manage software on Linux systems.

This is daily work for system admins and DevOps engineers.

📌 What Is a Package Manager?

A package manager:

Downloads software

Installs dependencies automatically

Updates packages safely

Removes software cleanly

📌 No manual .zip or .exe nonsense like Windows.

🧭 Package Managers by Distribution
Linux Distro	Package Manager
Ubuntu / Debian	apt
CentOS / RHEL / Rocky	yum (now dnf)
Fedora	dnf
Arch	pacman

📌 In servers & cloud, Ubuntu (apt) and RHEL-based (yum/dnf) dominate.

📥 apt Package Manager (Debian / Ubuntu)
🔹 Update Package Index (Very Important)
sudo apt update


📌 Fetches latest package information.
📌 Does not install anything.

🔹 Install a Package
sudo apt install nginx

🔹 Install Multiple Packages
sudo apt install git curl vim

🔹 Upgrade Installed Packages
sudo apt upgrade


📌 Upgrades packages using updated index.

🔹 Remove a Package
sudo apt remove nginx

🔹 Remove Package + Config Files
sudo apt purge nginx

🔹 Search for a Package
apt search docker

🔹 Show Package Info
apt show nginx

📥 yum Package Manager (RHEL / CentOS / Rocky)
🔹 Install a Package
sudo yum install nginx

🔹 Update Packages
sudo yum update

🔹 Remove a Package
sudo yum remove nginx

🔹 Search for a Package
yum search docker

🔹 List Installed Packages
yum list installed

🔄 apt vs yum
Feature	apt	yum
Used in	Ubuntu/Debian	RHEL/CentOS
Speed	Faster	Slightly slower
Dependency handling	Excellent	Excellent
Common in cloud	✅ Very common	✅ Very common

📌 Reality:
If you know one, you can learn the other in a day.
