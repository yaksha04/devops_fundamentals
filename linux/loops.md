Bash Loops
for and while

This document explains looping in Bash scripting using for and while loops.

Loops allow scripts to:

Repeat tasks

Process multiple files

Automate bulk operations

Replace manual repetitive work

This is essential for DevOps and system automation.

📌 Why Loops Matter

Without loops:

Scripts work once

You repeat commands manually

With loops:

Scripts scale

Automation becomes powerful

Ops work becomes fast and reliable

Example:

Check disk usage every 5 seconds

Rename 100 files

Deploy to multiple servers

🔁 for Loop
Purpose:

Iterates over a list of values.

🧱 Basic for Loop Syntax
for variable in list
do
    command
done

🧪 Simple Example
#!/bin/bash

for i in 1 2 3 4 5
do
    echo "Number: $i"
done

📂 Loop Over Files
for file in *.txt
do
    echo "Processing $file"
done


📌 Common in backups, cleanup scripts.

🔢 C-Style for Loop
for (( i=1; i<=5; i++ ))
do
    echo "Count: $i"
done


📌 Useful when you need counters.

🌍 Loop Over Command Output
for user in $(cat users.txt)
do
    echo "User: $user"
done


⚠️ Breaks if data contains spaces (advanced fix later).

🔁 while Loop
Purpose:

Repeats while a condition is true.

🧱 Basic while Syntax
while [ condition ]
do
    command
done

🧪 Simple Example
#!/bin/bash

count=1

while [ $count -le 5 ]
do
    echo "Count: $count"
    count=$((count + 1))
done

⏳ Infinite Loop (Be Careful)
while true
do
    echo "Running..."
    sleep 2
done


📌 Used in monitoring scripts
🚨 Dangerous if uncontrolled

📂 Read File Line by Line (Very Important)
while read line
do
    echo "$line"
done < file.txt


📌 Safest way to read files in Bash.

🔄 for vs while (When to Use What)
Feature	for	while
Known list	✅	❌
Condition-based	❌	✅
File iteration	✅	✅
Infinite loop	❌	✅
Monitoring scripts	❌	✅

💡 Rule of thumb:

Use for → when you know the items

Use while → when looping depends on condition

🛑 Loop Control Statements
break → exit loop
break

continue → skip iteration
continue

Example:
for i in 1 2 3 4 5
do
    if [ $i -eq 3 ]
    then
        continue
    fi
    echo $i
done


Output:

1
2
4
5

⚠️ Common Beginner Mistakes (Honest)

Infinite loops by mistake

Forgetting to update counter

Using for when while is needed

Not quoting variables

Reading files incorrectly with for

👉 These cause hung scripts and CPU waste.



