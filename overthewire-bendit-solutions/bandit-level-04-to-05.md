# Bandit Level 4 → Level 5

## Objective
The password for the next level is stored in the only human-readable file in the `inhere` directory.

## Environment
- **Connection:** SSH
- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **User:** `bandit4`

## Commands Used
```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
ls
cd inhere
ls
cat -- *
# Alternative:
cat ./*
# Alternative (identify the readable file first):
file ./*
```

## Command Breakdown
| Command | Purpose |
|---|---|
| `ssh bandit4@... -p 2220` | Connects to the Bandit server as `bandit4` on port 2220 |
| `ls` | Lists files in the current directory (shows the `inhere` folder) |
| `cd inhere` | Moves into the `inhere` directory |
| `ls` | Shows the files inside, named like `-file00` to `-file09` |
| `cat -- *` | Reads all files at once; `--` marks the end of options so names starting with `-` are treated as filenames |
| `cat ./*` | Alternative: puts `./` in front of every filename so none are mistaken for options |
| `file ./*` | Alternative: shows the type of each file, so the one marked "ASCII text" is the human-readable one |

## Approach
1. Connected with the password obtained from Level 3 → 4.
2. Found the `inhere` directory in the home directory and moved into it with `cd inhere`.
3. Listed the files and saw several files whose names start with `-`.
4. Needed to find the one human-readable file, but reading the files one by one was slow and failed because of the dash in their names.
5. Researched and used `cat -- *`, which read all the files at once. `cat ./*` worked the same way.
6. Picked the human-readable text out of the output, which was the password for Level 5.

## Challenges & Fixes
- **Problem 1: files could not be read one by one.** There were many files, and typing each one was slow. **Fix:** use a wildcard (`*`) to read them all at once.
- **Problem 2: filenames start with `-`.** Linux treats `-file00` as an option, so `cat -file00` fails. **Fix:** use `cat -- *` (the `--` marks the end of options) or `cat ./*` (the `./` marks each name as a path).
- **Problem 3: most files are not human-readable.** Reading everything also prints unreadable data. **Fix:** find the readable text in the output, or run `file ./*` first to see which file is ASCII text and read only that one. If the terminal gets messed up by the unreadable output, run `reset`.

## Key Takeaway
When filenames start with `-`, use `./` or `--` so Linux does not read them as options. Wildcards like `*` save time when many files need to be checked, and the `file` command tells you what kind of data each file holds before you open it.

## Result
✅ Password for Level 5 retrieved successfully. *(password not published)*
