# Bandit Level 1 → Level 2

## Objective
The password for the next level is stored in a file called `-` located in the home directory.

## Environment
- **Connection:** SSH
- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **User:** `bandit1`

## Commands Used
```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
ls
cat ./-
```

## Command Breakdown
| Command | Purpose |
|---|---|
| `ssh bandit1@... -p 2220` | Connects to the Bandit server as `bandit1` on port 2220 |
| `ls` | Lists files in the home directory and shows the file named `-` |
| `cat ./-` | Prints the contents of the file `-` in the current directory |
| `./` | Refers to the current directory, so `-` is read as a filename, not a special symbol |

## Approach
1. Connected with the password obtained from Level 0 → 1.
2. Ran `ls` and found a file named `-`.
3. Tried `cat -`, which hung because `cat` treats `-` as "read from standard input."
4. Exited with `Ctrl+C` and used `cat ./-` to point to the file explicitly.

## Challenges & Fixes
- **Problem:** `cat -` waits forever for keyboard input.
- **Cause:** In most Unix tools a lone `-` means standard input, not a file named `-`.
- **Fix:** Prefix the name with `./` so it is unambiguously a file path.
- **Note:** `cat -- -` does not solve this, because `--` only stops option parsing and `-` is still treated as stdin.

## Key Takeaway
A filename made only of special characters can be misread by the tool. Using an explicit path like `./-` removes the ambiguity.

## Result
✅ Password for Level 2 retrieved successfully. *(password not published)*
