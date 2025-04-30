# OverTheWire Bandit: Level 6 → Level 7 Walkthrough

## Hey, It’s Me!
I’m a cybersecurity student diving into pentesting, and this is my walkthrough for Bandit Level 6 → 7. Let’s find that password!

## Problem
The challenge states the password for Level 7 is located somewhere on the server that is owned by user bandit7 and group bandit6, with 33 bytes in size.
We need to search the server rather than searching the home directory.
> For unexplained commands, please refer to past levels in this repository.

## Solution
### Step 1: Explore the Directory
Check the current directory:
```
ls
```
> No output is returned, indicating the directory is empty.

Let’s check for hidden files:
```
ls -a
```
> .  ..  .bash_logout  .bashrc  .profile

Only standard hidden configuration files are present, so the password isn’t here.</br>
The challenge mentions the file is “somewhere on the server,” suggesting we need to search the entire filesystem.

### Step 2: List Server Contents
To confirm the server’s structure, list the root directory:
```
ls /
```
> bin  boot  dev  drifter  etc  formulaone  home  krypton  lib  lib32  lib64  libx32  lost+found  media  mnt  opt  proc  root  run  sbin  snap  srv  sys  tmp  usr  var

The server has many directories, and manually checking them would be inefficient. I need to use the find command to locate the file based on the given criteria.

### Step 3: Use the find Command
We need a file that is:

- A regular file (-type f)
- Exactly 33 bytes (-size 33c)
- Owned by user bandit7 (-user bandit7)
- Owned by group bandit6 (-group bandit6)

Let’s run the find command starting from the root directory (/):
```
find / -type f -size 33c -user bandit7 -group bandit6
```
> Many “Permission denied” errors occur because bandit6 lacks access to certain directories.

Among the errors, one file named: /var/lib/dpkg/info/bandit7.password.</br>
Obviously, this is the wanted file. In order to increase our skills, let's try to hide the errors.
- A user (e.g., bandit7) is an account with a unique ID (UID) that has permissions to access files and run commands.
- A group (e.g., bandit6) is a collection of users sharing specific permissions. Files have a user owner and a group owner,

### Step 4: Filter Errors
To clean up the output by suppressing error messages, we redirect errors to /dev/null:
```
find / -type f -size 33c -user bandit7 -group bandit6 2> /dev/null
```
> /var/lib/dpkg/info/bandit7.password

This confirms the file’s location without error messages.

- `2>` redirects the error messages.
- `/dev/null` is a special file that discards all data written to it.
- `2> /dev/null` suppresses error messages, showing only the command’s successful output.

### Step 5: Alternative Filtering with grep
To further confirm the file, we can filter the output for the keyword bandit7:
```
find / -type f -size 33c -user bandit7 -group bandit6 | grep bandit7
```
This highlights /var/lib/dpkg/info/bandit7.password.</br>
However, this step is optional since 2> /dev/null already provided a clean result.

### Step 6: Read the File
Now, let’s read the file’s contents:
```
cat /var/lib/dpkg/info/bandit7.password
```
> password_for_Level_7.

This is the password for Level 7!

## Learnables from this Level
- Linux Command: `find` searches filesystems with specific criteria like ownership (-user, -group) and size (-size). Explore options with man find.
- Users and Groups: Files are owned by a user and group, controlling access. You can check ownership for files with ls -l.
- Error Suppression: `2> /dev/null` discards error messages, cleaning up command output. This is crucial in pentesting to focus on relevant results.
- Enumeration skill: Searching an entire server (/) efficiently with find is a key pentesting skill for locating files when their location is unknown.

## What’s Next?
Ready for Level 7! Connect using:
`
ssh bandit7@bandit.labs.overthewire.org -p 2220
`
Paste the password password_for_Level_7. Let’s keep going! See you in [Level7-8](Level7-8.md).
