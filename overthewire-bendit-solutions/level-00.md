# Bandit Level 0 → Level 1

## Objective
Connect to the Bandit game server via SSH and locate the password for Level 1.

## Environment
- **Connection:** SSH
- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **User:** `bandit0`

## Commands Used
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
ls
cat <readme>
```

## Command Breakdown
| Command | Purpose |
|---|---|
| `ssh` | Opens a secure remote connection to another machine |
| `bandit0@...` | Specifies the username and target host |
| `-p 2220` | Connects on port 2220 instead of the SSH default (22) |
| `ls` | Lists files in the current directory |
| `cat` | Prints a file's contents to the terminal |

## Approach
1. Connected to the server using the SSH command above and the initial password provided on the Bandit website.
2. Ran `ls` to see what files were present in the home directory.
3. Used `cat` on the relevant file to reveal the password for Level 1.

## Key Takeaway
SSH is the standard way to access remote Linux systems securely — a core skill for any DevSecOps or infrastructure role. `ls` and `cat` are the two most basic commands for exploring a filesystem.

## Result
✅ Password for Level 1 retrieved successfully.
