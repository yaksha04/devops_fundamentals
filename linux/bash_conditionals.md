Bash Conditional Statements
if, else, elif

This document explains conditional logic in Bash scripting using if, else, and elif.

Conditions allow scripts to:

Make decisions

Handle errors

React to system state

Automate real workflows

This is non-negotiable for DevOps automation.

📌 Why Conditions Matter

Without conditions, scripts are dumb.
With conditions, scripts become intelligent.

Examples:

Check if a file exists

Verify disk usage

Run commands only if a service is running

Exit safely on failure

🧱 Basic if Syntax
if [ condition ]
then
    command
fi


⚠️ Spacing matters in Bash

✅ Correct:

if [ "$A" = "1" ]


❌ Wrong:

if ["$A"="1"]

🧪 Simple Example
#!/bin/bash

NUM=10

if [ $NUM -gt 5 ]
then
    echo "Number is greater than 5"
fi

🔁 if-else Statement
if [ condition ]
then
    command
else
    command
fi

Example:
#!/bin/bash

AGE=18

if [ $AGE -ge 18 ]
then
    echo "Eligible to vote"
else
    echo "Not eligible"
fi

🔂 if-elif-else Statement
if [ condition1 ]
then
    command
elif [ condition2 ]
then
    command
else
    command
fi

Example:
#!/bin/bash

MARKS=72

if [ $MARKS -ge 90 ]
then
    echo "Grade A"
elif [ $MARKS -ge 60 ]
then
    echo "Grade B"
else
    echo "Grade C"
fi

🔢 Numeric Comparison Operators
Operator	Meaning
-eq	equal
-ne	not equal
-gt	greater than
-lt	less than
-ge	greater or equal
-le	less or equal
Example:
if [ $A -eq $B ]

🔤 String Comparison Operators
Operator	Meaning
=	equal
!=	not equal
-z	string is empty
-n	string is not empty
Example:
if [ "$NAME" = "admin" ]

📂 File Test Operators (Very Important)
Test	Meaning
-f	file exists
-d	directory exists
-e	file or directory exists
-r	readable
-w	writable
-x	executable
Example:
if [ -f "/etc/passwd" ]
then
    echo "File exists"
fi


📌 Used heavily in real scripts.

⚡ Using && and || (Shortcut Conditions)
AND (&&)
[ -f file.txt ] && echo "File found"

OR (||)
[ -f file.txt ] || echo "File missing"


📌 Cleaner for small checks.

🧠 Best Practices

Always quote variables: "$VAR"

Use file tests before deleting files

Keep conditions readable

Exit early on failure

Example:

if [ ! -f "$1" ]
then
    echo "File not found"
    exit 1
fi

⚠️ Common Beginner Mistakes (Honest)

Forgetting spaces in [ condition ]

Using = instead of -eq for numbers

Not quoting variables

Nested conditions becoming unreadable

Assuming Bash behaves like Python ❌

👉 These mistakes cause silent script failures.

🧠 Key Takeaways

if controls logic in scripts

Use correct operators for numbers vs strings

File tests are extremely important

Spacing and quoting matter

Conditions turn scripts into automation tools

🚀 Suggested Next Topics

User input (read)

Script arguments ($1, $2)

Loops (for, while)

Functions in Bash

Writing real DevOps automation scripts
