# Day 07 — Linux Process Management: Monitoring

**Date:** [9th October]
**Focus:** Understanding what is actually running on a Linux system (`ps`, `ps aux`, `top`), what each user and process name means (`root`, `systemd`, `chrony`, `syslog`, `message+`), and where the system records everything (`/var/log/syslog`)

## Objectives
- Understand what a process is and how to see what is running
- Read the output of `ps aux` and `top`
- Learn what the common users and processes (`root`, `systemd+`, `message+`, `chrony`, `syslog`) are responsible for
- Find and read the system log in `/var/log`
- Get a first look at how to stop processes (`kill`, `killall`) and run them in the background (`&`)

## What I Did
- Wrote the four parts of process management in my notes: Monitoring, Controlling, Backgrounding, Prioritizing (today was Monitoring only)
- Ran `ps` and `ps aux` to list running processes
- Used `top` to watch processes live
- Identified the users and processes in the output: `root`, `systemd+`, `message+`, `chrony`, and `syslog`
- Read the system log with `sudo tail /var/log/syslog`
- Noted down `sleep 1000 &`, `kill PID`, and `killall sleep` for the Controlling and Backgrounding parts
- Fixed the mistakes in my first notes after review (see Challenges & Fixes)

## Key Concepts Learned
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
- **Log files:** `/var/log/syslog` is the general system log, `/var/log/auth.log` holds logins and `sudo` use, and `/var/log/kern.log` holds kernel messages.
- **`tail`:** `tail` shows only the last 10 lines of a file. `tail -f` keeps watching the file live (`Ctrl+C` to stop).
- **`sleep 1000 &`:** starts a dummy process for 1000 seconds. The `&` at the end sends it to the background.
- **`kill` vs `killall`:** `kill PID` ends the process with that PID, and `killall sleep` ends every process named `sleep`.
- **Logs are evidence:** logs are the evidence trail for audits and incident response, so they are read, never edited.

## Commands Summary

| Command | Purpose |
|---|---|
| `ps` | Show the processes running in the current terminal |
| `ps aux` | Show all running processes from all users |
| `ps -ef` | Same as `ps aux` in a different format (shows the parent PID) |
| `ps aux \| grep name` | Find a specific process by name |
| `top` | Live view of running processes, refreshing every 3 seconds |
| `sleep 1000 &` | Start a dummy 1000-second process in the background |
| `kill PID` | Kill the process with that PID |
| `killall sleep` | Kill all processes named `sleep` |
| `sudo tail /var/log/syslog` | Show the last 10 lines of the system log |
| `sudo tail -f /var/log/syslog` | Watch the system log live |

## Challenges & Fixes
- **Thought `root`, `systemd+`, `chrony`, and `syslog` were types of process:** they are usernames from the USER column of `ps aux`. Fix: read the command column to see which process each user runs (for example `chrony` runs `chronyd`).
- **Thought `systemd+` was the background process manager:** it is a truncated username for service accounts. Fix: the manager itself is `systemd`, PID 1, owned by `root`.
- **Wrote that `ps` shows current running processes:** plain `ps` only shows the current terminal. Fix: use `ps aux` to see everything.
- **Wrote `kill all sleep` as three words:** the command is one word. Fix: `killall sleep`.
- **Filed `sleep 1000 &` under Monitoring:** the `&` is what sends it to the background. Fix: it belongs under Backgrounding.
- **`tail` showed too few lines:** `tail` only shows the last 10 lines by default. Fix: use `sudo tail -f /var/log/syslog` to watch live, or `tail -n 50` for more lines.

## Next Steps
- Controlling: `kill`, signals, and force-terminating stuck applications
- Backgrounding: `&`, `jobs`, `fg`, and `bg`
- Prioritizing: `nice` and `renice`
- Re-explain what each user and process in `ps aux` does, in my own words (self-check)
- Keep documenting each topic with commands, errors, and fixes
