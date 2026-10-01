# Day 3 — Linux Basics: Files, Folders, and Navigation Commands

**Date:** [fill in date]
**Focus:** Learning the core Linux commands for creating, editing, deleting, and navigating files and folders, and understanding which commands are dangerous

## Objectives
- Learn how to create and remove folders and files from the terminal
- Learn how to edit text files with `nano`
- Understand the root directory (`/`) and why `rm -rf /` is dangerous
- Learn how to check my location and identity with `pwd` and `whoami`
- Learn how to list hidden files and read hidden content

## What I Did
- Practiced creating folders with `mkdir`
- Created and edited text files with `nano`
- Removed files with `rm` and folders with `rm -rf`
- Used `pwd` and `whoami` to check my location and user
- Listed all files, including hidden ones, with `ls -la`
- Tried reading hidden file content with `cat .*`
- Studied why `rm -rf /` is one of the most dangerous commands in Linux

## Key Concepts Learned
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

## Commands Summary

| Command | Purpose |
|---|---|
| `mkdir` | Make a folder |
| `rm` | Remove a file |
| `nano` | Create and edit a text file |
| `rm -rf` | Remove a folder and its contents |
| `/` | Root directory |
| `rm -rf /` | Dangerous: deletes system files, never run it |
| `pwd` | Show current location and path |
| `whoami` | Show current user |
| `ls -la` | List everything, including hidden files |
| `cat .*` | Show content of hidden files in the current folder |

## Challenges & Fixes
- **Danger of `rm -rf`:** because `-f` skips confirmation, a wrong path can delete important data instantly. Fix: double-check the path before pressing Enter, and run `pwd` and `ls` first to confirm where I am.
- **`cat .*` gives messy output:** the pattern `.*` also matches `.` and `..` (the current and parent directories), so `cat` prints errors like "Is a directory". Fix: ignore those errors, or target a specific hidden file, for example `cat .filename`.
- **Hidden files not visible with `ls`:** plain `ls` skips names starting with a dot. Fix: use `ls -la` (or `ls -a`).

## Next Steps
- Bandit Level 3 → 4 (hidden files and directories)
- Practice `ls -a`, `cd`, and `file`
- Practice `mkdir`, `nano`, and `rm` in a safe test folder
- Keep documenting each level with commands, errors, and fixes
