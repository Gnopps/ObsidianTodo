# ObsidianTodo

### Intro

Small script to monitor the files in your Obsidian-directory on Windows (or any other for that matter) for added keywords and then send the relevant line to your task-system (or any email). This is a great way to automate your task-creation without having to leave Obsidian.

### How it works

1. The script monitors files in your Obsidian-directory for a trigger you specify, e.g. "task"
2. Once the trigger is found it takes all lines with the keyword you specify and sends those one by one by to an email your specify. The script will capture all in the same line before the keyword and send as subject with the note name in the body.
3. The script then removes the trigger and changes the keyword to another keyword you specify

### Requirements
- The details for your email's SMTP-server. This can be found easily for most providers (like Fastmail, Gmail, etc.)
- Possibility to execute Powershell (any recent Windows-version I think)

### Installation
1. Copy script to a file on your compunter named ServiceToMonitorForTodo.ps1
2. Modify the first lines in the script with your data
3. Setup a task in Task Scheduler to launch the script when your computer starts (below settings I use).
	- General: Run only when user is logged on, Hidden, Configure for Windows 10
	- Trigger: At log on
	- Actions: Start a program
		- Program: "powershell.exe"
		- Arguments: "PowerShell -noexit -windowstyle hidden -file C:\Scripts\ServiceToMonitorForTodo.ps1"
	- Conditions: All off

### Setup
These variables need to be setup.

Email-related:
- $loginuser: Your username to login to your SMTP-server
- $loginpassword: Password to login to the SMTP-server
- $smtpserver: The SMTP server address
- $smtpport: The SMTP server port
- $sendfrom: Email address to send the email from
- $sendto: Email address to send the email to

Computer-related:
- $folder: The folder you wish to monitor (where your Obsidian vault is located)
- $filter: You can enter a wildcard filter here, otherwise all files are monitored.
- IncludeSubdirectories: Wether or not to monitor subdirectories (default is off)

Note-related:
- $trigger: Trigger word to wait for (default "#task")
- $lookfor: Keyword for each line to be captured (default "#todo")
- $replaceto: Keyword to replace with once a line has been processed (default "#intasklist")

### Notes
- It is possible to use the same keyword and trigger but that means that the script may edit the note at the same time as you are which means some information may be lost. Thus I add the trigger once I know I'm not typing in the note anymore.
- Monitor service was made with this script as base (by BigTeddy 05 September 2011): https://gallery.technet.microsoft.com/scriptcenter/Powershell-FileSystemWatche-dfd7084b
- I've never written anything in Powershell before so really do not make any guarantees in terms of functioanlity or bugs. It is a fairly short script though so you should be able to check it out yourself with a little skill.
