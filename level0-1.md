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
- _ssh_ is a tool to connect to another computer safely.
- _bandit0_ is the username for Level 0 (mentioned by Bandit's website).
- _bandit.labs.overthewire.org_ is the server’s address (mentioned by Bandit's website).
- _-p 2220_ means use port 2220 (mentioned by Bandit's website).
It asked for a password, type bandit0. You’re in! You’ll see a big welcome message.

### Step 2: Look Around
You might not know what to do at first, but let’s see what’s here. use this command:
```
ls
```
- _ls_ shows all files in the current spot (directory).
And guess what? It shows readme. Wow, that’s the file we need!

### Step 3: Open the File
Now I wanted to read the readme file. I tried this:
```
cat readme
```
- _cat_ is a command to show what’s inside a file.
It worked! You can see a message saying “Congratulations” and some rules, plus the password for Level 1. I won’t write the password here (rules say no spoilers!), copy it down.

### Step 4: Leave the Server
After getting the password, go back to your terminal. type:
```
exit
```
- _exit_ closes the connection and logs out.
It said “logout,”. Now we’re back on our Kali machine..

### Step 5: Save the Password
We don't want to forget the password, so we need to save it in the terminal. First, make a folder:
```
mkdir bandit
```
- _mkdir_ makes a new folder (directory).<br/>

Then, save the password in a file:
```
echo 'password_from_level_0' > bandit/p0.txt
```
- _echo_ prints something.
- _>_ puts that something into a file.
- _password_from_level_0_ is the password you copied. Replace password_from_level_0 with the password you copied from cat readme.
- _bandit/p0.txt_ is the path to the directory ‘bandit’ + the name of the file to save 'p0.txt'.<br/>
The password is now in bandit/p0.txt.

## Learnables from this level:
- Linux commands: _ls_ to look around, _cat_ to read files, _mkdir_ to make a directory, _echo_ to print text. These are used in real pentesting to explore systems.
- Redirection operator: _>_ to put text into a file.

## What’s Next?
To start Level 1, use:
```
ssh bandit1@bandit.labs.overthewire.org -p 2220
```
Paste the password you found. Good luck! See you in the next write up [Level1-2](Level1-2.md).
