# Bandit Level 6 → Level 7

## Objective
The password for the next level is stored somewhere on the server. The file is owned by user `bandit7`, owned by group `bandit6`, and is exactly 33 bytes in size.

## Environment
- **Connection:** SSH
- **Host:** `bandit.labs.overthewire.org`
- **Port:** `2220`
- **User:** `bandit6`

## Commands Used
```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
ls
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
# Alternative (find and read in one step):
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null -exec cat {} +
```

## Command Breakdown
| Command | Purpose |
|---|---|
| `ssh bandit6@... -p 2220` | Connects to the Bandit server as `bandit6` on port 2220 |
| `find /` | Searches the entire filesystem, starting from the root directory |
| `-user bandit7` | Matches files owned by the user `bandit7` |
| `-group bandit6` | Matches files owned by the group `bandit6` |
| `-size 33c` | Matches files of exactly 33 bytes (`c` = bytes) |
| `2>/dev/null` | Redirects errors (stream 2) to `/dev/null`, hiding the "Permission denied" noise |
| `-exec cat {} +` | Runs `cat` on the matches; `{}` is replaced by the file paths and `+` passes many files to one `cat` call |
| `cat <path>` | Prints the contents of the file that `find` located |

## Approach
1. Connected with the password obtained from Level 5 → 6.
2. Read the clues: the file is not in a specific folder, so it could be anywhere on the server.
3. Combined every clue (owner, group, size) into a single `find` search starting from `/`.
4. The output was flooded with "Permission denied" errors because a normal user cannot read most system directories.
5. Added `2>/dev/null` to discard the errors, leaving only the one real match.
6. Read the file with `cat` (or used `-exec cat {} +` to do it in one step) and got the password for Level 7.

## Challenges & Fixes
- **Problem 1: the search was too broad.** The password could be anywhere on the server. **Fix:** stack multiple `find` filters (`-user`, `-group`, `-size`) so only one file matches.
- **Problem 2: too much error output.** `find /` prints "Permission denied" for every folder the user cannot enter. **Fix:** redirect stderr with `2>/dev/null`.
- **Problem 3: first version of the command had syntax errors.** I wrote `find -user ...` with no starting path, so it only searched the current directory, and I typed `2</dev/null`. **Fix:** start the search at `/`, and use `2>` (output redirection), not `2<`.
- **Problem 4: reading the file as a separate step.** **Fix:** `-exec cat {} +` runs `cat` on the matches directly. The `+` ending is more efficient than `\;` because it batches files into one command.

## Key Takeaway
`find` can filter by owner (`-user`), group (`-group`), size (`-size`), type and permissions all at once, so even a file hidden somewhere on a huge filesystem can be located quickly. Combining it with `2>/dev/null` keeps the output clean, and `-exec cat {} +` lets you search and read in a single command. This builds on Level 5 → 6, where `find` with `-type f`, `-size` and `! -executable` did the same job inside one directory.

## Result
✅ Password for Level 7 retrieved successfully. *(password not published)*
