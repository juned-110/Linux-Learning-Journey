# Day 06 — Linux Command Revision, Special Filenames, and File Management

**Date:** [6th October] **Focus:** Revising Linux navigation, files, folders, permissions, ownership, and user management while practicing special filenames, `rm` options, and safe file/folder creation

## Objectives

- Revise basic Linux navigation and file-management commands
- Practice creating, reading, editing, and removing files and folders
- Understand the difference between `rm -r`, `rm -f`, and `rm -rf`
- Practice working with filenames containing spaces and leading `-`
- Understand how `--` and `./` prevent filenames from being treated as options
- Revise `chmod`, `chown`, users, groups, and ownership
- Practice creating files and directories with unusual names
- Continue preparing for OverTheWire Bandit and cybersecurity command-line work

## What I Did

- Revised `ls`, `cd`, `pwd`, `whoami`, `cat`, `mkdir`, `rm`, `nano`, and `touch`
- Revised `ls -la`, `cat .*`, and `cat ./ *`
- Practiced creating files with spaces and special characters in their names
- Created a file named `--spaces in this filename--`
- Added text to the file using `echo`
- Read the file using `cat`
- Created a directory with the same special name
- Revised how to open a file named `-`
- Practiced using `--` to stop Linux from treating a filename as an option
- Practiced using `./` to specify a filename as a path
- Reviewed why quotes are required when filenames contain spaces
- Revised `rm -r`, `rm -f`, and `rm -rf`
- Revised `chmod` permissions and numeric permission values
- Revised `chown`, users, groups, and ownership
- Revised `adduser`, `su`, `sudo -u`, `deluser`, and `delgroup`
- Practiced thinking about command behavior before executing potentially dangerous commands

## Key Concepts Learned

- **`rm -r`:** Removes directories/folders and their contents recursively.
- **`rm -f`:** Force removes files without asking for confirmation. It does not remove directories by itself.
- **`rm -rf`:** Combines recursive and force options, allowing directories and their contents to be removed without confirmation. It is dangerous if used on the wrong path.
- **`r` = recursive:** Allows `rm` to work with directories and their contents.
- **`f` = force:** Tells `rm` to remove without confirmation and ignore some errors such as missing files.
- **Quotes `" "`:** Keep spaces together as part of one filename.
- **`--`:** Tells a command to stop processing options, so the following text is treated as a filename or argument.
- **`./`:** Specifies that the name is a path in the current directory, preventing a filename beginning with `-` from being interpreted as an option.
- **Special filenames:** A filename beginning with `-` can be interpreted as a command option, while spaces can cause the shell to split one filename into multiple arguments.
- **Creating a file with spaces:** `touch "--spaces in this filename--"`
- **Adding text to a file:** `echo "Hello Linux" > "--spaces in this filename--"`
- **Reading a special filename:** `cat -- "--spaces in this filename--"`
- **Creating a directory with spaces and leading dashes:** `mkdir -- "--spaces in this filename--"`
- **File permissions:** `r` = read (4), `w` = write (2), and `x` = execute (1).
- **Permission classes:** `User`, `Group`, and `Others`.
- **`chmod`:** Changes file or directory permissions.
- **`chown`:** Changes the owner and/or group of a file or directory.
- **`whoami`:** Shows the current user.
- **`id`:** Shows the current user's UID, GID, and groups.
- **`adduser`:** Creates a new user.
- **`su - user`:** Switches to another user's login session.
- **`sudo -u user command`:** Runs a specific command as another user.
- **`deluser`:** Deletes a user account.
- **`delgroup`:** Deletes a group.
- **`ls /home`:** Shows the home directories of users.
- **Linux is case-sensitive:** `juned`, `Juned`, and `junedjaved` can be different names.
- **Command safety:** Before using a command, especially a command containing `sudo`, `rm`, `-r`, or `-f`, I should understand exactly what it will affect.

## Commands Summary

| **Command** | **Purpose** |
| ------------------------------------------ | -------------------------------------------------------------------------- |
| `ls` | List files and directories |
| `cd folder` | Enter a directory |
| `cd ..` | Move to the parent directory |
| `cd ~` | Go to the home directory |
| `pwd` | Show the current directory/path |
| `whoami` | Show the current user |
| `cat file` | Display the contents of a text file |
| `mkdir folder` | Create a directory |
| `nano file` | Create or edit a text file |
| `touch file` | Create an empty file or update its timestamp |
| `rm file` | Remove a file |
| `rm -r folder` | Remove a directory and its contents recursively |
| `rm -f file` | Force remove a file |
| `rm -rf folder` | Force and recursively remove a directory and its contents |
| `ls -la` | List files including hidden files with detailed information |
| `cat .*` | Attempt to display hidden files |
| `cat ./ *` | Attempt to read files in the current directory |
| `touch "--spaces in this filename--"` | Create a file with spaces and leading dashes |
| `echo "Hello Linux" > "--spaces in this filename--"` | Create/write text to the special filename |
| `cat -- "--spaces in this filename--"` | Read a filename with spaces and leading dashes |
| `cat "./--spaces in this filename--"` | Read the special filename using a path |
| `mkdir -- "--spaces in this filename--"` | Create a directory with spaces and leading dashes |
| `chmod 600 file` | Give the owner read/write permissions only |
| `chmod 700 file` | Give the owner read/write/execute permissions only |
| `chown user file` | Change the owner |
| `chown user:group file` | Change owner and group |
| `sudo adduser name` | Create a new user |
| `su - user` | Switch to another user |
| `sudo -u user command` | Run a command as another user |
| `sudo deluser name` | Delete a user account |
| `sudo deluser --remove-home name` | Delete the account and its home directory |
| `sudo deluser --remove-all-files name` | Delete the account and files owned by the user |
| `getent passwd name` | Check whether a user exists |
| `getent group name` | Check whether a group exists |
| `groups username` | Show the groups of a user |
| `sudo delgroup name` | Delete a group |

## Challenges & Fixes

- **Filename starts with `-`:** Linux may interpret it as a command option. Fix: use `--` or `./` before the filename.
- **Filename contains spaces:** The shell separates words at spaces. Fix: use quotes or escape each space with `\`.
- **`cat -- --spaces in this filename--` fails:** `--` solves the leading dash problem, but the shell still splits the filename at spaces. Fix: use quotes.
- **`cat "--spaces in this filename--"` fails:** Quotes solve the spaces problem, but the filename still begins with `-`. Fix: use `--` or `./`.
- **Correct solution:** `cat -- "--spaces in this filename--"` or `cat "./--spaces in this filename--"`.
- **Deleting directories with normal `rm`:** `rm` does not remove directories by itself. Fix: use `rm -r` when intentionally removing a directory.
- **Using `rm -rf`:** It can remove a directory and everything inside it without confirmation. Fix: always check the path before running it.
- **Permission errors:** A user may not have permission to modify a file. Fix: check ownership and permissions using `ls -l`, and use `sudo` only when necessary.
- **User and group names:** Linux is case-sensitive and requires the exact login/group name.

## Revision Practice

- Create a file called `test.txt`.
- Add some text using `nano`.
- Read the file using `cat`.
- Check its permissions using `ls -l`.
- Change its permissions using `chmod`.
- Create a directory called `practice`.
- Create a file inside it.
- Practice entering and leaving the directory using `cd` and `cd ..`.
- Create a filename containing spaces.
- Create a filename beginning with `-`.
- Practice reading the unusual filename using `--` and `./`.
- Review the difference between `rm`, `rm -r`, `rm -f`, and `rm -rf`.
- Review the difference between `chmod` and `chown`.
- Review the difference between `su - user` and `sudo -u user command`.

## Next Steps

- Continue with OverTheWire Bandit
- Practice finding files by owner, group, and size
- Practice `chmod` and `chown` again in a safe test folder
- Practice special filenames without looking at my notes
- Continue documenting commands, errors, solutions, and lessons learned
- Learn more Linux commands needed for cybersecurity and DevSecOps
