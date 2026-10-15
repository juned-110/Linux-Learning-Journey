# Bandit Level 5 → Level 6

## Objective
The password for the next level is stored in a file somewhere under the `inhere` directory. The file is human-readable, exactly 1033 bytes in size, and not executable.

## Environment
- **Connection:** SSH
- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **User:** `bandit5`

## Commands Used
```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
ls
cd inhere
ls
find . -type f -size 1033c ! -executable
cat ./maybehere07/.file2
# Alternative (find and read in one step):
find . -type f -size 1033c ! -executable -exec cat {} \;
```

## Command Breakdown
| Command | Purpose |
|---|---|
| `ssh bandit5@... -p 2220` | Connects to the Bandit server as `bandit5` on port 2220 |
| `ls` | Lists files in the current directory (shows the `inhere` folder) |
| `cd inhere` | Moves into the `inhere` directory |
| `find .` | Searches the current directory and all subdirectories |
| `-type f` | Matches regular files only, not directories |
| `-size 1033c` | Matches files of exactly 1033 bytes (`c` = bytes) |
| `! -executable` | `!` means NOT, so this excludes executable files |
| `-exec cat {} \;` | Runs `cat` on every match; `{}` is replaced by each file path and `\;` ends the command |
| `cat <path>` | Prints the contents of the file that `find` located |

## Approach
1. Connected with the password obtained from Level 4 → 5.
2. Moved into `inhere` and listed it. It contained many `maybehere` directories, each holding files.
3. Tried `cat *`, `cat ./*` and `cat -- *`, which failed because the targets were directories, not readable files (and some files are hidden).
4. Realised the file had to be found by its properties instead: file type, exact size, and not executable.
5. Used `find . -type f -size 1033c ! -executable` to narrow every file down to the one that matched.
6. Read that file with `cat` and got the password for Level 6.

## Challenges & Fixes
- **Problem 1: `cat` flags did not work.** `cat *` and `cat ./*` only see the top level, where there are only directories, and they skip hidden files. **Fix:** use `find`, which searches recursively and includes hidden files.
- **Problem 2: too many files to check by hand.** **Fix:** filter by the clues given: `-type f`, `-size 1033c`, `! -executable`.
- **Problem 3: first version of the command had syntax errors.** I wrote `! executable` and `exec`. **Fix:** `find` tests and actions need a leading dash (`-executable`, `-exec`), and `-exec` must end with `\;` or `+`.

## Key Takeaway
When files are spread across many folders, do not open them by hand. Use `find` and describe the file by its properties (type, size, permissions, owner). Searching first and reading second is faster, safer, and a core skill for finding files during security work.

## Result
✅ Password for Level 6 retrieved successfully. *(password not published)*
