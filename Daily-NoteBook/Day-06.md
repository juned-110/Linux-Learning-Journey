# SSH, Command Revision, Special Filenames, and File Management

**Name:** Juned Javed
**Focus:** Understanding SSH and secure remote access, generating and protecting SSH keys, and revising Linux navigation, files, folders, permissions, ownership, and user management while practicing special filenames, `rm` options, and safe file/folder creation

---

## 🎯 Objectives

- Understand what SSH is and the problem it solves
- Install and start the OpenSSH server and make a first SSH connection
- Understand password vs key authentication and generate an ED25519 key pair
- Read SSH logs and understand SSH hardening
- Revise basic Linux navigation and file-management commands
- Practice creating, reading, editing, and removing files and folders
- Understand the difference between `rm -r`, `rm -f`, and `rm -rf`
- Practice working with filenames containing spaces and leading `-`
- Understand how `--` and `./` prevent filenames from being treated as options
- Revise `chmod`, `chown`, users, groups, and ownership
- Practice creating files and directories with unusual names
- Continue preparing for cybersecurity command-line work

---

## ✅ What I Accomplished

- Understood what SSH is and the problem it solves
- Installed and started the OpenSSH server
- Made my first SSH connection to localhost
- Understood SSH port 22 and why admins change it
- Learned the difference between password and key authentication
- Generated an ED25519 SSH key pair
- Understood the private vs public key concept
- Read SSH logs like a forensics analyst
- Explored the SSH config file and security settings
- Understood SSH hardening for real servers
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

---

## 💻 Commands Learned

### SSH

| Command | What it does |
|---------|--------------|
| `ssh -V` | Checks the SSH version installed |
| `sudo apt install openssh-server -y` | Installs the SSH server |
| `sudo service ssh start` | Starts the SSH server |
| `sudo service ssh stop` | Stops the SSH server |
| `sudo service ssh status` | Checks if SSH is running |
| `ssh username@ip-address` | Connects to a remote server |
| `ssh username@localhost` | Connects to your own machine |
| `ssh username@ip -p 2220` | Connects on a specific port |
| `ssh-keygen -t ed25519 -C label` | Generates an SSH key pair |
| `cat ~/.ssh/id_ed25519.pub` | Views your public key |
| `ls -la ~/.ssh/` | Views SSH files and permissions |
| `sudo cat /etc/ssh/sshd_config` | Views the SSH server config |
| `sudo cat /var/log/auth.log \| grep ssh` | Views SSH login logs |
| `exit` | Disconnects from an SSH session |
| `hostname` | Shows the computer name |

### Files, Folders, and Special Filenames

| Command | What it does |
|---------|--------------|
| `ls` | Lists files and directories |
| `cd folder` | Enters a directory |
| `cd ..` | Moves to the parent directory |
| `cd ~` | Goes to the home directory |
| `pwd` | Shows the current directory/path |
| `whoami` | Shows the current user |
| `cat file` | Displays the contents of a text file |
| `mkdir folder` | Creates a directory |
| `nano file` | Creates or edits a text file |
| `touch file` | Creates an empty file or updates its timestamp |
| `rm file` | Removes a file |
| `rm -r folder` | Removes a directory and its contents recursively |
| `rm -f file` | Force removes a file |
| `rm -rf folder` | Force and recursively removes a directory and its contents |
| `ls -la` | Lists files including hidden files with detailed information |
| `cat .*` | Attempts to display hidden files |
| `cat ./ *` | Attempts to read files in the current directory |
| `touch "--spaces in this filename--"` | Creates a file with spaces and leading dashes |
| `echo "Hello Linux" > "--spaces in this filename--"` | Creates/writes text to the special filename |
| `cat -- "--spaces in this filename--"` | Reads a filename with spaces and leading dashes |
| `cat "./--spaces in this filename--"` | Reads the special filename using a path |
| `mkdir -- "--spaces in this filename--"` | Creates a directory with spaces and leading dashes |

### Permissions, Ownership, and Users

| Command | What it does |
|---------|--------------|
| `chmod 600 file` | Gives the owner read/write permissions only |
| `chmod 700 file` | Gives the owner read/write/execute permissions only |
| `chown user file` | Changes the owner |
| `chown user:group file` | Changes owner and group |
| `sudo adduser name` | Creates a new user |
| `su - user` | Switches to another user |
| `sudo -u user command` | Runs a command as another user |
| `sudo deluser name` | Deletes a user account |
| `sudo deluser --remove-home name` | Deletes the account and its home directory |
| `sudo deluser --remove-all-files name` | Deletes the account and files owned by the user |
| `getent passwd name` | Checks whether a user exists |
| `getent group name` | Checks whether a group exists |
| `groups username` | Shows the groups of a user |
| `sudo delgroup name` | Deletes a group |

---

## 🧠 Key Concepts Learned

### SSH
- **SSH** = Secure Shell, encrypted remote terminal access to computers
- **Encrypted** = all traffic is scrambled, so nobody can intercept and read it
- **Port 22** = the default SSH door, and hackers scan for it automatically
- **Client** = the computer YOU are sitting at
- **Host/Server** = the computer YOU connected TO
- **localhost** = your own machine, IP always `127.0.0.1`
- **Password auth** = login with a password, which can be brute forced
- **Key auth** = login with an SSH key, which is mathematically impossible to guess
- **Private key** = stays on YOUR computer only, NEVER share it!
- **Public key** = goes on the server, safe to share
- **known_hosts** = a file that remembers servers you connected to before
- **Passphrase** = an extra password protecting your private key
- **sshd_config** = the SSH server configuration file, which controls all SSH settings
- **RandomArt** = a visual fingerprint of your SSH key

### Special Filenames
- **Special filenames:** A filename beginning with `-` can be interpreted as a command option, while spaces can cause the shell to split one filename into multiple arguments.
- **Quotes `" "`:** Keep spaces together as part of one filename.
- **`--`:** Tells a command to stop processing options, so the following text is treated as a filename or argument.
- **`./`:** Specifies that the name is a path in the current directory, preventing a filename beginning with `-` from being interpreted as an option.
- **Creating a file with spaces:** `touch "--spaces in this filename--"`
- **Adding text to a file:** `echo "Hello Linux" > "--spaces in this filename--"`
- **Reading a special filename:** `cat -- "--spaces in this filename--"`
- **Creating a directory with spaces and leading dashes:** `mkdir -- "--spaces in this filename--"`

### Removing Files and Folders
- **`rm -r`:** Removes directories/folders and their contents recursively.
- **`rm -f`:** Force removes files without asking for confirmation. It does not remove directories by itself.
- **`rm -rf`:** Combines recursive and force options, allowing directories and their contents to be removed without confirmation. It is dangerous if used on the wrong path.
- **`r` = recursive:** Allows `rm` to work with directories and their contents.
- **`f` = force:** Tells `rm` to remove without confirmation and ignore some errors such as missing files.

### Permissions, Users, and Safety
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
- **Command safety:** Before using a command, especially one containing `sudo`, `rm`, `-r`, or `-f`, I should understand exactly what it will affect.

---

## 🔑 SSH Key Types

| Key Type | Age | Security | Recommendation |
|----------|-----|----------|----------------|
| RSA | 1977, old | Good but aging | Being phased out |
| ECDSA | Medium age | Better | Acceptable |
| ED25519 | 2011, new | Best | Always use this! |

---

## 🔐 SSH Key Permissions

- Private key `id_ed25519` = `chmod 600` = only the owner reads. **CORRECT**
- Public key `id_ed25519.pub` = `chmod 644` = everyone reads. **CORRECT**

If the private key has wrong permissions, SSH refuses to connect:

```
WARNING: UNPROTECTED PRIVATE KEY FILE!
Permissions 0644 are too open
```

---

## 🔒 SSH Config File: `/etc/ssh/sshd_config`

| Setting | Default | Secure Value | Why |
|---------|---------|--------------|-----|
| Port | 22 | Random, e.g. 47832 | Hides from automated scanners |
| PermitRootLogin | prohibit-password | no | Root login = full system access if hacked |
| PasswordAuthentication | yes | no | Eliminates brute force attacks completely |
| PermitEmptyPasswords | no | no | Never allow blank passwords |

> ⚠️ Change these settings only on real servers, not on a practice machine.

---

## 📊 My SSH Files

| File | What it is |
|------|-----------|
| `~/.ssh/id_ed25519` | Private key, `chmod 600`, NEVER SHARE |
| `~/.ssh/id_ed25519.pub` | Public key, `chmod 644`, safe to share |
| `~/.ssh/known_hosts` | Servers I connected to before |

---

## 🔐 Cybersecurity Connections

### Brute Force Attack Detection
```bash
sudo cat /var/log/auth.log | grep "Failed"
```
Multiple failed logins from the same IP = brute force attack!

### SSH Hardening Checklist for Real Servers
- Change the port from 22 to a random number
- Disable root login completely
- Disable password authentication, keys only
- Use ED25519 keys with a passphrase
- Monitor `/var/log/auth.log` regularly

### Man in the Middle Attack Warning
If the server fingerprint changes unexpectedly you will see:

```
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
```

This means someone may be intercepting your connection. Never ignore this warning!

### Private Key Theft
If the private key has `chmod 644`, other users on the same system can read it. They can copy and use it to impersonate you. Always keep the private key at `chmod 600`!

---

## 💡 Big Insight

> *"SSH keys are not just convenience, they are security."*
> Passwords can be guessed, stolen, and brute forced.
> SSH keys are mathematically generated randomness.
> A hacker would need millions of years to guess your ED25519 key.
> This is why every serious server uses key authentication only.
> In Year 2 when I set up AWS, SSH keys will be my first security step!

---

## ❓ Interview Questions I Can Now Answer

**Q: What is SSH and why is it used?**
A: SSH (Secure Shell) is a protocol for secure encrypted remote access to computers through the terminal. It encrypts all traffic between client and server, making it impossible for anyone to intercept commands or data. It is the standard way administrators and developers manage remote servers.

**Q: What is the difference between SSH password and key authentication?**
A: Password authentication requires typing a password, which can be guessed, stolen, or brute forced. Key authentication uses a mathematically generated key pair: the private key stays on your computer and the public key goes on the server. Keys are impossible to guess and eliminate brute force attacks completely.

**Q: Why should you change the SSH default port 22?**
A: Hackers use automated robots that scan the entire internet for open port 22. Changing to a random port like 47832 means these robots skip your server completely, stopping most automated attacks without any other changes.

**Q: What happens if SSH private key permissions are wrong?**
A: SSH refuses to connect and shows `WARNING: UNPROTECTED PRIVATE KEY FILE`. If permissions are too open, other users on the same system could read and steal the private key to impersonate you. The private key must always be `chmod 600`.

**Q: What is the known_hosts file?**
A: `known_hosts` stores fingerprints of servers you have connected to before. When you reconnect, SSH verifies the fingerprint matches. If it changed unexpectedly, SSH warns you. This could indicate a Man in the Middle attack where someone is intercepting your connection.

**Q: What does `PermitRootLogin no` mean in sshd_config?**
A: It prevents the root user from logging in via SSH directly. This is critical because if a hacker logs in as root they have complete unrestricted control over the entire system immediately.

---

## 🔧 Challenges & Fixes

- **Filename starts with `-`:** Linux may interpret it as a command option. Fix: use `--` or `./` before the filename.
- **Filename contains spaces:** The shell separates words at spaces. Fix: use quotes or escape each space with `\`.
- **`cat -- --spaces in this filename--` fails:** `--` solves the leading dash problem, but the shell still splits the filename at spaces. Fix: use quotes.
- **`cat "--spaces in this filename--"` fails:** Quotes solve the spaces problem, but the filename still begins with `-`. Fix: use `--` or `./`.
- **Correct solution:** `cat -- "--spaces in this filename--"` or `cat "./--spaces in this filename--"`.
- **Deleting directories with normal `rm`:** `rm` does not remove directories by itself. Fix: use `rm -r` when intentionally removing a directory.
- **Using `rm -rf`:** It can remove a directory and everything inside it without confirmation. Fix: always check the path before running it.
- **Permission errors:** A user may not have permission to modify a file. Fix: check ownership and permissions using `ls -l`, and use `sudo` only when necessary.
- **User and group names:** Linux is case-sensitive and requires the exact login/group name.

---

## 📝 Revision Practice

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

---

## ➡️ Next Steps

- Learn UFW firewall basics
- Understand what a firewall does
- Allow and deny specific ports
- Check firewall status
- Connect firewall rules to SSH port knowledge
- Practice finding files by owner, group, and size
- Practice `chmod` and `chown` again in a safe test folder
- Practice special filenames without looking at my notes
- Continue documenting commands, errors, solutions, and lessons learned
- Learn more Linux commands needed for cybersecurity and DevSecOps
