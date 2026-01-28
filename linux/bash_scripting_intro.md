What Is Bash Scripting?

A Bash script is a file containing a series of Linux commands executed automatically by the Bash shell.

Instead of running commands manually:

mkdir logs
cd logs
touch app.log


You automate them:

#!/bin/bash
mkdir logs
cd logs
touch app.log


📌 This is how real systems are managed.

📄 Bash Script File
File Extension

Usually:

.sh


Example:

backup.sh

🔑 Shebang (#!)
What Is Shebang?

The shebang tells Linux which interpreter should execute the script.

Syntax:
#!/bin/bash


📌 Must be the first line of the script.

Why Shebang Matters

Without shebang:

./script.sh


❌ may fail or use wrong shell

With shebang:

./script.sh


✅ runs correctly

Common Shebangs
Shebang	Meaning
#!/bin/bash	Bash shell
#!/usr/bin/env bash	Portable Bash
#!/bin/sh	POSIX shell

📌 Most DevOps scripts use:

#!/bin/bash

▶️ Making Script Executable
chmod +x script.sh


Run script:

./script.sh

📦 Variables in Bash
What Is a Variable?

A variable stores data that can be reused.

Define a Variable
NAME="Kuala"


⚠️ No spaces around =

❌ Wrong:

NAME = Kuala

Access a Variable
echo $NAME


Output:

Kuala


📌 $ is mandatory when reading variables.

🧪 Example Script with Variables
#!/bin/bash

APP_NAME="myapp"
ENV="production"

echo "Application: $APP_NAME"
echo "Environment: $ENV"

🔄 Command Substitution

Store command output in a variable:

DATE=$(date)


or

DATE=`date`


Preferred:

$(command)

Example:
#!/bin/bash

TODAY=$(date)
echo "Today is: $TODAY"

🌍 Environment Variables vs Script Variables
Type	Scope
Script variable	Current script
Environment variable	Available to child processes

Export example:

export APP_ENV=production
