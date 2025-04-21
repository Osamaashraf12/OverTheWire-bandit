# OverTheWire Bandit: Level 3 → Level 4 Writeup

## Hey, It’s Me!
I’m Osama, a cybersecurity student diving deeper into pentesting. This is my writeup for Bandit Level 3 → 4. Let’s hunt for that password!

## Problem
The challenge says the password is in a hidden file located in the inhere directory. Our mission is to find and read a hidden file.

## Setup
- A terminal (I’m on Kali Linux, but any terminal works).
- Basic command knowledge (I’ll explain each step clearly!).
> For unexplained commands, please refer to past levels in this repository.

## Solution
### Step 1: Get the Password for Level 3 and connect to the server
You became better than me in this step

### Step 2: Explore the Directory
Let’s see what’s available:
```
ls
```
> It shows a directory named inhere.

That matches the challenge description, so let’s dive in:
```
cd inhere
```
> I’m now in /home/bandit2/inhere.

### Step 3: Search for the Hidden File
The challenge mentions a hidden file, let’s list files and explore:
```
ls
```
> Nothing shows up! That’s odd.

Maybe the file is hidden? In Linux, hidden files start with a dot (.) and don’t appear with a regular ls. Let’s try listing all files, including hidden ones:
```
ls -a
```
- `-a` shows all files, including hidden ones (like . and .., which refer to directories).
> It shows: . .. ...Hiding-From-You

There it is! A file named ...Hiding-From-You. The name suggests it’s trying to stay sneaky, but we found it.

### Step 4: Read the Hidden File
Let’s read the file to get the password:
```
cat ...Hiding-From-You
```
> Now I have the password for Level 4! I copied it.

### Step 5: Leave the Server and save the file in my terminal
```
exit
cd /home/kali/bandit/
echo 'password_for_Level_4' > p4.txt
```

## Learnables from this Level
- Hidden Files: In Linux, files starting with a dot (.) are hidden and won’t show with a regular ls. Use `ls -a` to reveal them. This is common in real systems for configuration files or sensitive data.
- Command Options: The `-a` flag for `ls` is super useful for pentesting when files might be hidden intentionally.
- Enumeration: Always check for hidden files, directories, or processes in pentesting. Tools like `ls -a` or `find` are your friends!

## What’s Next?
Ready for Level 4! Connect using:
```
ssh bandit4@bandit.labs.overthewire.org -p 2220
```
Paste the password you found. Let’s keep going! See you in [Level4-5](Level4-5.md).
