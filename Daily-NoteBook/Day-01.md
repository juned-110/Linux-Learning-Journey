# Day 01 — Linux Learning Journey

**Name:** Juned Javed
**Date:** September 21, 2026
**Focus:** Establishing a working Linux environment and public documentation infrastructure

---

## 🎯 Objectives

- Set up a Linux environment for hands-on practice
- Establish a public GitHub presence for documenting progress
- Create a system for logging commands, errors, and solutions

---

## ✅ What I Accomplished Today

- Installed and set up Kali Linux through a Virtual Machine as my working Linux environment
- Set up my username and password
- Updated all system packages
- Practiced first Linux commands
- Created a GitHub account and enabled two-factor authentication for security
- Set up a public profile README to introduce my learning journey
- Created this repository (`linux-learning-journey`) to document daily progress

---

## 🖥️ Commands Learned

| Command | What it does |
|---------|-------------|
| `pwd` | Shows current location (Print Working Directory) |
| `ls` | Lists files and folders in current directory |
| `mkdir foldername` | Creates a new folder |
| `rmdir foldername` | Deletes an empty folder |
| `sudo apt update && sudo apt upgrade -y` | Updates all system packages |

---

## 🧠 Key Concepts Learned

- **Kali Linux** is a Debian-based Linux distribution designed primarily for cybersecurity, penetration testing, and security research
- A virtual machine allows Kali Linux to run in an isolated environment alongside Windows without replacing the main operating system
- **Terminal** = The command line interface where you type commands
- **Home folder** = `~` (for example `/home/<username>`) — my personal space in Linux
- **Spaces in folder names** = need quotes `" "` or backslash `\ `
- **Linux is case sensitive** — `MyFolder` and `myfolder` are different!
- A GitHub repository named exactly like your username displays its README on your public profile page
- Two-factor authentication adds a second verification step beyond a password, reducing account takeover risk

---

## 💡 Big Insight

> *"Windows is the roof, Linux is the basement"*
> Windows shows you what they want you to see.
> Linux shows you EVERYTHING — nothing is hidden!

---

## ❓ What Confused Me

- `mkdir folder my` creates TWO folders instead of one — spaces matter!
- Linux doesn't show password characters while typing — that's normal and secure!

---

## 🔧 Challenges & Fixes

- While turning on two-factor authentication, the problem I faced was that I was not familiar with authenticator apps. I searched online and learned that an authenticator app is used to generate verification codes for two-factor authentication. I downloaded Google Authenticator on my mobile phone and used it to complete the setup. Apart from this, the rest of the process went smoothly.

---

## ➡️ Next Steps

- Learn core terminal navigation commands (`pwd`, `ls`, `cd`, `cat`, `file`, `find`)
- Learn `touch` and `rm`
- Practice navigating the Linux filesystem
- Begin OverTheWire Bandit (Levels 0–2)
- Set up the `bandit-solutions/` documentation structure
