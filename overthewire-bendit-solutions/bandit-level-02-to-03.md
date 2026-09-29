# Bandit Level 2 → Level 3

## Objective
The password for the next level is stored in a file called `--spaces in this filename--` located in the home directory.

## Environment
- **Connection:** SSH
- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **User:** `bandit2`

## Commands Used
```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
ls
cat -- "--spaces in this filename--"
# Alternative:
cat "./--spaces in this filename--"
```

## Command Breakdown
| Command | Purpose |
|---|---|
| `ssh bandit2@... -p 2220` | Connects to the Bandit server as `bandit2` on port 2220 |
| `ls` | Lists files in the home directory |
| `"..."` (quotes) | Keeps the whole filename together as a single argument |
| `--` | Tells `cat` that options end here and everything after is a filename |
| `./` | Alternative fix: the path starts with `.` so it can't look like an option |
| `cat` | Prints the file's contents to the terminal |

## Approach
1. Connected with the password obtained from Level 1 → 2.
2. Ran `ls` and found the file `--spaces in this filename--`.
3. Tried `cat --spaces in this filename--`, which failed.
4. Fixed the two problems separately: quoted the name for the spaces, and used `--` (or `./`) for the leading dashes.

## Challenges & Fixes
- **Problem 1: spaces.** The shell split the name into four arguments (`--spaces`, `in`, `this`, `filename--`) before `cat` ever ran. **Fix:** wrap the name in quotes.
- **Problem 2: leading dashes.** Even when quoted, the name starts with `--`, so `cat` read it as an option and reported an invalid option. **Fix:** use `--` before the filename, or prefix the name with `./`.
- **Other option:** escaping each space with a backslash also works: `cat ./--spaces\ in\ this\ filename--`.

## Key Takeaway
Two separate problems were stacked on each other, and each needed its own fix. Always quote filenames with spaces, and use `--` or `./` for names that begin with a dash.

## Result
✅ Password for Level 3 retrieved successfully. *(password not published)*
