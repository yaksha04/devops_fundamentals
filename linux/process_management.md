Linux Process Management

This document explains how processes are viewed, monitored, and controlled in Linux using common process-management commands.

These concepts are critical for:

Linux administration

DevOps & SRE

Debugging production issues

Interviews

📌 What Is a Process?

A process is a running instance of a program.

Examples:

Running python app.py

A web server like nginx

A background cron job

Each process has:

PID (Process ID)

Owner (user)

State (running, sleeping, stopped)

Resource usage (CPU, memory)

🔍 Viewing Processes
🔹 ps Command (Process Status)
Show current shell processes
ps

🔹 Show All Processes (Very Important)
ps aux

Column	Meaning
USER	Process owner
PID	Process ID
%CPU	CPU usage
%MEM	Memory usage
COMMAND	Command name

📌 ps aux is asked in interviews.

🔹 Filter Processes
ps aux | grep nginx


📌 Common real-world usage.

📊 top Command (Live Monitoring)
Purpose:

Displays real-time process activity.

top


Shows:

CPU usage

Memory usage

Load average

Running processes

🔧 Useful top Shortcuts
Key	Action
q	Quit
k	Kill process
M	Sort by memory
P	Sort by CPU

📌 top is used during production incidents.

🛑 Killing Processes
🔹 kill Command
Syntax:
kill PID


Example:

kill 1234


📌 Sends SIGTERM (15) — graceful stop.

🔥 Force Kill (Last Option)
kill -9 PID


📌 SIGKILL — process dies immediately.

🚨 Truth:
Overusing kill -9 can corrupt files and data.

🔹 Kill by Name
pkill nginx


or

killall nginx


📌 Faster than finding PID manually.

🧠 Process States (Important)
State	Meaning
R	Running
S	Sleeping
D	Uninterruptible sleep
T	Stopped
Z	Zombie

⚠️ Zombie processes = bad parenting (parent didn’t clean up).

🔄 Foreground & Background Processes
Run Process in Background
sleep 100 &


📌 & sends process to background.

View Background Jobs
jobs

Bring Job to Foreground
fg %1

Send Running Process to Background
Ctrl + Z
bg


📌 Useful in terminals.

🔍 Other Useful Commands
Command	Purpose
htop	Better top (if installed)
uptime	System load
watch	Run command repeatedly
nice	Set process priority
renice	Change priority
