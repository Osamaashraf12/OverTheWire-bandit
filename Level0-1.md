# OverTheWire Bandit: Level 0 → Level 1 Writeup

## Hey, It’s Me!
I’m Osama, a student learning cybersecurity. This is my writeup for Bandit Level 0 → 1, my first step in pentesting writeups!

## Problem
Look for a file named readme where the password is stored.

## Setup
- A terminal (I’m using Kali Linux, but any terminal works).
- Know how to type simple commands (don’t worry, I’ll explain them!).

## Solution
### Step 1: Connect to the Server
To start, use this command to connect to the Bandit server:
```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
- `ssh` is a tool to connect to another computer safely.
- `bandit0` is the username for Level 0 (mentioned by Bandit's website).
- `bandit.labs.overthewire.org` is the server’s address (mentioned by Bandit's website).
- `-p 2220` means use port 2220 (mentioned by Bandit's website).
It asked for a password, type bandit0. You’re in! You’ll see a big welcome message.

### Step 2: Look Around
You might not know what to do at first, but let’s see what’s here. use this command:
```
ls
```
- `ls` shows all files in the current spot (directory).
And guess what? It shows readme. Wow, that’s the file we need!

### Step 3: Open the File
Now I wanted to read the readme file. I tried this:
```
cat readme
```
- `cat` is a command to show what’s inside a file.
It worked! You can see a message saying “Congratulations” and some rules, plus the password for Level 1.<br/> I won’t write the password here (rules say no spoilers!), copy it down.

### Step 4: Leave the Server
After getting the password, go back to your terminal. type:
```
exit
```
- `exit` closes the connection and logs out.
It said “logout,”. Now we’re back on our Kali machine..

### Step 5: Save the Password
We don't want to forget the password, so we need to save it in the terminal. First, make a folder:
```
mkdir bandit
```
- `mkdir` makes a new folder (directory).<br/>

Then, save the password in a file:
```
echo 'password_for_level_1' > bandit/p1.txt
```
- `echo` prints something.
- `>` puts that something into a file.
- `password_for_level_1` is the password you copied. Replace password_for_level_1 with the password you copied from cat readme.
- `bandit/p1.txt` is the path to the directory ‘bandit’ + the name of the file to save 'p1.txt'.<br/>
The password is now in bandit/p1.txt.

## Learnables from this level:
- Linux commands: `ls` to look around, `cat` to read files, `mkdir` to make a directory, `echo` to print text. These are used in real pentesting to explore systems.
- Redirection operator: `>` to put text into a file.

## What’s Next?
To start Level 1, use:
```
ssh bandit1@bandit.labs.overthewire.org -p 2220
```
Paste the password you found. Good luck! See you in the next write up [Level1-2](Level1-2.md).
