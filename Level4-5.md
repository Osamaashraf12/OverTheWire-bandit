# OverTheWire Bandit: Level 4 → Level 5 walkthrough

## Hey, It’s Me!
I’m diving into pentesting as a cybersecurity student, and this is my walkthrough for Bandit Level 4 → 5. Let’s find that password!

## Problem
The challenge states the password for the next level is in the only human-readable file in the inhere directory. Our task is to identify and read this file.
> For unexplained commands, please refer to past levels in this repository.

## Setup
Ignoring this step from next walkthrough.

## Solution
### Step 1: Get the Password from Level 2 and connect to the server
Ignoring this step from next walkthrough.

### Step 2: Explore the Directory
Let’s check the current directory:
```
ls
```
> inhere

The challenge mentions the inhere directory, so let’s move into it:
```
cd inhere
```

### Step 3: List Files
Let’s see what’s inside:
```
ls
```
> -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09

There are multiple files, all prefixed with a dash (-). The challenge says only one is human-readable, but what does that mean? Human-readable files typically contain ASCII text (like passwords), while others might be binary or encoded data.

### Step 4: Attempt to Read a File
Let’s try reading one file to understand its contents:
```
cat -file00
```
> Error: cat: invalid option -- 'f'

The dash (-) in the filename confuses cat. It reminds me of a past level. To read the file, we need to specify the full path or use ./ to avoid this issue:
```
cat /home/bandit4/inhere/-file00
```
> ŉOT   S  plS]-EH t :- Z

This looks like unreadable binary or encoded data, not human-readable text. This aligns with the challenge: most files are not human-readable, and we need to find the one that is.

### Step 5: Find the Human-Readable File
I explored two approaches to solve this, both useful for learning:

#### Option 1: Manually Check Files
Since there are only 10 files, we could read each one:
```
cat /home/bandit4/inhere/-file01
cat /home/bandit4/inhere/-file02
...
cat /home/bandit4/inhere/-file07
```
> password_for_Level_4

File -file07 contains readable ASCII text, which looks like the password! This approach works but isn't that smart.

#### Option 2: Use the file Command (Smarter Approach)
To identify the human-readable file efficiently, we can check the file types:
```
file /home/bandit4/inhere/-file0*
```
- `file` displays type of data in files.
- `*` means that any value can be here.
> 
> /home/bandit4/inhere/-file00: PGP Secret Sub-key -
> /home/bandit4/inhere/-file01: data
> /home/bandit4/inhere/-file02: data
> /home/bandit4/inhere/-file03: data
> /home/bandit4/inhere/-file04: data
> /home/bandit4/inhere/-file05: data
> /home/bandit4/inhere/-file06: data
> /home/bandit4/inhere/-file07: ASCII text
> /home/bandit4/inhere/-file08: data
> /home/bandit4/inhere/-file09: data

The `file` command identifies -file07 as ASCII text, while others are binary or data. This confirms -file07 is the human-readable file. Let’s read it:
`
cat /home/bandit4/inhere/-file07
`
> password_for_Level_5

This is the password for Level 5!

### Step 6: Leave the Server and save the file in my terminal
Ignoring this step from next walkthrough.


## Learnables from this Level
- Linux Command: The `file` command analyzes file types, making it a powerful tool for pentesting when you need to identify specific file formats (e.g., text vs. binary).
- Human-Readable Files: In Linux, human-readable files typically contain ASCII text (e.g., passwords, scripts). Binary or encoded files are not human-readable.
- Handling Special Characters: Files with dashes (-) can cause issues with commands like `cat`. Use full paths (e.g., /home/bandit4/inhere/-file00) or ./-file00 to access them.
- Enumeration concept: Manually checking files works for small sets, but tools like file or find are more efficient for larger directories, a key skill in pentesting.

## What’s Next?
Ready for Level 5! Connect using:
```
ssh bandit5@bandit.labs.overthewire.org -p 2220
```
Paste the password (password_for_level_5). Let’s keep going! See you in [Level5-6](Level5-6.md).
