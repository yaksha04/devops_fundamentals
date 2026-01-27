Environment Variables in Linux
export and .bashrc

This document explains environment variables in Linux, how to create them using export, and how to make them persistent using .bashrc.

Environment variables are critical in:

Linux systems

DevOps pipelines

Docker & Kubernetes

CI/CD

Application configuration

📌 What Are Environment Variables?

Environment variables are key–value pairs used by the shell and programs to control behavior.

Examples:

PATH

HOME

USER

JAVA_HOME

DATABASE_URL

They help avoid:
❌ hardcoded values
❌ exposing secrets in code

🔍 View Environment Variables
View all environment variables
env


or

printenv

View a specific variable
echo $PATH


📌 $ is used to access a variable.

✏️ Temporary Environment Variables
Create a variable (shell-only)
MY_VAR="hello"


📌 Exists only in current shell
📌 Not available to child processes

🔑 export Command
Purpose:

Makes a variable available to child processes.

Syntax:
export VARIABLE_NAME=value

Example:
export APP_ENV=production


Check:

echo $APP_ENV


📌 This variable:

Works in current terminal

Is lost after logout or reboot

🔁 Temporary vs Exported Variables
Type	Scope
Normal variable	Current shell only
Exported variable	Shell + child processes
📂 Persistent Environment Variables (.bashrc)
Why .bashrc?

.bashrc is executed every time a new terminal opens.

📌 Used to:

Persist environment variables

Set aliases

Configure shell behavior

Location:
~/.bashrc

Add Environment Variable to .bashrc

Open file:

nano ~/.bashrc


Add at bottom:

export JAVA_HOME=/usr/lib/jvm/java-17
export APP_ENV=production


Apply changes:

source ~/.bashrc

🧪 Verify Persistence

Close terminal → reopen → run:

echo $JAVA_HOME


If value appears → ✅ success

⚠️ .bashrc vs .profile vs .bash_profile
File	When Used
.bashrc	Interactive shells
.profile	Login shells
.bash_profile	Login shells (bash)

📌 Most DevOps work uses .bashrc.

🔐 Environment Variables & Security

❌ DO NOT store secrets like:

Database passwords

API keys

Tokens

in:

GitHub repos

.bashrc committed to Git

✅ Use:

.env files

Secret managers

CI/CD secret stores
