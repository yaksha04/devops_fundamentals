Disk Usage Checker – Bash Script

This Bash script checks disk usage and prints a warning if usage crosses a defined threshold.

This pattern is commonly used in:

Server monitoring

Cron jobs

DevOps automation

Production health checks

📜 Script: disk_usage_checker.sh
#!/bin/bash

# Threshold percentage
THRESHOLD=80

# Get disk usage of root filesystem
USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

echo "Current disk usage: ${USAGE}%"

if [ "$USAGE" -ge "$THRESHOLD" ]
then
    echo "⚠️ Warning: Disk usage is above ${THRESHOLD}%"
    exit 1
else
    echo "✅ Disk usage is under control"
    exit 0
fi

🔍 Line-by-Line Explanation (Important)
1️⃣ Shebang
#!/bin/bash


Tells Linux to run this script using Bash.

2️⃣ Threshold Definition
THRESHOLD=80


Disk usage limit

Can be changed easily (e.g., 70, 90)

3️⃣ Disk Usage Extraction
df -h / | awk 'NR==2 {print $5}' | sed 's/%//'


What happens here:

df -h / → disk usage of root filesystem

awk 'NR==2 {print $5}' → extracts Use% column

sed 's/%//' → removes % symbol

📌 Result → clean number like 65, 92, etc.

4️⃣ Condition Check
if [ "$USAGE" -ge "$THRESHOLD" ]


-ge → numeric comparison

Checks if usage is greater than or equal to threshold

5️⃣ Exit Codes (Very Important)
Exit Code	Meaning
0	Success (OK state)
1	Failure (Warning/Error)

📌 Monitoring tools depend on exit codes.

▶️ How to Run the Script
Make executable:
chmod +x disk_usage_checker.sh

Run:
./disk_usage_checker.sh

🧪 Sample Output
Case 1: Disk OK
Current disk usage: 45%
✅ Disk usage is under control

Case 2: Disk High
Current disk usage: 92%
⚠️ Warning: Disk usage is above 80%
