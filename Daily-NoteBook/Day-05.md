# Day 05 — Linux Permissions, Ownership, and User Management

**Date:** [5th October]
**Focus:** Understanding how Linux decides who can read, write, and run a file (`chmod`, `chown`), and how to add, switch to, and completely remove a user

## Objectives
- Understand file permissions and change them with `chmod` (symbolic and numeric modes)
- Understand file ownership (owner and group) and change it with `chown`
- Learn how Linux decides which permissions apply to me
- Create a practice user with `adduser`, switch to that user, and delete it completely
- Learn to read and fix common permission and ownership errors

## What I Did
- Learned `chmod` and tested myself with a 7-question quiz
- Read file owner and group from the 3rd and 4th columns of `ls -l`
- Checked my identity with `whoami` and `id`
- Created a practice user with `sudo adduser`
- Changed the owner and group of a test file with `sudo chown`
- Set permissions to `600` and tested who could still read the file
- Hit three errors (`invalid user`, `Operation not permitted`, `missing operand`) and fixed each one
- Studied how to act as another user with `sudo -u` and `su -`
- Studied how to delete a user completely and verify that nothing is left

## Key Concepts Learned
- **Owner, group, others:** every file has one owner, one group, and everyone else is "others". `chmod` decides *what* each of them can do, and `chown` decides *who* the owner and group are.
- **Permission bits:** `r` = read (4), `w` = write (2), `x` = execute (1). Add them per class, so `754` = owner `rwx`, group `r-x`, others `r--`.
- **`chmod` symbolic mode:** `u+x` adds execute for the owner, `go-w` removes write from group and others, and `a=r` sets everyone to read only (`=` replaces what was there).
- **`600` vs `400`:** `600` is owner read and write, nobody else gets anything. `400` is owner read only.
- **Directory `x` bit:** on a folder, `x` means "allowed to enter it". Without `x` I cannot `cd` into the folder even if I have `r` and `w`.
- **`chown`:** changes the owner and/or group. Forms: `chown user file`, `chown user:group file`, `chown :group file`, and `-R` for a folder and everything inside it.
- **Who can run `chown`:** a normal user cannot give a file away, so `sudo` is needed. Only the owner (or root) can run `chmod` on a file.
- **How Linux checks permissions:** it asks "am I the owner?", then "am I in the group?", then "I'm others". The **first match wins** and only that class's permissions apply. So an owner `rw-`, group `---` file (`600`) cannot be read by someone who is in the group.
- **root ignores permissions:** `sudo cat file` works even on a `600` file owned by someone else.
- **Names vs numbers:** Linux stores owners as numbers (UID and GID), and names are labels. If a user is deleted, files they owned show a bare number, which is why I give files back **before** deleting a user.
- **Linux is case-sensitive:** `juned`, `Juned`, and `junedjaved` are three different names. `chown` needs the exact **login name**, not the full name.
- **`adduser` details:** only the username and password matter. Full name, room number, and phone are optional (press Enter to skip), and no real personal details should go in practice users.
- **Deleting a user:** `deluser` removes only the account, `--remove-home` also removes the home folder, and `--remove-all-files` also removes every file the user owns on the system.
- **Traces remain:** shell history and system logs may still show that a user was created. Logs are evidence and must never be edited.

## Commands Summary

| Command | Purpose |
|---|---|
| `chmod 754 file` | Set permissions with numbers (owner, group, others) |
| `chmod u+x file` | Add execute for the owner only |
| `chmod go-w file` | Remove write from group and others |
| `chmod a=r file` | Set everyone to read only |
| `ls -l file` | Show permissions, owner, and group |
| `ls -ld folder` | Show permissions of the folder itself |
| `whoami` | Show current user |
| `id` / `id username` | Show UID, GID, and groups (also checks if a user exists) |
| `sudo adduser name` | Create a new user |
| `sudo chown user file` | Change the owner |
| `sudo chown user:group file` | Change owner and group together |
| `sudo chown -R user:group folder` | Change ownership of a folder and its contents |
| `chgrp group file` | Change only the group |
| `sudo -u user command` | Run one command as another user |
| `su - user` | Switch into another user's session (`exit` to return) |
| `sudo deluser name` | Delete the account, keep the home folder |
| `sudo deluser --remove-home name` | Delete the account and home folder |
| `sudo deluser --remove-all-files name` | Delete the account and all files owned by the user |
| `getent passwd name` / `getent group name` | Check that the user or group is really gone |
| `sudo delgroup name` | Remove a leftover group |

## Challenges & Fixes
- **`chown: invalid user: 'juned'`:** the user did not exist, then I used the wrong name. Fix: check with `id username`, and use the exact login name (Linux is case-sensitive).
- **`chown: changing ownership ... Operation not permitted`:** a normal user cannot give a file away. Fix: use `sudo chown ...`.
- **`chmod: changing permissions ... Operation not permitted`:** after giving the file away I was no longer the owner. Fix: use `sudo chmod ...`, or act as the owner with `sudo -u` or `su -`.
- **`chmod: missing operand`:** I typed `sudo chmod text` without a mode. Fix: `chmod` always needs a mode and then a file, for example `sudo chmod 640 text`.
- **Could not read a `600` file after giving it away:** I was in the group class, and the group digit was `0`. Fix: understand the owner → group → others check, or use a mode like `640`.
- **Another user cannot reach my file:** they need `x` on every folder on the way, including my home folder. Fix: `chmod o+x ~` temporarily, then `chmod o-x ~` to restore it.
- **Deleting a user leaves orphan files:** files show a bare number as owner. Fix: `chown` them back to myself first, before deleting the user.
- **Personal details in `adduser`:** the optional fields can hold personal data. Fix: press Enter to skip them, and redact any such details before pasting terminal output into a public repo.

## Next Steps
- Bandit Level 6 → 7 (find files by owner, group, and size)
- Practice `chmod` and `chown` again in a safe test folder, without looking at my notes
- Re-explain chmod vs chown in my own words (self-check)
- Keep documenting each level with commands, errors, and fixes
