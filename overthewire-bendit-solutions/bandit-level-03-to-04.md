# Bandit Level 3 → Level 4

## Objective
The password for the next level is stored in a hidden file inside the `inhere` directory.

## Environment
- **Connection:** SSH
- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **User:** `bandit3`

## Commands Used
```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
ls
cd inhere
ls
ls -la
cat .*
# Alternative:
cat ./...Hiding-From-You
```

## Command Breakdown
| Command | Purpose |
|---|---|
| `ssh bandit3@... -p 2220` | Connects to the Bandit server as `bandit3` on port 2220 |
| `ls` | Lists files in the current directory (the `inhere` folder looks empty because hidden files are skipped) |
| `cd inhere` | Moves into the `inhere` directory |
| `ls -la` | Lists all files, including hidden ones (names starting with `.`), with details |
| `cat .*` | Prints the content of every hidden file in the current directory |
| `cat ./...Hiding-From-You` | Alternative: reads the hidden file directly by name |

## Approach
1. Connected with the password obtained from Level 2 → 3.
2. Ran `ls` and found the `inhere` directory, then moved into it with `cd inhere`.
3. Ran `ls` again, and the directory looked empty.
4. Ran `ls -la` and found a hidden file whose name starts with dots.
5. Used `cat .*` to read all hidden files at once, and the password appeared in the output.

## Challenges & Fixes
- **Problem 1: the directory looked empty.** Plain `ls` does not show names that start with a dot. **Fix:** use `ls -la` (or `ls -a`) to reveal hidden files.
- **Problem 2: messy output from `cat .*`.** The pattern `.*` also matches `.` and `..` (the current and parent directories), so `cat` prints "Is a directory" errors. **Fix:** ignore those errors, because the hidden file's content is still printed. Or read the file directly with `cat ./...Hiding-From-You`.
- **Other option:** use `cat ./` followed by the exact hidden filename once `ls -la` shows it.

## Key Takeaway
Files starting with `.` are hidden from plain `ls`. Always use `ls -la` when a directory looks empty, and remember that `.*` matches every hidden entry, including `.` and `..`.

## Result
✅ Password for Level 4 retrieved successfully. *(password not published)*
