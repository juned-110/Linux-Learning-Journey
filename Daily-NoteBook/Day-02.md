# Navigation Commands and Special Filenames

**Name:** Juned Javed 
**Focus:** Learning navigation commands and understanding how the shell and `cat` handle special filenames

---

## 🎯 Objectives

- Learn navigation commands
- Learn why some filenames cannot be opened with a plain `cat`
- Document the commands, errors, and fixes

---

## ✅ What I Accomplished

- Learned navigation commands
- Worked with a file named `-` and a file named `--spaces in this filename--`
- Tried the obvious commands first, saw them fail, and researched why

---

## 🖥️ Commands Learned

| Command | What it does |
|---------|-------------|
| `cd foldername` | Go inside a folder |
| `cd ..` | Go back one folder |
| `cd ~` | Go home instantly |
| `cd /` | Go to root of system |
| `cp file destination` | Copy a file to another location |
| `file filename` | Check what type a file is |
| `cat ./-` | Read a file named `-` |
| `cat -- "--spaces in this filename--"` | Read a file with spaces and dashes in its name |
| `shred -u filename` | Securely delete a file |

---

## 🧠 Key Concepts Learned

### Linux Filesystem
- `/mnt` = the standard location where extra filesystems are mounted (mnt = mount)
- Everything in Linux is a file or folder, even hard drives!

### Filenames, Options, and the Shell
- **Dash-prefixed filenames:** a name starting with `-` can be mistaken for an option (like `--help`) instead of a file.
- **`--` (double dash):** a Unix convention meaning "options end here; everything after this is a filename or argument."
- **`./` prefix:** `./-` explicitly means "the file named `-` in the current directory," so it can't be mistaken for an option or for standard input.
- **`-` means standard input:** for `cat` (and many tools), a lone `-` means "read from stdin," not "open a file named `-`." This is why `cat -` just hangs waiting for input.
- **Spaces split arguments:** the shell splits the command at spaces *before* `cat` runs, so a filename with spaces must be quoted (`"..."`) or escaped (`\ `).
- **Order of operations:** the shell processes the line first (splitting, quoting), then the program parses its arguments. Knowing which stage is causing the problem is the key to debugging.

### Quotes in Linux
| Type | When to use |
|------|------------|
| `"double quotes"` | Normal use, but `$` becomes a variable |
| `'single quotes'` | When the path contains a `$` sign |
| `backslash\ space` | Alternative for spaces in names |

### Deleted Files
- Deleted files are recoverable until overwritten!
- Tool for secure deletion: `shred -u filename`

---

## 💡 Big Insights

> *"Deleted doesn't mean gone!"*
> Files remain on disk until overwritten by new data.
> This is why Digital Forensics is a real career skill!

> *"Linux exposes EVERYTHING."*
> Cybersecurity professionals need to see the basement, because attackers hide there!

---

## ❓ What Confused Me

- `$` sign needs single quotes in Linux paths
- `cat -` hangs because `-` is treated as "read from keyboard"

---

## 🔧 Challenges & Fixes

- **`cat -` hung with no output.** `cat` treated `-` as "read from keyboard input." Pressing `Ctrl+C` exits. Fix: `cat ./-`.
- **`cat -- -` also did not work as expected.** `--` stops option parsing, but `-` is still treated by `cat` as stdin, not a filename. The `./` prefix is the reliable fix for this file.
- **`cat --spaces in this filename--` failed.** The shell split it into four separate arguments, and `--spaces` was read as an invalid option. Fix: quote the name and stop option parsing: `cat -- "--spaces in this filename--"`.
- **Typo:** I typed `,/` instead of `./` at one point. A small reminder to read the command carefully before pressing Enter.

---

## ➡️ Next Steps

- Practice `ls -a`, `cd`, and `file`
- Learn `touch` (create files), `cat` (read files), `nano` (edit files), and `rm` (delete files)
- Practice creating and editing files from the terminal
