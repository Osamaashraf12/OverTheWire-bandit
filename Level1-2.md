# OverTheWire Bandit: Level 1 → Level 2 Writeup

## Hey, It’s Me!
I’m Osama, a student learning cybersecurity. This is my writeup for Bandit Level 1 → 2, my next step in pentesting writeups. Let’s find that password!

## Problem
Find a password in a file named -. That’s our target! WARNING: Not all file names are accessible.

## Setup
- A terminal (I’m using Kali Linux, but any terminal works).
- Know how to type simple commands (I’ll explain them!). 
> For unexplained commands, please refer to [Level0-1](Level0-1.md)

## Solution
### Step 1: Get the Password from Level 0
> If you’re stuck at the password prompt, press Ctrl+C to return to your terminal.

Before connecting, I need the password from Level 0. It’s in a file I saved earlier. Let’s find it:
```
locate p0.txt
```
- _locate_ searches for files on my computer.
> It shows /home/kali/bandit/p0.txt.

Now read it:
```
cat /home/kali/bandit/p0.txt
```
> I see the password (password_from_level_0). I copied it.

### Step 2: Connect to the Server
Now let’s connect to the Bandit server:
```
ssh bandit1@bandit.labs.overthewire.org -p 2220
```
> It asks for the password. I pasted the one from p0.txt. I’m in!

### Step 3: Look Around
Let’s see what’s here:
```
ls
```
> Guess what? It shows -. Wow, that’s the file we need!

### Step 3: Alternative File Search
I want to learn, not just win. Let’s try finding the - file with other commands. First, I tried:
```
locate -
```
> But it says “Command ‘locate’ not found” and suggests installing it. I tried installing it with admin privileges:
```
sudo apt install plocate
```
- _sudo_ runs commands as an admin.
> But it failed because I don’t have admin rights. That makes sense, no admin powers in a wargame!

Let’s try another command:

```
find -
```
- _find_ searches for files in the current directory.
> Yahhoo! It shows -. So, _find_ works, but _locate_ doesn’t here.

### Step 4: Read the File
Now let’s read the - file:
```
cat -
```
> Weird! Nothing shows up, and it hangs. Maybe the - name is tricky? I pressed Ctrl+C to stop it.

The - name looks like a command option, not a file. Let’s try using the full path (to tell the system it’s a file not a command option). 
First, check where I am:
```
pwd
```
- _pwd_ shows my current directory.
> It says /home/bandit1. So the file’s path is /home/bandit1/-. Let’s try:
```
cat /home/bandit1/-
```
> It works! I see the password for Level 2. I copied it.

### Step 4: Alternative File Read
I love learning, so let’s try another way: redirection:
```
cat < -
```
- _<_ sends a file’s content to _cat_ (unlike _>_, which sends output to a file).
> It shows the password again! Two ways to read the file, perfect!

### Step 5: Leave the Server
Time to go back to my terminal:
```
exit
```
> It says “logout,” and I’m back on my Kali machine.

### Step 6: Save the Password
Let’s save the password so I don’t forget. I’ll use the same directory as before:
```
cd /home/kali/bandit/
```
- _cd_ changes to a directory.
If I forgot the path, I can find it:
```
locate p0.txt
```
> It shows /home/kali/bandit/p0.txt, so I’m in the right place.

Now save the password:
```
echo 'password_from_level_1' > p1.txt
```
Replace password_from_level_1 with the password you copied.
Let’s check:
```
ls
```
> It shows p0.txt and p1.txt. The password is saved!

### Learnables from this level:
- Linux commands: _pwd_ to check my directory, _cd_ to move directories, _find_ to search files, _locate_ (but it didn’t work in the SSH server).
- Redirection:_ >_ saves output to a file, _<_ sends a file to a command. These are super useful in pentesting to handle files and data.
File names: Weird names like - can trick commands like cat. Using paths or redirection fixes it. This happens in real systems too!

What’s Next?
Let’s keep going! For Level 2, use:
```
ssh bandit2@bandit.labs.overthewire.org -p 2220
```
Paste the password you found. Good luck! See you in [Level2-3](Level2-3.md).
