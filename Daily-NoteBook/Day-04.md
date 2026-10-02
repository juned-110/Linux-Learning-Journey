# Day 4 — Linux Basics: File Creation, Permissions, and Dash-Named Files
**Date:** [26th september 2026]
**Focus:** Learning how to create empty files, control file permissions with `chmod`, and read files whose names start with a dash (`-`)

## Objectives
- Learn how to create empty files with `touch`
- Understand Linux file permissions (read, write, execute) and how they are written as numbers
- Learn how to change permissions with `chmod`
- Understand why filenames starting with `-` cause problems and how to handle them
- Learn how to read files in the current directory with `cat ./*`

## What I Did
- Created empty files with `touch` and edited them with `nano`
- Studied the permission values: r = 4, w = 2, x = 1, - = 0
- Learned how permissions are split between User, Group, and Others
- Practiced `chmod` with numeric permissions (example: `chmod 402 <filename>`)
- Learned how Linux treats filenames that start with `-`
- Read files with dash-names using `./` and `cat ./*`

## Key Concepts Learned
- **`touch`:** creates an empty file, or updates the timestamp of an existing file. Use `nano filename` afterwards to edit it.
- **`chmod`:** "change mode." It changes the permissions of a file or folder.
- **Permission values:**

  | Permission | Number |
  |---|---|
  | r (read) | 4 |
  | w (write) | 2 |
  | x (execute) | 1 |
  | - (none) | 0 |

- **Permission groups:** permissions are set for three categories, in this order:

  | User (owner) | Group (family) | Others |
  |---|---|---|
  | rwx | rwx | rwx |

- **How the numbers work:** each digit of the chmod number is the sum of the permissions for one group.
  Example: `chmod 402 <filename>` → `4` = `r--` (User), `0` = `---` (Group), `2` = `-w-` (Others), so the result is `r-- --- -w-`.
- **Filenames starting with `-`:** Linux may treat a name like `-file` as a command option instead of a filename. Putting `./` in front (`./-file`) tells Linux it is a path to a file. Using `--` (double dash) also marks the end of options, e.g. `cat -- -file`.
- **`cat ./*`:** reads all files in the current directory, including files whose names start with `-`, because each name is passed with `./` in front of it.

## Commands Summary

| Command | Purpose |
|---|---|
| `touch filename` | Create an empty file (or update its timestamp) |
| `nano filename` | Edit the file |
| `chmod 402 filename` | Change file permissions using numbers |
| `./-filename` | Refer to a file whose name starts with `-` |
| `cat -- -filename` | Read a dash-named file using the end-of-options marker |
| `cat ./*` | Read all files in the current directory, including dash-named ones |

## Challenges & Fixes
- **Dash-named files treated as options:** `cat -filename` fails because `cat` reads `-filename` as an option. Fix: use `cat ./-filename` or `cat -- -filename`.
- **Remembering permission numbers:** it is easy to mix up which digit belongs to which group. Fix: remember the order User → Group → Others, and add r=4, w=2, x=1 for each group.
- **`cat ./*` skips hidden files:** the `*` pattern does not match names starting with `.`. Fix: use `ls -la` to see hidden files and read them by name.

## Next Steps
- Practice `chmod` with different numbers (e.g. 644, 755) and check results with `ls -l`
- Practice reading dash-named files in a safe test folder
- Continue the next Bandit level
- Keep documenting each level with commands, errors, and fixes
