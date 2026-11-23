# Files, Folders, Grep, Pipes, and Git Basics

**Name:** Juned Javed
**Focus:** Learning the core Linux commands for creating, editing, deleting, searching, and navigating files and folders, understanding which commands are dangerous, and making my first Git commit and push from the terminal

---

## 🎯 Objectives

- Learn how to create and remove folders and files from the terminal
- Learn how to edit text files with `nano`
- Learn how to read, copy, move, and delete files
- Understand the root directory (`/`) and why `rm -rf /` is dangerous
- Learn how to check my location and identity with `pwd` and `whoami`
- Learn how to list hidden files and read hidden content
- Learn text searching with `grep` and its flags
- Learn how to chain commands together using pipes `|`
- Clone a GitHub repository and make my first commit and push

---

## ✅ What I Accomplished

- Learned file creation and editing commands (`touch`, `nano`)
- Learned file reading and copying commands (`cat`, `cp`, `mv`)
- Learned file deletion commands (`rm`)
- Practiced creating folders with `mkdir`
- Removed files with `rm` and folders with `rm -rf`
- Used `pwd` and `whoami` to check my location and user
- Listed all files, including hidden ones, with `ls -la`
- Tried reading hidden file content with `cat .*`
- Studied why `rm -rf /` is one of the most dangerous commands in Linux
- Learned text searching with `grep` and all its flags
- Learned how to chain commands together using pipes `|`
- Cloned my GitHub repository to the Linux terminal for the first time
- Made my first Git commit and push from the terminal

---

## 💻 Commands Learned

| Command | What it does |
|---------|--------------|
| `touch filename` | Creates a new empty file |
| `mkdir foldername` | Makes a folder |
| `nano filename` | Opens a file in the terminal text editor to create and edit it |
| `cat filename` | Reads and displays file content |
| `cp file destination` | Copies a file to another location |
| `mv file destination` | Moves or renames a file |
| `rm filename` | Deletes a file permanently |
| `rm -rf foldername` | Removes a folder and its contents |
| `/` | Root directory |
| `rm -rf /` | **Dangerous:** deletes system files, never run it |
| `pwd` | Shows current location and full path |
| `whoami` | Shows the current user |
| `ls -la` | Lists everything, including hidden files, with details |
| `cat .*` | Shows content of hidden files in the current folder |
| `grep "word" file` | Searches for a word inside a file |
| `grep -i "word" file` | Searches ignoring uppercase/lowercase |
| `grep -n "word" file` | Shows line numbers of matches |
| `grep -c "word" file` | Counts how many lines match |
| `grep -r "word" folder` | Searches inside all files in a folder |
| `cat file \| grep "word"` | Pipe: feeds output into the next command |
| `cat file \| grep "word" \| wc -l` | Chains 3 commands together |
| `git clone <url>` | Downloads a GitHub repo to Linux |
| `git status` | Shows what files have changed |
| `git add .` | Stages all changes for commit |
| `git commit -m "message"` | Saves changes with a description |
| `git push` | Uploads commits to GitHub |

---

## 🧠 Key Concepts Learned

### Files and Folders
- **`mkdir`:** creates a new folder (directory).
- **`rm`:** removes a file, such as a text file.
- **`nano`:** a simple terminal text editor used to create and edit text files.
- **`rm -rf`:** removes a folder and everything inside it. `-r` means recursive (go through all contents) and `-f` means force (no confirmation prompts), so it should be used carefully.
- **`/` (root directory):** the top-level directory of the whole Linux file system. Every other file and folder lives under it.
- **`rm -rf /` (DANGER):** attempts to delete everything starting from the root directory, which means all system files. This can corrupt or destroy the system, so it must never be run.
- **`pwd`:** "print working directory." It shows where the user currently is and displays the full path of that position.
- **`whoami`:** shows which user is currently logged in.
- **`ls -la`:** lists everything in a folder in long format, including hidden files (names starting with `.`), with details like permissions and owners.
- **`cat .*`:** shows the content of the hidden files in the current folder.

### Searching and Chaining
- **grep** = Global Regular Expression Print. It searches text inside files.
- **Flags** = extra options added to commands using `-` like `-i`, `-n`, `-c`
- **Pipe `|`** = takes the output of one command and feeds it into the next
- **Chaining** = combining multiple commands to do powerful things in one line

### Git
- **git clone** = downloading an existing GitHub repo to your local Linux machine
- **Staging** = `git add` prepares files before committing, so you choose what to save
- **Commit** = a permanent snapshot of your work with a message describing what changed
- **Push** = sends your local commits to GitHub so the world can see them

---

## 💡 Big Insight

> *"grep + pipes is how real analysts work"*
> Instead of reading thousands of log lines manually,
> you filter, search, and count in seconds.
> This is Digital Forensics and SOC work in its simplest form.

---

## ❓ What Confused Me

- `cat file | grep "word"` and `grep "word" file` give the same result. The pipe feels redundant at first but becomes essential when chaining 3+ commands
- `git add .` vs `git add filename`: the dot means "everything", a specific name means just that file
- Cloning puts the repo in whatever folder you are currently in, so always `cd ~` first

---

## 🔧 Challenges & Fixes

- **Danger of `rm -rf`:** because `-f` skips confirmation, a wrong path can delete important data instantly. Fix: double-check the path before pressing Enter, and run `pwd` and `ls` first to confirm where I am.
- **`cat .*` gives messy output:** the pattern `.*` also matches `.` and `..` (the current and parent directories), so `cat` prints errors like "Is a directory". Fix: ignore those errors, or target a specific hidden file, for example `cat .filename`.
- **Hidden files not visible with `ls`:** plain `ls` skips names starting with a dot. Fix: use `ls -la` (or `ls -a`).

---

## ➡️ Next Steps

- Learn file permissions (`chmod`, `chown`)
- Understand what `rwx` means
- Learn why permissions matter in cybersecurity
- Practice `ls -la` to see hidden files and permissions
- Practice `ls -a`, `cd`, and `file`
- Practice `mkdir`, `nano`, and `rm` in a safe test folder
