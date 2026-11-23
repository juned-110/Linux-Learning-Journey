# Day 2 — Filenames, Options, and Bandit Levels 1–3

**Date:** [fill in date]  
**Focus:** Understanding how the shell and `cat` handle special filenames, and completing Bandit Levels 1→2 and 2→3

## Objectives
- Learn why some filenames cannot be opened with a plain `cat`
- Complete Bandit Level 1 → Level 2
- Complete Bandit Level 2 → Level 3
- Document the commands, errors, and fixes for both levels

## What I Did
- Logged in to the Bandit server over SSH and worked through Level 1 → 2 (file named `-`)
- Worked through Level 2 → 3 (file named `--spaces in this filename--`)
- Tried the obvious commands first, saw them fail, and researched why
- Wrote up both levels in the `bandit-solutions/` folder

## Key Concepts Learned
- **Dash-prefixed filenames:** a name starting with `-` can be mistaken for an option (like `--help`) instead of a file.
- **`--` (double dash):** a Unix convention meaning "options end here; everything after this is a filename or argument."
- **`./` prefix:** `./-` explicitly means "the file named `-` in the current directory," so it can't be mistaken for an option or for standard input.
- **`-` means standard input:** for `cat` (and many tools), a lone `-` means "read from stdin," not "open a file named `-`." This is why `cat -` just hangs waiting for input.
- **Spaces split arguments:** the shell splits the command at spaces *before* `cat` runs, so a filename with spaces must be quoted (`"..."`) or escaped (`\ `).
- **Order of operations:** the shell processes the line first (splitting, quoting), then the program parses its arguments. Knowing which stage is causing the problem is the key to debugging.

## Challenges & Fixes
- **`cat -` hung with no output.** `cat` treated `-` as "read from keyboard input." Pressing `Ctrl+C` exits. Fix: `cat ./-`.
- **`cat -- -` also did not work as expected.** `--` stops option parsing, but `-` is still treated by `cat` as stdin, not a filename. The `./` prefix is the reliable fix for this file.
- **`cat --spaces in this filename--` failed.** The shell split it into four separate arguments, and `--spaces` was read as an invalid option. Fix: quote the name and stop option parsing: `cat -- "--spaces in this filename--"`.
- **Typo:** I typed `,/` instead of `./` at one point. A small reminder to read the command carefully before pressing Enter.

## Next Steps
- Bandit Level 3 → 4 (hidden files and directories)
- Practice `ls -a`, `cd`, and `file`
- Keep documenting each level with commands, errors, and fixes
