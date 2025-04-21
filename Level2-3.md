# OverTheWire Bandit: Level 2 → Level 3 Writeup

## Hey, It’s Me!
I’m Osama, a student learning cybersecurity. This is my writeup for Bandit Level 2 → 3, my next step in pentesting writeups. Let’s find that password!

## Problem
Find a password in a file named spaces in this filename in the home directory. WARNING: File names with spaces can be tricky!

## Setup
- A terminal (I’m using Kali Linux, but any terminal works).
- Know how to type simple commands (I’ll explain them!).
> For unexplained commands, please refer to past levels in this repository.

## Solution
### Step 1: Get the Password for Level 2
Before connecting, I need the password from Level 1. It’s in a file I saved earlier [Level1-2](Level1-2.md). Let’s find it:
```
locate p1.txt
cat /home/kali/bandit/p1.txt
```
> I see the password (password_for_level_3).

I copied it.

### Step 2: Connect to the Server
Now let’s connect to the Bandit server:
```
ssh bandit2@bandit.labs.overthewire.org -p 2220
```
> It asks for the password.

I pasted the one from p2.txt. I’m in! If you’re stuck at the password prompt, press Ctrl+C to return to your terminal.

### Step 3: Look Around
I didn’t get the challenge at first, but let’s try:
```
ls
```
> It shows "spaces in this filename".

I get it now. the file name has spaces!

### Step 4: Read the File
Let’s read the file:
```
cat spaces in this filename
```
> Hhhmmmm, it fails! It says “No such file or directory” for each word.

Makes sense. Spaces aren’t normal in file names, so cat thinks they’re separate files.

### Step 5: Read with Escaped Spaces
The spaces are special characters. To read them, I put a \ before each space to escape it:
```
cat spaces\ in\ this\ filename
```
> Yahhoo! It works! I see the password for Level 3.

I copied it.

### Step 5: Alternative File Read
I love learning, so let’s try another way—put the whole name in quotes to treat it as one string:
```
cat "spaces in this filename"
```
- " makes the system see the name as one piece.
> It shows the password again!

Two ways to read the file, perfect!

### Step 6: Leave the Server
Time to go back to my terminal:
```
exit
```
> It says “logout,” and I’m back on my Kali machine.

### Step 7: Save the Password
Let’s save the password so I don’t forget. I’ll use the same directory:
```
cd /home/kali/bandit/
echo 'password_for_level_3' > p3.txt
```
Replace password_for_level_3 with the password you copied.

## Learnables from this level:
- Special characters: Spaces in file names are tricky. Use \ to escape them or " to quote the name. This is common in pentesting when exploring weird file systems.
- File names: Unusual names (like spaces or - from Level1-2) need special handling, which happens in real-world systems too!

What’s Next?
Let’s keep going! For Level 3, use:
```
ssh bandit3@bandit.labs.overthewire.org -p 2220
```
Paste the password you found. Good luck! See you in [Level3-4](Level3-4.md).
