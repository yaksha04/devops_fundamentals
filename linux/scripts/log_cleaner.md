Log Cleaner – Bash Script

This script finds and deletes old log files to prevent disks from filling up.

Used in:

Production servers

Cron jobs

DevOps maintenance tasks

📜 Script: log_cleaner.sh
#!/bin/bash

# Directory containing logs
LOG_DIR="/var/log/myapp"

# Delete logs older than N days
DAYS=7

# Check if log directory exists
if [ ! -d "$LOG_DIR" ]
then
    echo "Log directory does not exist: $LOG_DIR"
    exit 1
fi

echo "Cleaning logs older than $DAYS days in $LOG_DIR"

# Find and delete old log files
find "$LOG_DIR" -type f -name "*.log" -mtime +$DAYS -print -delete

echo "Log cleanup completed"
exit 0

🔍 Line-by-Line Explanation
1️⃣ Configuration
LOG_DIR="/var/log/myapp"
DAYS=7


LOG_DIR → where logs live

DAYS → how old logs must be to delete

📌 These are safe knobs — easy to tune.

2️⃣ Safety Check (CRITICAL)
if [ ! -d "$LOG_DIR" ]


Prevents accidental deletes

Stops script if directory is wrong

🚨 Never skip this in production

3️⃣ Find Old Logs
find "$LOG_DIR" -type f -name "*.log" -mtime +$DAYS


-type f → files only

-name "*.log" → log files

-mtime +7 → older than 7 days

4️⃣ Print Before Delete (Good Practice)
-print -delete


Shows what will be deleted

Then deletes it

📌 Debug-friendly & safer.

▶️ How to Run
chmod +x log_cleaner.sh
sudo ./log_cleaner.sh


📌 sudo required for /var/log.

🧪 Dry Run Mode (HIGHLY Recommended)

Before deleting, test:

find "$LOG_DIR" -type f -name "*.log" -mtime +$DAYS -print


If output looks correct → enable -delete.

⏰ Run Automatically (Cron Example)
crontab -e


Run daily at 2 AM:

0 2 * * * /path/log_cleaner.sh >> /var/log/log_cleaner.log 2>&1




