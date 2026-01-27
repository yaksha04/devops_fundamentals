Linux Pipes and Redirection

This document explains pipes (|) and input/output redirection (>, >>, <) in Linux.
These concepts are foundational for shell scripting, DevOps automation, and log analysis.

📌 Why Pipes & Redirection Matter

Linux philosophy:

Small commands + chaining = powerful workflows

In real systems:

You rarely run one command alone

Outputs become inputs

Logs are redirected, filtered, stored

If you don’t understand pipes and redirection →
you’re using Linux at 10% power.

🔗 Pipes (|)
Purpose:

Passes the output of one command as the input of another command.

Syntax:
command1 | command2


📌 STDOUT of command1 → STDIN of command2

🔹 Basic Example
ls | grep ".txt"


📌 Lists only .txt files.

🔹 Real DevOps Example
ps aux | grep nginx


📌 Find running nginx processes.

🔹 Multiple Pipes
cat app.log | grep "error" | sort | wc -l


📌 Meaning:

Read log file

Filter errors

Sort results

Count lines

This is real production usage, not theory.

🔁 Input / Output Streams

Linux has three standard streams:

Stream	Name	Number
STDIN	Input	0
STDOUT	Output	1
STDERR	Error	2

Understanding this avoids silent failures.

➡️ Output Redirection (> and >>)
Redirect Output to File
ls > files.txt


📌 Overwrites file if it exists.

Append Output to File
ls >> files.txt


📌 Adds output to end of file.

Redirect Errors
ls invalidfile 2> error.txt


📌 Redirects error messages only.

Redirect Output + Error
command > all.txt 2>&1


📌 Common in scripts.

⬅️ Input Redirection (<)
Purpose:

Takes input from a file instead of keyboard.

Example:
wc -l < users.txt


📌 Counts lines in file without printing filename.

🔥 Special Redirection
Discard Output (Black Hole)
command > /dev/null


📌 Output is thrown away.

Discard Errors Only
command 2> /dev/null


📌 Used in cron jobs & scripts.

🔗 Pipes vs Redirection (Important)

| Feature | Pipes (|) | Redirection (>) |
|------|-----------|------------------|
| Connects commands | Yes | No |
| Writes to file | No | Yes |
| Used in chaining | Yes | No |
| Automation scripts | Yes | Yes |

💡 Rule:

Use pipes to connect commands

Use redirection to save results
