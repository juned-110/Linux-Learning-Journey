# File Permissions, chmod, chown, and Dash-Named Files

**Name:** Juned Javed
**Focus:** Learning how to create empty files, understanding Linux file permissions, controlling them with `chmod` and `chown`, and reading files whose names start with a dash (`-`)

---

## 🎯 Objectives

- Learn how to create empty files with `touch`
- Understand Linux file permissions (read, write, execute) and how they are written as numbers
- Learn how to change permissions with `chmod`
- Learn how to change file ownership with `chown`
- Understand real cybersecurity use cases of permissions
- Understand why filenames starting with `-` cause problems and how to handle them
- Learn how to read files in the current directory with `cat ./*`

---

## ✅ What I Accomplished

- Created empty files with `touch` and edited them with `nano`
- Learned how Linux file permissions work
- Studied the permission values: r = 4, w = 2, x = 1, - = 0
- Learned how permissions are split between User, Group, and Others
- Learned to read permission output from `ls -la`
- Learned `chmod` with both the symbol method and the number method
- Practiced `chmod` with numeric permissions (example: `chmod 402 <filename>`)
- Learned `chown` to change file ownership
- Understood real cybersecurity use cases of permissions
- Discovered why `chmod 777` is dangerous
- Tested "Permission denied" by locking files with `chmod 000`
- Learned how Linux treats filenames that start with `-`
- Read files with dash-names using `./` and `cat ./*`

---

## 💻 Commands Learned

| Command | What it does |
|---------|--------------|
| `touch filename` | Creates an empty file (or updates its timestamp) |
| `nano filename` | Edits the file |
| `ls -la` | Shows all files with permissions and owner |
| `chmod +x file` | Adds execute permission |
| `chmod -w file` | Removes write permission |
| `chmod 402 filename` | Changes file permissions using numbers |
| `chmod 600 file` | Owner read+write only, nobody else |
| `chmod 644 file` | Owner read+write, everyone read only |
| `chmod 755 file` | Owner full, everyone read+execute |
| `chmod 777 file` | Everyone full permission (dangerous!) |
| `chmod 000 file` | Nobody can do anything |
| `chown root file` | Changes owner to root |
| `chown <username> file` | Changes owner back to yourself |
| `sudo chown root file` | Changes owner with admin power |
| `echo "text" > file` | Writes text into a file instantly |
| `echo "text" >> file` | Adds text to a file without deleting old content |
| `./-filename` | Refers to a file whose name starts with `-` |
| `cat -- -filename` | Reads a dash-named file using the end-of-options marker |
| `cat ./*` | Reads all files in the current directory, including dash-named ones |

---

## 🧠 Key Concepts Learned

### Creating Files
- **`touch`:** creates an empty file, or updates the timestamp of an existing file. Use `nano filename` afterwards to edit it.
- **echo** = prints text on screen or writes text into a file instantly

### Permissions
- **`chmod`:** "change mode." It changes the permissions of a file or folder.
- **Permission Groups** = 3 types: owner (u), group (g), others (o)
- **Permission Types** = r (read = 4), w (write = 2), x (execute = 1), - (none = 0)
- **Dash `-`** = always holds the position of a missing permission
- **Permission groups order:** permissions are set for three categories, in this order:

  | User (owner) | Group (family) | Others |
  |---|---|---|
  | rwx | rwx | rwx |

- **chmod numbers** = add the r+w+x values together for each group. Each digit of the chmod number is the sum of the permissions for one group.
  Example: `chmod 402 <filename>` → `4` = `r--` (User), `0` = `---` (Group), `2` = `-w-` (Others), so the result is `r-- --- -w-`.

### Ownership
- **chown** = changes WHO owns the file, chmod changes WHAT they can do
- **sudo** = run a command as administrator (root)
- **File owner vs Folder owner** = owning a folder lets you delete files inside even if the file belongs to root

### Dash-Named Files
- **Filenames starting with `-`:** Linux may treat a name like `-file` as a command option instead of a filename. Putting `./` in front (`./-file`) tells Linux it is a path to a file. Using `--` (double dash) also marks the end of options, e.g. `cat -- -file`.
- **`cat ./*`:** reads all files in the current directory, including files whose names start with `-`, because each name is passed with `./` in front of it.

---

## 🔢 chmod Number System

| Number | Permission | Calculation |
|--------|------------|-------------|
| 7 | rwx | 4+2+1 |
| 6 | rw- | 4+2 |
| 5 | r-x | 4+1 |
| 4 | r-- | 4 |
| 2 | -w- | 2 |
| 0 | --- | 0 |

---

## 🔐 Real World Permission Uses

| Permission | Where Used | Why |
|------------|------------|-----|
| `600` | SSH private keys | Only you can read, so hackers cannot steal it |
| `644` | Normal files | Everyone reads, only owner edits |
| `755` | Scripts and programs | Everyone runs, only owner modifies |
| `700` | Private folders | Only owner can open the folder |
| `000` | Fully locked files | Nobody can touch it at all |
| `777` | NEVER use this | Everyone can modify, extremely dangerous |

---

## 💡 Big Insight

> *"chmod controls WHAT can be done, chown controls WHO does it"*
> In Linux I am the boss of my own files.
> I decide who can read, write, and execute, and nobody else.
> This is exactly how system administrators protect servers
> and exactly what hackers look for when attacking systems.

---

## ❓ What Confused Me

- Thought `chown root` alone would block deletion, but folder ownership still allows it
- `chmod` and `chown` must be used TOGETHER for full protection
- `sudo chown` needs the admin password, but sudo remembers it for a few minutes

---

## 🔧 Challenges & Fixes

- **Dash-named files treated as options:** `cat -filename` fails because `cat` reads `-filename` as an option. Fix: use `cat ./-filename` or `cat -- -filename`.
- **Remembering permission numbers:** it is easy to mix up which digit belongs to which group. Fix: remember the order User → Group → Others, and add r=4, w=2, x=1 for each group.
- **`cat ./*` skips hidden files:** the `*` pattern does not match names starting with `.`. Fix: use `ls -la` to see hidden files and read them by name.

---

## ➡️ Next Steps

- Practice `chmod` with different numbers (e.g. 644, 755) and check results with `ls -l`
- Practice reading dash-named files in a safe test folder
- Learn process management (`ps`, `kill`, `top`)
- Learn SSH basics
- Understand how Linux manages running programs
