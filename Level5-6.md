# OverTheWire Bandit: Level 5 → Level 6 Walkthrough

## Hey, It’s Me!
I’m a cybersecurity student diving into pentesting, and this is my walkthrough for Bandit Level 5 → 6. Let’s find that password!

## Problem
The challenge states the password for Level 6 is in the inhere directory, in a file that is human-readable, 1033 bytes in size and not executable.</br>
We need to know how to find a file with some specifications.
> For unexplained commands, please refer to past levels in this repository.


## Solution
### Step 1: Explore the Directory
Check the current directory:
```
ls
```
> inhere

The challenge points to the inhere directory, so let’s move into it:
```
cd inhere
```

### Step 2: List Files
List the contents of the inhere directory:
```
ls
```
> maybehere00  maybehere04  maybehere08  maybehere12  maybehere16
> 
> maybehere01  maybehere05  maybehere09  maybehere13  maybehere17
> 
> maybehere02  maybehere06  maybehere10  maybehere14  maybehere18
> 
> maybehere03  maybehere07  maybehere11  maybehere15  maybehere19

There are 20 directories, each likely containing files. Manually checking each one would be unprofessional, so we need a smarter approach to find the file matching the criteria.

### Step 3: Use the find Command
To locate the file efficiently, we use the find command with the given specifications. Let’s break down the command used:
```
find . -type f -size 1033c -not -executable -exec file {} + | grep ASCII
```
> ./maybehere07/.file2: ASCII text, with very long lines (1000)

- `.` specifies the starting point for the search, which is the current directory (inhere). It searches through all subdirectories.
- `-type f` restricts the search to files (not directories).
- `-size 1033c` matches files exactly 1033 bytes in size (c for bytes).
- `-not -executable` filters non executable files.
- `-exec` tells `find` to run a command (`file` in our case) on the files it finds.
- `file` identifies the type of each file (e.g., ASCII text, binary).
- `{}` represents each file found by `find`. It gets replaced with the actual file paths.
- `+` Groups all matching files and runs the `file` command on them together.
- `-exec file {} +` executes (runs) `file` command on all matching files to determine their type (e.g., ASCII text, binary).
- `|` passes the output of the `find` command to the next command (which is `grep`).
- `grep ASCII` filters the output to show only files containing the word 'ASCII' (which means human-readable).

This command identifies the file ./maybehere07/.file2 as ASCII text.

### Step 4: Read the File
Now that we know the file’s location, let’s read its contents:
```
cat ./maybehere07/.file2
```
> password_for_Level_6.

This is the password for Level 6! Use it to keep going! See you in [Level6-7](Level6-7.md).

## Learnables from this Level
- Linux Command: `find` is a powerful tool for searching files based on criteria like type, size, and permissions. Use `man` to explore commands options.
- Piping `|`: Combines commands (e.g., find with grep).
