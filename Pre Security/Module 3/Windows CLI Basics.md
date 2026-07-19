---
title: Windows CLI Basics
source: TryHackMe (Operating Systems module)
platform: TryHackMe
module: Operating Systems
tags: [cybersecurity, tryhackme, windows, cmd, command-prompt, cli, filesystem, beginner]
status: in-progress
---

# 🖥️ Windows CLI Basics

> [!info] Room Info
> **Module:** Operating Systems
> Goal: Navigate Windows confidently via the Command Prompt (CMD) — folders, hidden files, file search, reading files, and basic system/network info.

---

## 1. What Is the Windows Command Line?

**Command Prompt (CMD)** is a text-based interface for interacting with Windows. Instead of clicking folders and menus, you type commands — listing files, moving between folders, checking system info.

### Learning Objectives
- Use the Windows command line confidently
- Navigate folders without clicking
- Find files when you only know their name
- Read files using the terminal
- Collect basic system and network information

> [!tip] Same Skills, Different Syntax
> This mirrors [[Linux CLI Basics]] almost exactly in *purpose* — navigation, search, reading files, gathering system info — just with different commands and output formats. Worth comparing the two side by side.

---

## 2. Navigating the Filesystem

### Step 1 — "Where Am I?"

```cmd
cd
```
With no arguments, `cd` prints your current directory's full path — usually your user folder on Windows.

> [!note] `cd` Does Double Duty
> On Windows, `cd` alone **shows** your location; `cd <folder>` **changes** it. (Unlike Linux, where `pwd` and `cd` are separate commands.)

### Step 2 — "What's Around Me?"

```cmd
dir
```
Lists files and folders in the current directory (visible items only).

### Step 3 — Are There Hidden Files?

```cmd
dir /a
```
Shows **everything**, including hidden items.

> [!tip] Hidden ≠ Secret
> Same principle as Linux dotfiles — hidden just means Windows doesn't show it by default in a normal listing, not that it's protected or secret.

### Step 4 — Moving Around

```cmd
cd folder_name     :: move into a folder
cd ..               :: move up one level
```

Example: `cd Documents` moves you into the Documents folder.

> [!tip] Explore as You Go
> Use `dir` or `dir /a` inside each folder you enter to see what's there — helpful for building a mental map of the filesystem, especially when hunting for something not in an obvious location.

### Step 5 — Finding a File on Disk

```cmd
dir /s <filename>
```
The `/s` flag searches **all subfolders** starting from the current directory and prints the full path if found.

Example: `dir /s task_brief.txt`

### Step 6 — Navigate to the File

```cmd
cd <path_to_folder>
dir
```
Use the path found in Step 5, then confirm the file's presence with `dir`.

### Step 7 — Read the File

```cmd
type <filename>
```
Prints the file's contents directly in the Command Prompt — the Windows equivalent of Linux's `cat`.

> [!question]- 🧪 Quick Quiz: Navigating the Filesystem
> 1. What does `cd` with no arguments do on Windows?
> 2. What's the Windows equivalent of Linux's `ls`?
> 3. How do you show hidden files/folders in a Windows directory listing?
> 4. What does the `/s` flag do when combined with `dir`?
> 5. What command reads a file's contents directly into the terminal — and what's its Linux equivalent?
> 6. Write the full command to search your entire current directory tree for a file named `budget.xlsx`.
>
> **Answers**
> 1. Prints the current directory's full path.
> 2. `dir`
> 3. `dir /a`
> 4. Searches all subfolders from the current location, printing the full path of any match.
> 5. `type <filename>` — equivalent to Linux's `cat <filename>`.
> 6. `dir /s budget.xlsx`

---

## 3. Gathering System & Network Information

### Who Am I Logged In As?

```cmd
whoami
```
Prints the username of the currently logged-in account. Matters because **different users have different permissions**.

### What's the Computer's Name?

```cmd
hostname
```
Prints a short machine name — useful for identifying systems on a network, especially in workplace environments.

### What Version of Windows Is This?

```cmd
systeminfo
```
Prints extensive system detail. Focus on:

| Field | What It Tells You |
|---|---|
| **OS Name** | Which Windows edition is installed |
| **OS Version** | Specific build/version number |
| **System Type** | 32-bit vs. 64-bit architecture |

> [!note] Don't Get Overwhelmed
> `systeminfo` returns a lot of output — you're not expected to understand every field right away. Focus on the three above for now.

### How Is This Machine Connected to the Network?

```cmd
ipconfig
```
Shows network configuration. Focus on:

| Field | What It Tells You |
|---|---|
| **IPv4 Address** | The machine's local network address |
| **Default Gateway** | The router/gateway the machine routes traffic through |

> [!question]- 🧪 Quick Quiz: System & Network Information
> 1. Why does it matter which user account (`whoami`) you're logged in as?
> 2. What does `hostname` show, and why is it useful in a workplace?
> 3. Which three fields should you focus on in `systeminfo` output as a beginner?
> 4. What does `ipconfig` show, and which two fields matter most for basic troubleshooting?
> 5. What does the "System Type" field in `systeminfo` actually tell you?
>
> **Answers**
> 1. Different users have different permissions — knowing your identity tells you what you're allowed to do on the system.
> 2. The machine's short network name — useful for identifying specific systems on a network.
> 3. OS Name, OS Version, System Type.
> 4. Network configuration; the most important fields are IPv4 Address and Default Gateway.
> 5. Whether the system is running a 32-bit or 64-bit version of Windows.

---

## 🧠 Key Takeaways — Command Cheat Sheet

| Command | Purpose | Linux Equivalent |
|---|---|---|
| `cd` (no args) | Show current directory | `pwd` |
| `dir` | List directory contents | `ls` |
| `dir /a` | List contents including hidden items | `ls -al` |
| `cd <folder>` / `cd ..` | Move into a folder / up one level | `cd <folder>` / `cd ..` |
| `dir /s <filename>` | Search all subfolders for a file | `find <path> -name <file>` |
| `type <filename>` | Print a file's contents | `cat <filename>` |
| `whoami` | Show current username | `whoami` |
| `hostname` | Show computer's network name | `hostname` |
| `systeminfo` | Show detailed OS/system info | `uname -a` |
| `ipconfig` | Show network configuration | `ip a` / `ifconfig` |

- Windows `cd` is dual-purpose (show *and* change directory) — a key syntax difference from Linux's separate `pwd`/`cd`.
- Hidden files on Windows work the same conceptually as Linux dotfiles — hidden by default, not protected.
- `dir /s` and Linux's `find` solve the same problem (locate a file by name across subfolders) with different syntax.
- `systeminfo` and `ipconfig` are your first stops for OS and network diagnostics on any unfamiliar Windows machine.

## 📝 Full Module Recap Quiz
> [!question]- End-to-End Review (test yourself without peeking at the sections above)
> 1. Write the full command sequence to: check your current directory, list all contents including hidden ones, move into a folder called `Reports`, and move back up.
> 2. Write the command to search your whole current directory tree for a file named `contract.pdf`.
> 3. What's the Windows command to read a file's contents in the terminal, and what's its direct Linux equivalent?
> 4. Name the four commands used to gather system/user/network info in this room, and what each reveals.
> 5. Which three fields from `systeminfo` should a beginner focus on?
> 6. Which two fields from `ipconfig` matter most, and what does each represent?

## 🔗 Related Notes
- [[Linux CLI Basics]]
- [[Windows Basics]]
- [[What is an Operating System]]
- [[Inside a Computer System]]
- [[Operating Systems MOC]]

## 📌 Next Steps
- [ ] Practice these commands on a real or virtual Windows machine
- [ ] Build a personal side-by-side cheat sheet comparing Windows CMD vs. Linux Bash commands
- [ ] Revisit quiz sections and rebuild the command cheat sheet from memory for spaced repetition
