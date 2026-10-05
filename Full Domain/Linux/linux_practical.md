# Linux / Unix — Commands, Uses & Practical Maximum

## 1. Navigation Commands

### `pwd` — Print Working Directory

Shows the current directory.

```bash
pwd
```

Example output:

```text
/home/user/project
```

---

### `ls` — List Files

Shows files and directories.

```bash
ls
```

Useful forms:

```bash
ls -l
ls -a
ls -la
ls -lh
ls -lt
```

### Important options

| Option | Meaning                   |
| ------ | ------------------------- |
| `-l`   | Long/list details         |
| `-a`   | Show hidden files         |
| `-h`   | Human-readable sizes      |
| `-t`   | Sort by modification time |
| `-R`   | Recursive listing         |

---

### `cd` — Change Directory

```bash
cd /home/user
cd ..
cd ~
cd -
```

Meaning:

```text
.. → parent directory
~  → home directory
-  → previous directory
```

---

### `mkdir` — Create Directory

```bash
mkdir project
mkdir -p project/src/python
```

`-p` creates parent directories when required.

---

### `rmdir` — Remove Empty Directory

```bash
rmdir old_folder
```

It works only for empty directories.

---

## 2. File Creation and Management

### `touch`

Creates an empty file or updates its timestamp.

```bash
touch file.txt
```

Multiple files:

```bash
touch a.txt b.txt c.txt
```

---

### `cat`

Displays file contents.

```bash
cat file.txt
```

Multiple files:

```bash
cat file1.txt file2.txt
```

---

### `less`

Views a file page by page.

```bash
less largefile.txt
```

Useful for large files.

---

### `head`

Shows the beginning of a file.

```bash
head file.txt
head -n 5 file.txt
```

---

### `tail`

Shows the end of a file.

```bash
tail file.txt
tail -n 10 file.txt
```

Very important for logs:

```bash
tail -f app.log
```

`-f` continuously follows new content.

---

### `cp`

Copies files/directories.

```bash
cp file.txt backup.txt
cp file.txt /tmp/
cp -r project backup_project
```

`-r` = recursive.

---

### `mv`

Moves or renames files/directories.

Rename:

```bash
mv old.txt new.txt
```

Move:

```bash
mv file.txt /tmp/
```

---

### `rm`

Removes files.

```bash
rm file.txt
```

Directory recursively:

```bash
rm -r folder
```

Force:

```bash
rm -f file.txt
```

Recursive + force:

```bash
rm -rf folder
```

⚠️ `rm -rf` is dangerous because it can permanently delete data.

---

## 3. File Information

### `file`

Determines the type of a file.

```bash
file example.txt
```

---

### `stat`

Displays detailed metadata.

```bash
stat file.txt
```

Can show:

* Size
* Permissions
* Owner
* Inode
* Timestamps

---

### `wc`

Counts lines, words, and bytes/characters depending on options.

```bash
wc file.txt
wc -l file.txt
wc -w file.txt
wc -c file.txt
```

---

### `du`

Shows disk usage.

```bash
du file.txt
du -h
du -sh folder
```

---

### `df`

Shows filesystem disk space.

```bash
df
df -h
```

### `du` vs `df`

```text
du → usage of files/directories
df → available/used space of filesystems
```

---

# 4. File Searching

## `find`

Searches filesystem objects.

```bash
find . -name "test.txt"
```

Find directories:

```bash
find . -type d
```

Find files:

```bash
find . -type f
```

Find Python files:

```bash
find . -name "*.py"
```

Find files larger than 10 MB:

```bash
find . -type f -size +10M
```

Find recently modified files:

```bash
find . -type f -mtime -1
```

---

# 5. Text Searching

## `grep`

Searches file contents.

```bash
grep "hello" file.txt
```

Case-insensitive:

```bash
grep -i "hello" file.txt
```

Show line numbers:

```bash
grep -n "hello" file.txt
```

Recursive:

```bash
grep -r "hello" project/
```

Invert match:

```bash
grep -v "hello" file.txt
```

Count matches:

```bash
grep -c "hello" file.txt
```

---

## `grep` + pipe

```bash
ps aux | grep python
```

Meaning:

```text
ps output
   ↓
pipe
   ↓
grep searches python
```

---

# 6. Sorting and Filtering

## `sort`

Sorts lines.

```bash
sort names.txt
```

Reverse:

```bash
sort -r names.txt
```

Numeric:

```bash
sort -n numbers.txt
```

---

## `uniq`

Removes adjacent duplicate lines.

```bash
uniq names.txt
```

Usually combined with sort:

```bash
sort names.txt | uniq
```

Count duplicates:

```bash
sort names.txt | uniq -c
```

---

## `cut`

Extracts sections from lines.

```bash
cut -d ',' -f 1 users.csv
```

Meaning:

```text
-d ',' → comma delimiter
-f 1   → first field
```

---

## `tr`

Translates or deletes characters.

```bash
echo "hello" | tr 'a-z' 'A-Z'
```

Output:

```text
HELLO
```

---

## `awk`

Powerful text processing tool.

```bash
awk '{print $1}' file.txt
```

CSV-like example:

```bash
awk -F ',' '{print $1}' users.csv
```

---

## `sed`

Stream editor used for searching, replacing, deleting, and transforming text.

Replace first occurrence per line:

```bash
sed 's/old/new/' file.txt
```

Replace globally:

```bash
sed 's/old/new/g' file.txt
```

---

# 7. Input / Output

## Standard Streams

```text
0 → stdin
1 → stdout
2 → stderr
```

---

## Output Redirection `>`

Writes output to a file and replaces existing content.

```bash
echo "hello" > file.txt
```

---

## Append `>>`

Adds output to the end.

```bash
echo "hello" >> file.txt
```

---

## Input Redirection `<`

Uses a file as standard input.

```bash
sort < names.txt
```

---

## stderr Redirection

```bash
command 2> error.log
```

---

## stdout + stderr

```bash
command > output.log 2> error.log
```

Both into same file:

```bash
command > output.log 2>&1
```

---

# 8. Pipes

## `|`

Connects stdout of one command to stdin of another.

```bash
ls | grep ".py"
```

Another:

```bash
ps aux | grep python
```

More complex:

```bash
cat access.log | grep "404" | wc -l
```

Logic:

```text
cat
 ↓
grep
 ↓
wc
```

---

# 9. Process Management

## `ps`

Displays processes.

```bash
ps
```

More detailed:

```bash
ps aux
```

Process tree:

```bash
ps aux --forest
```

Search:

```bash
ps aux | grep python
```

---

## `top`

Real-time process/resource monitoring.

```bash
top
```

Shows:

* CPU
* Memory
* Processes
* Load
* Process IDs

---

## `htop`

Interactive process monitor with a more user-friendly interface.

```bash
htop
```

May need to be installed separately.

---

## `pgrep`

Finds process IDs based on process name/pattern.

```bash
pgrep python
```

---

## `pidof`

Finds PIDs associated with a program.

```bash
pidof python
```

---

## `pstree`

Displays processes as a tree.

```bash
pstree
```

Useful for understanding parent-child relationships.

---

# 10. Killing / Controlling Processes

## `kill`

Sends a signal to a process.

```bash
kill PID
```

Common:

```bash
kill -TERM PID
kill -KILL PID
```

Conceptually:

```text
kill -TERM → graceful termination request
kill -KILL → forced termination
```

---

## `pkill`

Kills/signals processes based on name/pattern.

```bash
pkill python
```

⚠️ Be careful because it can affect multiple processes.

---

## `killall`

Sends a signal to processes matching a name.

```bash
killall python
```

---

# 11. Foreground / Background

Run a process in background:

```bash
command &
```

Example:

```bash
python app.py &
```

---

## `jobs`

Shows jobs associated with the current shell.

```bash
jobs
```

---

## `fg`

Brings a background job to the foreground.

```bash
fg
```

---

## `bg`

Continues a stopped job in the background.

```bash
bg
```

---

## `nohup`

Allows a command to continue running after the terminal/session disconnects in typical usage.

```bash
nohup python app.py &
```

---

# 12. Signals

## `kill -SIGTERM`

```bash
kill -SIGTERM PID
```

Graceful termination request.

## `kill -SIGKILL`

```bash
kill -SIGKILL PID
```

Force termination.

## `kill -STOP`

```bash
kill -STOP PID
```

Stops a process.

## `kill -CONT`

```bash
kill -CONT PID
```

Continues a stopped process.

---

# 13. Permissions

## `chmod`

Changes permissions.

Symbolic:

```bash
chmod u+x script.sh
chmod g+w file.txt
chmod o-r file.txt
```

Numeric:

```bash
chmod 755 script.sh
chmod 644 file.txt
```

---

## `chown`

Changes owner.

```bash
chown user file.txt
```

Owner + group:

```bash
chown user:group file.txt
```

Recursive:

```bash
chown -R user:group project/
```

---

## `chgrp`

Changes group ownership.

```bash
chgrp developers file.txt
```

---

## `umask`

Displays current creation mask:

```bash
umask
```

Changes it for the current shell:

```bash
umask 022
```

---

# 14. User Management

## `whoami`

Shows current username.

```bash
whoami
```

---

## `id`

Shows user and group identity information.

```bash
id
```

---

## `who`

Shows logged-in users.

```bash
who
```

---

## `w`

Shows logged-in users and their activity.

```bash
w
```

---

## `users`

Shows currently logged-in usernames.

```bash
users
```

---

## `passwd`

Changes a user's password.

```bash
passwd
```

---

## `useradd`

Creates a user.

```bash
useradd username
```

---

## `usermod`

Modifies a user account.

```bash
usermod ...
```

---

## `userdel`

Deletes a user account.

```bash
userdel username
```

---

# 15. Privilege Management

## `sudo`

Run a command with elevated/another user's privileges.

```bash
sudo command
```

---

## `su`

Switch user.

```bash
su username
```

---

# 16. Environment

## `env`

Displays environment variables or runs a command with a modified environment.

```bash
env
```

---

## `printenv`

Displays environment variables.

```bash
printenv
```

Specific variable:

```bash
printenv PATH
```

---

## `export`

Creates/exports an environment variable to child processes.

```bash
export NAME="Musthafa"
```

Check:

```bash
echo "$NAME"
```

---

## `echo`

Displays text or variable values.

```bash
echo "Hello"
echo "$PATH"
```

---

# 17. Command Information

## `which`

Shows the executable found through PATH.

```bash
which python
```

---

## `whereis`

Locates binary/source/manual-related files for a command.

```bash
whereis python
```

---

## `type`

Shows how the shell interprets a command.

```bash
type cd
type python
```

---

## `command -v`

Portable way to determine how a command would be resolved.

```bash
command -v python
```

---

## `history`

Shows command history.

```bash
history
```

---

# 18. Manual / Help

## `man`

Shows manual pages.

```bash
man ls
man chmod
man grep
```

---

## `help`

Shows help for shell built-ins in shells that support it.

```bash
help cd
```

---

## `--help`

Many commands provide short help.

```bash
ls --help
```

---

# 19. Networking Commands

## `ip`

Modern Linux networking command.

Show addresses:

```bash
ip addr
```

Show routes:

```bash
ip route
```

Show links:

```bash
ip link
```

---

## `ping`

Tests basic network reachability.

```bash
ping google.com
```

---

## `ss`

Displays socket/network connection information.

```bash
ss
ss -tuln
```

Conceptually:

```text
-t → TCP
-u → UDP
-l → listening
-n → numeric
```

---

## `curl`

Transfers data from/to URLs and is commonly used to test HTTP APIs.

```bash
curl https://example.com
```

GET request:

```bash
curl http://localhost:8000/
```

POST example:

```bash
curl -X POST http://localhost:8000/login/
```

---

## `wget`

Downloads files/resources from the network.

```bash
wget https://example.com/file.zip
```

---

## `nslookup`

Queries DNS information.

```bash
nslookup example.com
```

---

## `dig`

Detailed DNS query tool.

```bash
dig example.com
```

---

## `hostname`

Displays or works with the system hostname.

```bash
hostname
```

---

# 20. SSH

## `ssh`

Connects to a remote machine.

```bash
ssh username@server
```

Specify port:

```bash
ssh -p 2222 username@server
```

---

## SSH Key Generation

```bash
ssh-keygen
```

Creates an SSH key pair.

Conceptually:

```text
Private key → kept secret
Public key  → placed on server
```

---

# 21. SCP

Copy local file to remote:

```bash
scp file.txt user@server:/home/user/
```

Copy remote file locally:

```bash
scp user@server:/home/user/file.txt .
```

Copy directory:

```bash
scp -r project/ user@server:/home/user/
```

---

# 22. rsync

Synchronize directories.

```bash
rsync -av project/ backup/
```

Remote:

```bash
rsync -av project/ user@server:/home/user/project/
```

Important idea:

```text
cp    → copies
rsync → synchronizes efficiently
```

---

# 23. Archives and Compression

## `tar`

Creates/extracts archives.

Create archive:

```bash
tar -cf archive.tar project/
```

Extract:

```bash
tar -xf archive.tar
```

Create gzip-compressed archive:

```bash
tar -czf archive.tar.gz project/
```

Extract:

```bash
tar -xzf archive.tar.gz
```

---

## `gzip`

Compresses files.

```bash
gzip file.txt
```

Decompress:

```bash
gunzip file.txt.gz
```

---

## `zip`

Creates ZIP archives.

```bash
zip archive.zip file.txt
```

Directory:

```bash
zip -r archive.zip project/
```

---

## `unzip`

Extracts ZIP archives.

```bash
unzip archive.zip
```

---

# 24. Disk Management

## `df`

Filesystem space:

```bash
df -h
```

---

## `du`

Directory/file usage:

```bash
du -sh project/
```

---

## `lsblk`

Shows block devices.

```bash
lsblk
```

---

## `mount`

Shows or mounts filesystems.

```bash
mount
```

---

## `umount`

Unmounts a filesystem.

```bash
umount /mount/point
```

---

# 25. System Information

## `uname`

Displays system information.

```bash
uname
uname -a
```

---

## `hostname`

```bash
hostname
```

---

## `uptime`

Shows how long the system has been running and load information.

```bash
uptime
```

---

## `free`

Displays memory usage.

```bash
free -h
```

---

## `lscpu`

Shows CPU information.

```bash
lscpu
```

---

## `lsmem`

Shows memory information.

```bash
lsmem
```

---

# 26. Date and Time

## `date`

Shows current date/time.

```bash
date
```

---

## `cal`

Displays a calendar on systems where the utility is installed.

```bash
cal
```

---

# 27. Processes and Resource Usage

## `time`

Measures how long a command takes.

```bash
time python program.py
```

Useful for basic performance measurement.

---

## `nice`

Starts a process with a specified niceness.

```bash
nice -n 10 command
```

---

## `renice`

Changes niceness of an existing process.

```bash
renice 10 -p PID
```

---

# 28. Logs

## `journalctl`

Reads systemd journal logs.

```bash
journalctl
```

Current boot:

```bash
journalctl -b
```

Follow logs:

```bash
journalctl -f
```

Service logs:

```bash
journalctl -u service-name
```

---

# 29. Services

## `systemctl`

Check service:

```bash
systemctl status service
```

Start:

```bash
systemctl start service
```

Stop:

```bash
systemctl stop service
```

Restart:

```bash
systemctl restart service
```

Enable at boot:

```bash
systemctl enable service
```

Disable:

```bash
systemctl disable service
```

---

# 30. Scheduled Tasks

## `crontab`

Manage user cron jobs.

View:

```bash
crontab -l
```

Edit:

```bash
crontab -e
```

Cron structure:

```text
minute hour day-of-month month day-of-week command
```

Example concept:

```text
0 2 * * * backup-command
```

Means approximately:

> Run at 2:00 AM every day.

---

# 31. Text Editors

Common terminal editors:

```text
nano
vim
vi
```

### `nano`

Simple terminal editor.

```bash
nano file.txt
```

### `vim`

Advanced terminal editor.

```bash
vim file.txt
```

---

# 32. Links

## `ln`

Creates hard links.

```bash
ln original.txt hardlink.txt
```

Symbolic link:

```bash
ln -s original.txt softlink.txt
```

---

# 33. Processes and Parent/Child Relationships

Find process:

```bash
ps aux | grep python
```

Show process tree:

```bash
pstree
```

Find PID:

```bash
pgrep python
```

Inspect a process:

```bash
ps -p PID -f
```

---

# 34. File Permissions Practical Set

### Check permissions

```bash
ls -l file.txt
```

### Make executable

```bash
chmod +x script.sh
```

### Set 755

```bash
chmod 755 script.sh
```

### Set 644

```bash
chmod 644 file.txt
```

### Change owner

```bash
chown user file.txt
```

### Change owner and group

```bash
chown user:group file.txt
```

---

# 35. Shell Script Practical

Create:

```bash
nano hello.sh
```

Content:

```bash
#!/bin/bash

name="Musthafa"

echo "Hello $name"
```

Make executable:

```bash
chmod +x hello.sh
```

Run:

```bash
./hello.sh
```

---

# 36. Shell Condition Practical

```bash
#!/bin/bash

age=20

if [ "$age" -ge 18 ]; then
    echo "Adult"
else
    echo "Minor"
fi
```

---

# 37. Shell Loop Practical

```bash
#!/bin/bash

for i in 1 2 3 4 5
do
    echo "$i"
done
```

---

# 38. Shell Function Practical

```bash
#!/bin/bash

greet() {
    echo "Hello $1"
}

greet "Musthafa"
```

---

# 39. Command-Line Argument Practical

Script:

```bash
#!/bin/bash

echo "First argument: $1"
echo "Second argument: $2"
```

Run:

```bash
./script.sh hello world
```

Output:

```text
First argument: hello
Second argument: world
```

---

# 40. File Search Practicals

### Find all Python files

```bash
find . -type f -name "*.py"
```

### Find directories

```bash
find . -type d
```

### Find files larger than 100 MB

```bash
find . -type f -size +100M
```

### Find files modified today/recently

```bash
find . -type f -mtime -1
```

---

# 41. Log Analysis Practicals

Count errors:

```bash
grep -c "ERROR" app.log
```

Show errors with line numbers:

```bash
grep -n "ERROR" app.log
```

Follow live log:

```bash
tail -f app.log
```

Find 404 requests:

```bash
grep "404" access.log
```

Count 404 responses:

```bash
grep -c "404" access.log
```

---

# 42. Process Investigation Practical

Find Python processes:

```bash
ps aux | grep python
```

Get PID:

```bash
pgrep python
```

Inspect PID:

```bash
ps -p PID -f
```

Monitor:

```bash
top
```

Send graceful termination:

```bash
kill -TERM PID
```

Force termination:

```bash
kill -KILL PID
```

---

# 43. Background Process Practical

Start:

```bash
python app.py &
```

Check:

```bash
jobs
```

Bring foreground:

```bash
fg
```

Stop/continue background jobs conceptually:

```text
Ctrl+Z → stop current foreground job
bg     → continue it in background
fg     → bring it back
```

---

# 44. SSH Practical

Connect:

```bash
ssh user@server
```

Generate key:

```bash
ssh-keygen
```

Copy a file:

```bash
scp file.txt user@server:/tmp/
```

Synchronize project:

```bash
rsync -av project/ user@server:/tmp/project/
```

---

# 45. Networking Practical

Check IP addresses:

```bash
ip addr
```

Check routes:

```bash
ip route
```

Test reachability:

```bash
ping 8.8.8.8
```

Test DNS:

```bash
nslookup example.com
```

Inspect connections:

```bash
ss -tuln
```

Test HTTP:

```bash
curl http://localhost:8000/
```

---

# 46. Localhost Web Server Practical

For a Django server:

```bash
python manage.py runserver
```

Then test:

```bash
curl http://127.0.0.1:8000/
```

You can inspect HTTP status and response using curl options.

---

# 47. Port Investigation

Check listening TCP/UDP sockets:

```bash
ss -tuln
```

Find a particular port:

```bash
ss -tuln | grep 8000
```

This is useful when debugging:

> "Why is my application not accessible?"

---

# 48. Disk Investigation Practical

Filesystem usage:

```bash
df -h
```

Directory usage:

```bash
du -sh *
```

Find large files:

```bash
find . -type f -size +100M
```

---

# 49. Permission Debugging Practical

Check:

```bash
ls -l file.txt
```

Inspect metadata:

```bash
stat file.txt
```

Change permissions:

```bash
chmod 644 file.txt
```

Change owner:

```bash
chown user:group file.txt
```

---

# 50. Environment Practical

Check:

```bash
echo "$PATH"
```

Set variable:

```bash
export APP_ENV="development"
```

Check:

```bash
echo "$APP_ENV"
```

Run another process:

```bash
python app.py
```

The child process can normally inherit exported environment variables.

---

# 51. Pipes — Advanced Practical

Find Python processes and count them:

```bash
ps aux | grep python | wc -l
```

Find errors and sort:

```bash
grep "ERROR" app.log | sort
```

Find unique error messages:

```bash
grep "ERROR" app.log | sort | uniq
```

Count unique values:

```bash
grep "ERROR" app.log | sort | uniq -c
```

---

# 52. Redirection — Advanced Practical

Save output:

```bash
ps aux > processes.txt
```

Append:

```bash
ps aux >> processes.txt
```

Save errors:

```bash
command 2> errors.txt
```

Save output and errors separately:

```bash
command > output.txt 2> errors.txt
```

---

# 53. Combining `find` + `grep`

Find Python files containing `django`:

```bash
find . -type f -name "*.py" -exec grep -l "django" {} \;
```

This is a strong practical example because it combines:

```text
find → filesystem search
grep → content search
```

---

# 54. Combining `ps` + `grep`

```bash
ps aux | grep nginx
```

Logic:

```text
ps       → list processes
    ↓
pipe
    ↓
grep     → filter nginx
```

---

# 55. Combining `du` + `sort`

Find largest directories/files from current directory:

```bash
du -sh * | sort -h
```

Reverse order:

```bash
du -sh * | sort -hr
```

---

# 56. `awk` Practical

Suppose:

```text
101 Musthafa 90
102 Ali 85
103 John 95
```

Print names:

```bash
awk '{print $2}' students.txt
```

Print names and marks:

```bash
awk '{print $2, $3}' students.txt
```

Find marks greater than 90:

```bash
awk '$3 > 90 {print $2, $3}' students.txt
```

---

# 57. `sed` Practical

Replace text:

```bash
sed 's/old/new/g' file.txt
```

Delete lines containing a pattern:

```bash
sed '/ERROR/d' file.txt
```

Print a specific range:

```bash
sed -n '1,10p' file.txt
```

---

# 58. `cut` Practical

Given:

```text
1,Muhammed,Python
2,Ali,Django
3,John,SQL
```

Get usernames:

```bash
cut -d ',' -f 2 users.csv
```

Get technology:

```bash
cut -d ',' -f 3 users.csv
```

---

# 59. Archive Practical

Create:

```bash
tar -czf project.tar.gz project/
```

List:

```bash
tar -tzf project.tar.gz
```

Extract:

```bash
tar -xzf project.tar.gz
```

---

# 60. Service Debugging Practical

Check service:

```bash
systemctl status nginx
```

Check logs:

```bash
journalctl -u nginx
```

Restart:

```bash
systemctl restart nginx
```

This gives a useful troubleshooting flow:

```text
Service not working
       ↓
systemctl status
       ↓
journalctl
       ↓
Find error
       ↓
Fix
       ↓
restart
       ↓
test again
```

---

# 61. Full Linux Troubleshooting Workflow

When a web application is not working:

### Step 1 — Is the process running?

```bash
ps aux | grep python
```

### Step 2 — Is the port listening?

```bash
ss -tuln | grep 8000
```

### Step 3 — Can localhost reach it?

```bash
curl http://127.0.0.1:8000/
```

### Step 4 — Check logs

```bash
journalctl
```

or application logs.

### Step 5 — Check permissions

```bash
ls -l
```

### Step 6 — Check disk space

```bash
df -h
```

### Step 7 — Check memory

```bash
free -h
```

### Step 8 — Check CPU/processes

```bash
top
```

---

# 62. Maximum Practical Challenges

These are the practical questions you should be able to solve without looking at notes.

## Level 1 — Basic

1. Show your current directory.
2. List hidden files.
3. Create a directory.
4. Create three files.
5. Rename a file.
6. Move a file.
7. Copy a file.
8. Delete a file.
9. Remove an empty directory.
10. Display file contents.
11. Display the first 10 lines.
12. Display the last 10 lines.
13. Check file type.
14. Check file metadata.
15. Count lines in a file.

---

## Level 2 — Filesystem

16. Find all `.py` files.
17. Find all directories.
18. Find files larger than 10 MB.
19. Find files modified recently.
20. Find a file by exact name.
21. Search for a word inside a file.
22. Search recursively.
23. Search case-insensitively.
24. Show matching line numbers.
25. Count matching lines.
26. Find a file and search its contents.
27. Find the largest files.
28. Find disk usage of a directory.
29. Check filesystem free space.

---

## Level 3 — Permissions

30. Check permissions.
31. Give a script execute permission.
32. Set permission to 755.
33. Set permission to 644.
34. Remove write permission.
35. Change file owner.
36. Change group ownership.
37. Check current umask.
38. Explain what umask does.
39. Determine what permissions a new file normally receives.
40. Explain owner/group/others.

---

## Level 4 — Processes

41. List running processes.
42. Find a Python process.
43. Find its PID.
44. Find its parent process.
45. Monitor CPU and memory.
46. Show process tree.
47. Start a process in background.
48. List background jobs.
49. Bring a job to foreground.
50. Continue a stopped job in background.
51. Send SIGTERM.
52. Send SIGKILL.
53. Explain zombie process.
54. Explain orphan process.
55. Identify which process is using a particular port.

---

## Level 5 — Pipes & Redirection

56. Redirect command output to a file.
57. Append output.
58. Redirect errors.
59. Separate stdout and stderr.
60. Pipe output into grep.
61. Pipe output into wc.
62. Sort output.
63. Remove duplicates.
64. Count duplicates.
65. Extract a specific field.
66. Replace text using sed.
67. Filter rows using awk.

---

## Level 6 — Networking

68. Find your IP address.
69. Display routing table.
70. Test IP reachability.
71. Test DNS resolution.
72. Find listening ports.
73. Test localhost.
74. Test an HTTP endpoint.
75. Check which service is listening on a port.
76. Connect to a remote server using SSH.
77. Generate SSH keys.
78. Copy a file using SCP.
79. Synchronize a directory using rsync.

---

## Level 7 — System Administration

80. Check CPU information.
81. Check memory.
82. Check disk space.
83. Check system uptime.
84. Check hostname.
85. Check logged-in users.
86. Check your user ID.
87. Check environment variables.
88. Set an environment variable.
89. Find the executable location of a command.
90. Read a command's manual.
91. Check system services.
92. Start a service.
93. Stop a service.
94. Restart a service.
95. Check service logs.
96. Follow live logs.

---

## Level 8 — Shell Scripting

97. Write a Hello World script.
98. Create a variable.
99. Read a command-line argument.
100. Write an if/else condition.
101. Write a loop.
102. Write a function.
103. Check whether a file exists.
104. Check whether a directory exists.
105. Read a file line by line.
106. Count files in a directory.
107. Create a backup script.
108. Create a log-cleaning script.
109. Write a script that checks disk usage.
110. Write a script that checks whether a process is running.

---

# 63. ⭐ Maximum Reviewer Practical Scenarios

These are especially important because reviewers often ask **"How would you troubleshoot this?"** rather than simply asking for a command.

## Scenario 1 — Python server is not opening

Think:

```text
1. Is process running?
2. Is port listening?
3. Can localhost connect?
4. Are there application errors?
5. Is firewall involved?
```

Useful concepts:

```bash
ps
ss
curl
logs
```

---

## Scenario 2 — Permission denied

Think:

```text
1. Check permissions
2. Check owner
3. Check group
4. Check parent-directory permissions
5. Check current user
6. Use sudo only if appropriate
```

Concepts:

```bash
ls -l
stat
id
whoami
chmod
chown
```

---

## Scenario 3 — Disk is full

Think:

```text
1. Check filesystem usage
2. Find large directories
3. Find large files
4. Inspect logs
5. Remove/archive unnecessary data
```

Concepts:

```bash
df -h
du -sh
find
```

---

## Scenario 4 — Process is consuming too much CPU

Think:

```text
1. Identify process
2. Find PID
3. Inspect resource usage
4. Determine whether it is expected
5. Investigate/profile
6. Stop gracefully if necessary
```

Concepts:

```bash
top
ps
pgrep
kill
profiling
```

---

## Scenario 5 — Application is slow

Think:

```text
Application slow
      ↓
Check CPU
      ↓
Check memory
      ↓
Check disk
      ↓
Check network
      ↓
Check application logs
      ↓
Profile application
      ↓
Find bottleneck
```

---

## Scenario 6 — Port already in use

Think:

```text
Check listening sockets
        ↓
Find PID/process
        ↓
Determine whether process is required
        ↓
Stop/reconfigure process
        ↓
Start application again
```

Useful concept:

```bash
ss -tuln
ps
```

---

## Scenario 7 — Find all Django files containing a specific word

Concept:

```text
find → locate Python files
grep → search their contents
```

---

## Scenario 8 — Monitor a log continuously

Concept:

```text
tail -f
```

Use it when debugging applications or services that continuously write logs.

---

## Scenario 9 — Securely move a project to another machine

Concept:

```text
SSH  → remote access
SCP  → file transfer
rsync → synchronization
```

---

## Scenario 10 — Service failed to start

Think:

```text
systemctl status
        ↓
journalctl
        ↓
identify error
        ↓
fix configuration/permission/dependency
        ↓
restart
        ↓
verify
```

---

# 64. Commands You Must Know for Review

### 🔴 Must Master

```text
pwd
ls
cd
mkdir
touch
cp
mv
rm
cat
head
tail
find
grep
chmod
chown
umask
ps
top
kill
jobs
fg
bg
echo
export
sudo
su
df
du
ip
ping
ss
curl
ssh
scp
tar
systemctl
journalctl
```

### 🟠 Strongly Know

```text
file
stat
wc
sort
uniq
cut
tr
awk
sed
pgrep
pstree
pkill
nice
renice
env
printenv
which
whereis
type
history
rsync
wget
nslookup
dig
free
uname
uptime
lscpu
crontab
ln
mount
umount
```

### 🟢 Advanced / Good to Know

```text
xargs
tee
xargs + find
awk + grep
sed + grep
process substitution
named pipes
lsof
strace
vmstat
iostat
sar
journalctl filtering
systemd units
```

---

# 65. Final Command Mental Map

```text
NAVIGATION
pwd ls cd mkdir rmdir

FILES
touch cp mv rm cat less head tail file stat

SEARCH
find grep

TEXT
sort uniq cut tr awk sed wc

PERMISSIONS
chmod chown chgrp umask sudo su

PROCESSES
ps top htop pgrep pidof pstree kill pkill jobs fg bg

INPUT/OUTPUT
stdin stdout stderr
> >> < 2> 2>&1 |

NETWORK
ip ping ss curl wget
nslookup dig
hostname

REMOTE
ssh ssh-keygen scp rsync

ARCHIVES
tar gzip gunzip zip unzip

SYSTEM
uname uptime free lscpu df du lsblk

SERVICES
systemctl journalctl

SCHEDULING
cron crontab

ENVIRONMENT
env printenv export echo

DEBUGGING
time
strace
logs
profiling

USER MANAGEMENT
whoami id who w users passwd

FILESYSTEM
mount umount ln

SHELL SCRIPTING
variables
conditions
loops
functions
arguments
exit codes
```

# ⭐ Final Practical Rule

For the review, don't just memorize:

> "What does `grep` do?"

Be able to answer:

> "`grep` searches text for matching patterns. For example, if I have a Django log file and want to find all ERROR lines, I can use grep. I can combine it with a pipe to filter output from another command."

That style demonstrates **definition + purpose + real-world use + command logic**, which is much stronger in a reviewer discussion.
