# Firewall (UFW), Defense in Depth, and Process Monitoring

**Name:** Juned Javed
**Focus:** Understanding firewalls and configuring UFW rules, connecting them to defense in depth, and understanding what is actually running on a Linux system (`ps`, `ps aux`, `top`), what each user and process name means, and where the system records everything (`/var/log/syslog`)

---

## 🎯 Objectives

- Understand what a firewall is and why it exists
- Install UFW and configure allow, deny, and IP whitelisting rules
- Understand rule ordering and why SSH must be allowed before enabling the firewall
- Connect firewall concepts to defense in depth
- Understand what a process is and how to see what is running
- Read the output of `ps aux` and `top`
- Learn what the common users and processes (`root`, `systemd+`, `message+`, `chrony`, `syslog`) are responsible for
- Find and read the system log in `/var/log`
- Get a first look at how to stop processes (`kill`, `killall`) and run them in the background (`&`)

---

## ✅ What I Accomplished

- Understood what a firewall is and why it exists
- Installed UFW (Uncomplicated Firewall) on Linux
- Learned the golden rule: always allow SSH before enabling the firewall
- Enabled UFW and configured real firewall rules
- Allowed and denied specific ports
- Learned IP whitelisting: allow a specific IP only
- Understood rule ordering in a firewall
- Understood the difference between allow and deny
- Cleaned up firewall rules properly
- Connected firewall concepts to real cybersecurity scenarios
- Understood all 4 layers of defense in depth
- Wrote the four parts of process management in my notes: Monitoring, Controlling, Backgrounding, Prioritizing (this session covered Monitoring only)
- Ran `ps` and `ps aux` to list running processes
- Used `top` to watch processes live
- Identified the users and processes in the output: `root`, `systemd+`, `message+`, `chrony`, and `syslog`
- Read the system log with `sudo tail /var/log/syslog`
- Noted down `sleep 1000 &`, `kill PID`, and `killall sleep` for the Controlling and Backgrounding parts
- Fixed the mistakes in my first notes after review (see Challenges & Fixes)

---

## 💻 Commands Learned

### Firewall (UFW)

| Command | What it does |
|---------|--------------|
| `sudo apt install ufw -y` | Installs the UFW firewall |
| `sudo ufw status` | Checks firewall status and rules |
| `sudo ufw enable` | Turns the firewall ON |
| `sudo ufw disable` | Turns the firewall OFF |
| `sudo ufw allow 22` | Allows SSH connections |
| `sudo ufw allow 80` | Allows HTTP website traffic |
| `sudo ufw allow 443` | Allows HTTPS secure website traffic |
| `sudo ufw deny 3306` | Blocks the MySQL database port |
| `sudo ufw delete allow 80` | Deletes an allow rule |
| `sudo ufw delete deny 3306` | Deletes a deny rule |
| `sudo ufw allow from IP to any port 22` | Allows a specific IP only for SSH |
| `sudo ufw reset` | Deletes ALL rules and starts fresh |
| `echo $SSH_CONNECTION` | Checks if you are inside an SSH session |

### Process Monitoring and Logs

| Command | What it does |
|---------|--------------|
| `ps` | Shows the processes running in the current terminal |
| `ps aux` | Shows all running processes from all users |
| `ps -ef` | Same as `ps aux` in a different format (shows the parent PID) |
| `ps aux \| grep name` | Finds a specific process by name |
| `top` | Live view of running processes, refreshing every 3 seconds |
| `sleep 1000 &` | Starts a dummy 1000-second process in the background |
| `kill PID` | Kills the process with that PID |
| `killall sleep` | Kills all processes named `sleep` |
| `sudo tail /var/log/syslog` | Shows the last 10 lines of the system log |
| `sudo tail -f /var/log/syslog` | Watches the system log live |

---

## 🧠 Key Concepts Learned

### Firewall and UFW
- **Firewall** = a security guard that controls what traffic enters and exits your system
- **Port** = a numbered door on your system. Every service has its own port
- **UFW** = Uncomplicated Firewall, a simplified version of the complex iptables
- **Allow** = open a specific door for connections
- **Deny** = block a specific door completely
- **Default behavior** = UFW blocks ALL incoming connections when enabled, so allow SSH first!
- **IP whitelisting** = only specific trusted IPs are allowed through a port
- **Rule ordering** = UFW reads rules top to bottom, and the first match wins!
- **Delete rule** = you must specify the exact rule, because allow vs deny matters!
- **localhost bypass** = UFW does not block localhost connections, only external ones!
- **IPv4 and IPv6** = every rule applies to both, which is why you see a v6 duplicate

### Process Management
- **The four parts of process management:** Monitoring (what is actually running), Controlling (pausing, stopping, and force-terminating stuck applications), Backgrounding (running tasks in the terminal), and Prioritizing (telling Linux which tasks are urgent).
- **`ps` vs `ps aux`:** `ps` alone shows only the processes in my current terminal. `ps aux` shows all running processes from all users.
- **The first column is USER:** in `ps aux`, the first column is the account that owns the process. So `root`, `syslog`, `chrony`, `systemd+`, and `message+` are usernames, not types of process.
- **`root`:** the superuser account (UID 0) with full control of the system, like Administrator in Windows.
- **`systemd`:** PID 1, owned by `root`. It is the first process at boot and it starts, stops, and supervises all other services.
- **`systemd+`:** a username cut off at 8 characters (the `+` means more letters are hidden). It stands for service accounts like `systemd-resolve` and `systemd-timesync`, which handle DNS and basic time sync with limited privileges.
- **`message+`:** the account `messagebus`, which runs `dbus-daemon` (D-Bus). It lets background apps and system services talk to each other, for example an app telling the desktop to show a notification.
- **`chrony`:** runs `chronyd`, an NTP daemon (Network Time Protocol). It keeps the system time accurate by syncing with time servers on the internet.
- **`syslog`:** runs `rsyslogd`. It records authentication attempts (failed or passed), hardware warnings, and system warnings as text files in `/var/log`.
- **Why services run as their own users:** if a service is hacked, the attacker only gets that account's limited power, not root. This is the principle of least privilege.
- **`top`:** a live view of running processes that refreshes every 3 seconds. Keys: `q` quit, `M` sort by memory, `P` sort by CPU.
- **TTY column:** `?` means no terminal is attached, so it is a background service.
- **STAT codes:** `R` running, `S` sleeping, `D` waiting on disk, `T` stopped, `Z` zombie, `s` session leader, `+` foreground.
- **`sleep 1000 &`:** starts a dummy process for 1000 seconds. The `&` at the end sends it to the background.
- **`kill` vs `killall`:** `kill PID` ends the process with that PID, and `killall sleep` ends every process named `sleep`.

### Logs
- **Log files:** `/var/log/syslog` is the general system log, `/var/log/auth.log` holds logins and `sudo` use, and `/var/log/kern.log` holds kernel messages.
- **`tail`:** shows only the last 10 lines of a file. `tail -f` keeps watching the file live (`Ctrl+C` to stop).
- **Logs are evidence:** logs are the evidence trail for audits and incident response, so they are read, never edited.

---

## 🔐 Important Ports to Remember

| Port | Service | Security Note |
|------|---------|---------------|
| 22 | SSH | Always allow, and change the default port on real servers |
| 80 | HTTP | Allow for web servers. Denying it blocks the website |
| 443 | HTTPS | Allow for secure web servers |
| 3306 | MySQL | Always deny from outside. The database must be private |
| 21 | FTP | Very insecure, avoid using |
| 53 | DNS | Domain name resolution |
| 25 | SMTP | Email sending |

---

## ⚠️ Golden Rules of UFW

1. ALWAYS allow SSH port 22 BEFORE enabling UFW
2. ALWAYS specify allow or deny correctly when deleting rules
3. Rule order matters, first match wins, so put specific rules before general ones
4. Database ports should ALWAYS be denied from outside
5. Build good habits now, because these same rules apply on real AWS servers!

---

## 🔐 Cybersecurity Connections

### Defense in Depth: All 4 Layers

**Layer 1 = UFW Firewall**
- What it does: blocks unwanted connections before they reach the system
- What I learned: allow/deny ports, IP whitelisting, rule ordering
- Real use: block all ports except 22, 80, 443 on a production server

**Layer 2 = SSH Configuration**
- What it does: controls who can authenticate and how
- What I learned: `sshd_config`, `PermitRootLogin`, `PasswordAuthentication`
- Real use: disable root login, force key auth, change port 22

**Layer 3 = File Permissions**
- What it does: controls who can read, write, and execute files
- What I learned: `chmod`, `chown`, rwx numbers, private key protection
- Real use: `chmod 600` on SSH keys, `chmod 644` on public files

**Layer 4 = Process Monitoring**
- What it does: detects suspicious activity on a running system
- What I learned: `ps aux`, `top`, `kill`, reading process output
- Real use: find malware processes, kill suspicious programs

All 4 layers together = real security professional thinking! Missing even one layer = a security gap hackers will find!

### Database Protection
Port 3306 denied = hackers cannot even reach the database. Even with correct credentials, the firewall stops them before the connection!

### IP Whitelisting
Only a trusted IP is allowed for SSH. A hacker from a different IP is blocked by the firewall immediately. Even knowing your password is useless if the firewall blocks them!

### Port 80 and 443 Explained
- Allowing these does NOT expose your browsing history!
- It means your machine CAN act as a web
