---
title: Linux CLI Basics
source: TryHackMe (Operating Systems module)
platform: TryHackMe
module: Operating Systems
tags: [cybersecurity, tryhackme, linux, cli, terminal, bash, filesystem, beginner]
status: in-progress
---

# 🐧 Linux CLI Basics

> [!info] Room Info
> **Module:** Operating Systems
> Goal: Understand what the Linux terminal is, get comfortable navigating the filesystem, and learn to gather basic system information — all through a "new intern" mission scenario.

---

## 1. Introduction

Linux is everywhere in cyber security — servers, security tools, hacking environments. Before defending systems or investigating incidents, you need to navigate Linux via the **command-line interface (CLI)**.

> [!quote] Scenario
> You're a brand-new intern on a cyber security team, working through a guided mission via hands-on tasks.

### Learning Objectives
- Understand what the Linux terminal is and what it's used for
- Feel comfortable interacting with the Linux environment
- Navigate the Linux filesystem with basic commands

---

## 2. A Quick Note About the Terminal

The **terminal** is a text-based interface for controlling a Linux system — you type commands instead of clicking through a GUI.

> [!tip] Why Security Professionals Use the Terminal
> - Faster than clicking around
> - Gives more control
> - Many security tools **only** run in the terminal

If it feels unfamiliar now, that's normal — it becomes second nature with repetition.

---

## 3. Interacting With the Terminal — Core Navigation Commands

> [!quote] Mission
> Find a file called `mission_brief.txt` somewhere on the system.

### Step 1 — "Where Am I?"

```bash
pwd
```
> **P**rint **W**orking **D**irectory — shows the folder you're currently in.

```
ubuntu@tryhackme:~$ pwd
/home/ubuntu
```

### Step 2 — "What's Around Me?"

```bash
ls          # list contents of current directory
ls -l       # long format: permissions, size, date, etc.
ls -al      # long format + hidden files
```

**`ls`** output:
```
Desktop    Downloads  Pictures  Templates  logs
Documents  Music      Public    Videos     projects
```

**`ls -l`** adds detail — permissions, owner, size, date modified — for every item.

> [!tip] Hidden Files
> Files starting with a dot (`.`) are hidden by default in Linux — not "secret," just hidden from a plain `ls`. Use `ls -al` to reveal them (also shows `.` = current dir, `..` = parent dir).

### Step 3 — Moving Around

```bash
cd <directory>    # move into a directory
cd ..              # move up one level
cd ~               # go to home directory
```

Example:
```
ubuntu@tryhackme:~$ cd Documents/
ubuntu@tryhackme:~/Documents$ pwd
/home/ubuntu/Documents

ubuntu@tryhackme:~/Documents$ cd ..
ubuntu@tryhackme:~$ pwd
/home/ubuntu
```

### Step 4 — Finding Files with `find`

```bash
find <starting_point> -name <filename>
```

Example — searching the whole home directory (`~`) for `mission_brief.txt`:
```bash
find ~ -name mission_brief.txt
```
```
/<path>/mission_brief.txt
```

> [!note] What's Happening
> `find` checks every folder inside the starting point — this can take a moment on large filesystems. If found, it prints the full path.

### Step 5 — Reading a File with `cat`

```bash
cat <filename>
```

`cat` (con**cat**enate) prints a file's contents directly to the terminal — the fastest way to read short text files.

> [!question]- 🧪 Quick Quiz: Terminal Navigation
> 1. What does `pwd` stand for, and what does it show?
> 2. What's the difference between `ls`, `ls -l`, and `ls -al`?
> 3. How do you tell if a file is "hidden" in Linux, just from its name?
> 4. What command moves you up one directory level?
> 5. Write the `find` command to search your entire home directory for a file called `notes.txt`.
> 6. What does `cat` do?
>
> **Answers**
> 1. "Print Working Directory" — shows the folder you're currently in.
> 2. `ls` = basic listing; `ls -l` = detailed listing (permissions, size, date); `ls -al` = detailed listing including hidden files.
> 3. Its name starts with a dot (`.`).
> 4. `cd ..`
> 5. `find ~ -name notes.txt`
> 6. Prints a file's contents to the terminal.

---

## 4. Gathering System Information

> [!quote] Next Mission
> Collect a small system report: who you're logged in as, the kernel version, total disk space, and the Linux distribution name.

### Who Am I?

```bash
whoami
```
Prints your current username.
```
ubuntu@tryhackme:~$ whoami
ubuntu
```

### What System Am I On?

```bash
uname -a
```
Full system info line:
```
Linux tryhackme <version>-aws #17-Ubuntu SMP Mon Sep 2 13:48:07 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux
```

**Breakdown:**

| Field | Meaning |
|---|---|
| `Linux` | The kernel running |
| `tryhackme` | Hostname |
| `<version>-aws` | Kernel version |
| `x86_64` | Hardware platform (64-bit) |
| `GNU/Linux` | OS type (Linux kernel + GNU tools) |

> [!tip] Just the OS Name?
> `uname` (no flags) prints just `Linux`. `uname -a` gives the full picture — use `-a` when you actually need the details.

### Checking Disk and Storage

```bash
df -h
```
`-h` = **h**uman-readable (shows `2G`, `500M` instead of raw byte counts).

```
Filesystem      Size  Used Avail Use% Mounted on
/dev/root        20G   12G    7G  17% /
tmpfs           1.9G     0  1.9G   0% /dev/shm
tmpfs           774M  1.2M  773M   1% /run
```

**Breakdown:**

| Entry | Meaning |
|---|---|
| `/dev/root` | Main disk — total/used/available size and % full |
| `tmpfs` | Temporary filesystem stored in **RAM**, not physical disk |
| `/dev/shm` | Shared memory area |
| `/run/user/<id>` | Per-user temporary storage |

### Reading a System File

Linux configuration/info files live in `/etc`.

```bash
cd /etc
ls
cat os-release
```

`os-release` gives clean distro details:
```
PRETTY_NAME="Ubuntu 24.04.1 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.1 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
```

> [!success] Why `os-release` > `uname` for Distro Info
> `os-release` gives clearer, more complete distribution details (full name, version codename, etc.) than `uname` alone provides.

> [!question]- 🧪 Quick Quiz: System Information
> 1. What command tells you your current username?
> 2. What does `uname -a` show that plain `uname` doesn't?
> 3. In `uname -a` output, what does `x86_64` refer to?
> 4. What does the `-h` flag do in `df -h`, and why is it useful?
> 5. What's the difference between the `/dev/root` and `tmpfs` entries in `df -h` output?
> 6. Where does Linux typically store config/info files like `os-release`?
> 7. Why might you prefer `cat /etc/os-release` over `uname` for identifying the distro?
>
> **Answers**
> 1. `whoami`
> 2. The full system info — hostname, kernel version, hardware platform, OS type — not just the kernel name.
> 3. The hardware platform (64-bit architecture).
> 4. Converts raw byte counts into human-readable units (like `2G`, `500M`) — much easier to read at a glance.
> 5. `/dev/root` is the actual physical disk; `tmpfs` entries are temporary filesystems stored in RAM, not on disk.
> 6. `/etc`
> 7. `os-release` gives clearer, more complete distribution details (full name, version, codename) than `uname` provides.

---

## 5. Wrapping Up

By the end of this room, you've navigated the filesystem, searched for (and read) files, and gathered core system information — the foundational skill set for any further Linux work, from general use to security investigation.

---

## 🧠 Key Takeaways — Command Cheat Sheet

| Command | Purpose |
|---|---|
| `pwd` | Show current directory |
| `ls` / `ls -l` / `ls -al` | List directory contents (basic / detailed / detailed + hidden) |
| `cd <dir>` / `cd ..` / `cd ~` | Move into a directory / up one level / to home |
| `find <path> -name <file>` | Search for a file by name starting from a given path |
| `cat <file>` | Print a file's contents |
| `whoami` | Show current username |
| `uname` / `uname -a` | Show OS name / full system info |
| `df -h` | Show disk usage in human-readable format |

- The terminal is faster, more precise, and often the *only* way to run many security tools — worth building fluency early.
- Hidden files/dotfiles aren't secret, just filtered out of the default `ls` view.
- `find` searches recursively from a starting point — can be slow on large trees, but reliable.
- `/etc` is the standard home for Linux configuration files; `os-release` is a quick, reliable way to ID a distro.

## 📝 Full Module Recap Quiz
> [!question]- End-to-End Review (test yourself without peeking at the sections above)
> 1. Write the full sequence of commands you'd use to: check where you are, list contents (with hidden files), move into a folder called `logs`, and go back up.
> 2. Write the `find` command to locate a file named `report.csv` anywhere under your home directory.
> 3. What does each field in a typical `uname -a` output represent?
> 4. What does `df -h` show, and what does the `-h` flag change about the output?
> 5. Where does Linux keep most system configuration files, and what's a quick way to check your distro name and version?
> 6. Why do cyber security professionals favor the terminal over a GUI?

## 🔗 Related Notes
- [[What is an Operating System]]
- [[Windows Basics]]
- [[Windows CLI Basics]]
- [[Inside a Computer System]]
- [[Operating Systems MOC]]

## 📌 Next Steps
- [ ] Practice these commands on a real Linux VM or WSL install
- [ ] Continue to [[Windows CLI Basics]] to compare the two CLI philosophies
- [ ] Revisit quiz sections and rebuild the command cheat sheet from memory for spaced repetition
