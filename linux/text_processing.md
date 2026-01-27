Linux Text Processing: grep, sort, wc

This document explains basic text processing commands in Linux:
grep, sort, and wc.

These commands are heavily used in:

Log analysis

Debugging

DevOps pipelines

Shell scripting

Interviews

📌 Why Text Processing Matters

On real systems:

Logs are plain text

Config files are plain text

Outputs of commands are plain text

If you can’t process text, Linux becomes slow and painful.

🔍 grep Command
Meaning:

Global Regular Expression Print

Purpose:

Searches for patterns inside text.

🔹 Basic Syntax
grep "pattern" filename

Example:
grep "error" app.log


📌 Prints all lines containing error.

🔧 Common grep Options
Command	Description
grep -i	Case-insensitive
grep -n	Show line numbers
grep -v	Exclude pattern
grep -r	Recursive search
grep -c	Count matches
Examples
grep -i "fail" server.log

grep -v "INFO" app.log

grep -r "port" /etc


📌 Used daily in log analysis.

🔢 sort Command
Purpose:

Sorts lines of text alphabetically or numerically.

🔹 Basic Syntax
sort filename

🔧 Common sort Options
Command	Description
sort -n	Numeric sort
sort -r	Reverse order
sort -u	Unique values
sort -k	Sort by column
Examples
sort names.txt

sort -n marks.txt

sort -u data.txt


📌 Often combined with grep.

🔢 wc Command
Meaning:

Word Count

Purpose:

Counts lines, words, and characters.

🔹 Basic Syntax
wc filename

Output Format:
lines words characters filename

🔧 Common wc Options
Command	Description
wc -l	Line count
wc -w	Word count
wc -c	Character count
Examples
wc app.log

wc -l users.txt

wc -w README.md


📌 Very useful for log size estimation.

🔗 Command Chaining (Real DevOps Use)

Linux shines when commands are combined.

Example:
grep "error" app.log | sort | wc -l


📌 Meaning:

Search error

Sort results

Count lines

This is actual production usage, not theory.
