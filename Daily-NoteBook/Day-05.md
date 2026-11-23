# Processes, System Info, Permissions, Ownership, and User Management

**Name:** Juned Javed
**Focus:** Understanding how Linux manages processes, reading system information and logs, understanding SSH, and learning how Linux decides who can read, write, and run a file (`chmod`, `chown`), including how to add, switch to, and completely remove a user

---

## 🎯 Objectives

- Understand what a process is and how Linux manages processes
- View and stop processes with `ps`, `top`, and `kill`
- Check system information with `df -h`, `free -h`, `uname -a`, and `uptime`
- Understand syslog, SSH, and Swap memory
- Understand file permissions and change them with `chmod` (symbolic and numeric modes)
- Understand file ownership (owner and group) and change it with `chown`
- Learn how Linux decides which permissions apply to me
- Create a practice user with `adduser`, switch to that user, and delete it completely
- Learn to read and fix common permission and ownership errors

---

## ✅ What I Accomplished

- Learned what a process is and how Linux manages them
- Learned to view processes using `ps`, `ps aux`, and `top`
- Learned to kill processes using the `kill` command
- Learned system information commands `df -h`, `free -h`, `uname -a`, `uptime`
- Understood what syslog is and its role in cybersecurity
- Understood what SSH is and why it matters in security
- Understood what Swap memory is
- Read and interpreted all command outputs independently without help
- Connected process management concepts to real cybersecurity scenarios
- Learned `chmod` and tested myself with a 7-question quiz
- Read file owner and group from the 3rd and 4th columns of `ls -l`
- Checked my identity with `whoami` and `id`
- Listed folder contents with permissions using `ls -la` and `ls -ls`
- Listed all user home folders with `ls /home`
- Created a practice user with `sudo adduser`
- Changed the owner and group of a test file with `sudo chown`
- Set permissions to `600` and tested who could still read the file
- Hit three errors (`invalid user`, `Operation not permitted`, `missing operand`) and fixed each one
- Studied how to act as another user with `sudo -u` and `su -`
- Studied how to delete a user completely and verify that nothing is left
- Checked a user's groups with `groups username` and deleted a user's home folder with `sudo rm -r`

---

## 💻 Commands Learned

### Processes and System Information

| Command | What it does |
|---------|--------------|
| `ps` | Shows only YOUR running processes |
| `ps aux` | Shows ALL processes on the entire system |
| `top` | Live real-time process monitor, like Task Manager |
| `kill PID` | Stops a process using its ID number |
| `sleep 100 &` | Starts a dummy process in the background for testing |
| `ps aux \| grep name` | Searches for a specific process by name |
| `df -h` | Shows disk storage space in human readable format |
| `free -h` | Shows RAM and Swap usage in human readable format |
| `uname -a` | Shows complete system and kernel information |
| `uptime` | Shows how long the system has been running, and the load |

### Permissions, Ownership, and Users

| Command | What it does |
|---------|--------------|
| `chmod 754 file` | Sets permissions with numbers (owner, group, others) |
| `chmod u+x file` | Adds execute for the owner only |
| `chmod go-w file` | Removes write from group and others |
| `chmod a=r file` | Sets everyone to read only |
| `ls -l file` | Shows permissions, owner, and group |
| `ls -ld folder` | Shows permissions of the folder itself |
| `ls -la folder` | Shows permissions of all files inside the folder, including hidden files |
| `ls -ls folder` | Shows permissions of the files inside the folder, with file sizes in blocks |
| `ls /home` | Lists the home folders of all users |
| `whoami` | Shows the current user |
| `id` / `id username` | Shows UID, GID, and groups (also checks if a user exists) |
| `groups username` | Shows which groups a user belongs to |
| `sudo adduser name` | Creates a new user |
| `sudo chown user file` | Changes the owner |
| `sudo chown user:group file` | Changes owner and group together |
| `sudo chown -R user:group folder` | Changes ownership of a folder and its contents |
| `chgrp group file` | Changes only the group |
| `sudo -u user command` | Runs one command as another user |
| `su - user` | Switches into another user's session (`exit` to return) |
| `sudo deluser name` | Deletes the account, keeps the home folder |
| `sudo deluser --remove-home name` | Deletes the account and home folder |
| `sudo deluser --remove-all-files name` | Deletes the account and all files owned by the user |
| `sudo rm -r /home/username` | Manually deletes a user's home folder (double-check the path first) |
| `getent passwd name` / `getent group name` | Checks that the user or group is really gone (or exists) |
| `sudo delgroup name` | Removes a leftover group |

---

## 🧠 Key Concepts Learned

### Processes and System Information
- **Process** = every program running on Linux is a process with a unique PID
- **PID** = Process ID, a unique number assigned to every running process
- **ps aux columns** = USER (owner), PID (ID), %CPU (processor), %MEM (memory), COMMAND (program name)
- **root processes** = system processes owned by admin. Linux itself runs these
- **`<username>` processes** = YOUR processes, the things you started
- **`&`** = run a process in the background so the terminal stays free
- **Swap** = emergency fake RAM created from hard drive space when real RAM is full
- **syslog** = Linux system logger. It records every event, login, and error on the system
- **SSH** = Secure Shell. It lets you remotely control another computer securely through the terminal
- **Load average** = 3 numbers showing system stress over the last 1, 5, and 15 minutes
- **0.00 load average** = system completely relaxed and healthy

### Permissions and Ownership
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

### User Management
- **`adduser` details:** only the username and password matter. Full name, room number, and phone are optional (press Enter to skip), and no real personal details should go in practice users.
- **Deleting a user:** `deluser` removes only the account, `--remove-home` also removes the home folder, and `--remove-all-files` also removes every file the user owns on the system.
- **Viewing folders with `ls`:** `ls -la folder` shows permissions of everything inside the folder, including hidden files (names starting with `.`). `ls -ls folder` also shows a long listing with permissions, but skips hidden files and adds the file size in blocks as the first column.
- **User home folders:** every normal user has a home folder inside `/home`, so `ls /home` lists all the users who have one.
- **Checking users and groups:** `groups username` shows which groups a user belongs to, and `getent group name` confirms whether a group exists.
- **Manual home folder removal:** `sudo rm -r /home/username` deletes a user's home folder and everything inside it. It cannot be undone, so I must double-check the path before running it.
- **Traces remain:** shell history and system logs may still show that a user was created. Logs are evidence and must never be edited.

---

## 📊 Reading ps aux Output

| USER | PID | COMMAND | Meaning |
|------|-----|---------|---------|
| root | 1 | systemd | Linux boss process, the first to start |
| root | 113 | cron | Automatic task scheduler |
| syslog | 170 | rsyslogd | System logger, records all events |
| `<username>` | 914 | bash | MY terminal session |
| `<username>` | 1003 | ps aux | Command I just ran |

**How to identify:**
- USER = root → Linux system process
- USER = `<username>` → MY process
- COMMAND = bash → my terminal
- COMMAND = what I typed → current running command

---

## 🔍 Special Processes Explained

| Process | Owner | Purpose |
|---------|-------|---------|
| systemd | root | PID 1, boss of all processes |
| cron | root | Runs automatic scheduled tasks |
| rsyslogd | syslog | Records all system events to logs |
| chronyd | _chrony | Keeps the system clock accurate |
| dbus-daemon | message+ | Internal Linux process communication |
| bash | `<username>` | My terminal session |

---

## 🔐 Cybersecurity Connections

### Finding Malware with ps aux
```bash
ps aux | grep -i suspicious
```
- Malware appears as unknown processes
- A suspicious process running as root = serious red flag
- High CPU from an unknown process = possible cryptominer

### SSH Security
- SSH allows remote terminal access to servers
- Hackers attempt brute force attacks on SSH
- Failed SSH attempts are recorded in `/var/log/auth.log`
- Strong passwords and SSH keys prevent unauthorized access

### Syslog Forensics
```bash
cat /var/log/auth.log | grep "Failed"
```
Multiple failed logins from the same IP = brute force attack detected!

### Memory Exhaustion Attack
- Attackers fill RAM intentionally to crash systems
- `free -h` helps monitor RAM consumption
- Heavy swap usage = system struggling = possible attack

### Disk Space Attack
- Attackers fill disk space to crash services
- `df -h` helps monitor disk usage

---

## 💡 Big Insight

> *"ps aux is the security analyst's first weapon"*
> When a system is compromised the first thing an analyst runs is ps aux.
> Every malware, every backdoor, every suspicious script shows up here.
> Learning to read process output is learning to investigate attacks.
> This is real SOC analyst and Digital Forensics work!

---

## ❓ Interview Questions I Can Now Answer

**Q: What is a process in Linux?**
A: A process is any program currently running on the system. Every process has a unique PID assigned by the kernel. Linux manages all processes through systemd which is always PID 1.

**Q: How would you find a suspicious process on a Linux system?**
A: I would run `ps aux` to list all running processes and look for unknown process names, processes consuming unusual CPU or memory, or unexpected processes running as root. I would then use `grep` to filter specific names and `kill` to terminate suspicious processes.

**Q: What is the difference between ps and ps aux?**
A: `ps` shows only processes belonging to the current user in the current terminal. `ps aux` shows ALL processes running on the entire system from all users, including system processes owned by root.

**Q: What is Swap memory?**
A: Swap is hard drive space that Linux uses as emergency RAM when physical memory is full. It is slower than real RAM because hard drives are slower than memory chips. Heavy swap usage indicates the system needs more RAM.

**Q: What is SSH and why is it important in security?**
A: SSH (Secure Shell) is a protocol that allows secure encrypted remote access to Linux systems through the terminal. It is important because it is a common attack target. Hackers attempt brute force attacks against SSH to gain unauthorized access to servers. Failed SSH attempts are logged in `/var/log/auth.log`.

**Q: What is syslog?**
A: Syslog is the Linux system logging service that records all system events, including logins, errors, and sudo commands. It stores logs in `/var/log/`. Security analysts use syslog for incident investigation and forensic analysis.

---

## 🔧 Challenges & Fixes

- **`chown: invalid user: 'juned'`:** the user did not exist, then I used the wrong name. Fix: check with `id username`, and use the exact login name (Linux is case-sensitive).
- **`chown: changing ownership ... Operation not permitted`:** a normal user cannot give a file away. Fix: use `sudo chown ...`.
- **`chmod: changing permissions ... Operation not permitted`:** after giving the file away I was no longer the owner. Fix: use `sudo chmod ...`, or act as the owner with `sudo -u` or `su -`.
- **`chmod: missing operand`:** I typed `sudo chmod text` without a mode. Fix: `chmod` always needs a mode and then a file, for example `sudo chmod 640 text`.
- **Could not read a `600` file after giving it away:** I was in the group class, and the group digit was `0`. Fix: understand the owner → group → others check, or use a mode like `640`.
- **Another user cannot reach my file:** they need `x` on every folder on the way, including my home folder. Fix: `chmod o+x ~` temporarily, then `chmod o-x ~` to restore it.
- **Deleting a user leaves orphan files:** files show a bare number as owner. Fix: `chown` them back to myself first, before deleting the user.
- **Home folder left behind after `deluser`:** the account is gone but `/home/username` still exists. Fix: use `--remove-home` next time, or delete it manually with `sudo rm -r /home/username` after confirming the exact path with `ls /home`.
- **Personal details in `adduser`:** the optional fields can hold personal data. Fix: press Enter to skip them, and redact any such details before pasting terminal output into a public repo.

---

## ➡️ Next Steps

- Learn SSH in detail
- Connect to a remote server via SSH
- Understand SSH keys and why `chmod 600` matters for them
- Learn basic firewall concepts with `ufw`
- Practice `chmod` and `chown` again in a safe test folder, without looking at my notes
- Re-explain chmod vs chown in my own words (self-check)
