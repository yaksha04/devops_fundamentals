Linux Disk & Memory Usage: df and du

This document explains how to check disk space usage in Linux using the df and du commands.
These commands are critical for system administration, DevOps, and production troubleshooting.

📌 Why Disk Monitoring Matters

In real systems:

Disk full = app crash

Logs can silently fill disks

Databases stop working

Servers become unstable

📌 Most production outages start with “disk full”.

📊 df Command (Disk Free)
Purpose:

Shows disk space usage of mounted filesystems.

Syntax:
df

🔹 Human-Readable Output (Very Important)
df -h


Example output:

Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       40G   25G   13G  66% /

Column Meaning:
Column	Description
Filesystem	Disk/partition
Size	Total size
Used	Used space
Avail	Free space
Use%	Usage percentage
Mounted on	Mount point

📌 Use% > 80% = warning
📌 Use% > 90% = incident

🔧 Common df Options
Command	Description
df -h	Human readable
df -T	Show filesystem type
df /path	Check specific mount
📁 du Command (Disk Usage)
Purpose:

Shows space used by files and directories.

Syntax:
du


📌 By default, shows usage for every subdirectory (noisy).

🔹 Most Used Form
du -sh folder_name


Example:

du -sh logs/


Output:

2.5G    logs/


📌 -s → summary
📌 -h → human-readable

🔹 Find Largest Directories
du -h /var | sort -hr | head


📌 Real-world command used to debug disk issues.

🔧 Common du Options
Command	Description
du -h	Human readable
du -s	Summary only
du -a	Include files
du --max-depth=1	Limit depth
🆚 df vs du (Important Difference)
Feature	df	du
Shows	Filesystem usage	Directory/file usage
Level	Disk/partition	Folder/file
Use case	“Is disk full?”	“What is using disk?”

💡 Rule of thumb:

Use df → check disk health

Use du → find disk hogs
