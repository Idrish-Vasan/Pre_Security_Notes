---
title: Introduction to Operating System Security
source: TryHackMe (Operating Systems module)
platform: TryHackMe
module: Operating Systems
tags: [cybersecurity, tryhackme, os-security, cia-triad, authentication, passwords, malware, beginner]
status: in-progress
---

# 🔐 Introduction to Operating System Security

> [!info] Room Info
> **Module:** Operating Systems
> Goal: Understand why OS security matters, the three pillars of security (Confidentiality, Integrity, Availability), and three common attack targets — weak authentication, weak file permissions, and malicious programs.

---

## 1. Introduction to Operating System Security

### Quick Recap: What Is an OS?

**Hardware** = every physical, touchable computer part — screen, keyboard, printer, USB storage, and the desktop board (which houses the **CPU** and **RAM**, and connects to storage like an HDD/SSD).

Hardware alone is useless without something to control it — that's the **Operating System (OS)**: the layer between hardware and the applications/programs you run (browsers, messaging apps, etc.). Apps never touch hardware directly — they run **on top of** the OS, which grants access according to specific rules.

> [!tip] Ties Back
> This is the same layered model from [[What is an Operating System]] — user → applications → OS → hardware. This room builds on that to focus specifically on **security**.

### OS Categories by Device Type

| Category | Examples |
|---|---|
| **Laptop/Desktop** | MS Windows 11, macOS |
| **Smartphone** | Android, iOS |
| **Server** | MS Windows Server 2022, IBM AIX, Oracle Solaris |
| **Personal + Server** | Linux |

### Why OS Security Matters — What's At Stake

**On a smartphone**, you likely store:
- Private conversations
- Private photos
- Personal/work email
- Saved passwords (browser or notes)
- E-banking apps

**On a laptop/computer**, you likely store:
- Confidential work/university files
- Private personal documents (ID/passport copies)
- Email programs (Outlook, Thunderbird)
- Saved passwords
- Digital camera/smartphone photo backups

> [!warning] The Core Risk
> You don't want someone you don't trust accessing this data — which is exactly why the OS itself needs to be secured, not just individual apps.

### The Three Pillars of Security (CIA Triad)

| Pillar | Definition |
|---|---|
| **Confidentiality** | Secret/private files and information are only available to intended persons |
| **Integrity** | No one can tamper with files — stored or in transit |
| **Availability** | Your system is available to use whenever you need it |

> [!question]- 🧪 Quick Quiz: Introduction to OS Security
> 1. What's the difference between hardware and an operating system?
> 2. Give one example each of an OS designed for: laptops/desktops, smartphones, servers, and both personal + server use.
> 3. Name three types of private data commonly stored on a smartphone.
> 4. Define Confidentiality, Integrity, and Availability in your own words.
> 5. Why can't applications run directly on hardware?
>
> **Answers**
> 1. Hardware is the physical, touchable components (CPU, RAM, screen, etc.); the OS is the software layer that controls hardware and lets applications use it according to rules.
> 2. Laptop/Desktop: Windows 11 or macOS. Smartphone: Android or iOS. Server: Windows Server 2022, IBM AIX, or Oracle Solaris. Personal + Server: Linux.
> 3. Any three of: private conversations, private photos, personal/work email, saved passwords, e-banking apps.
> 4. Confidentiality = only intended people can access private data; Integrity = data can't be tampered with (stored or in transit); Availability = the system/data is accessible whenever needed.
> 5. Applications require the OS to mediate access to hardware — they run on top of the OS, which grants access according to specific rules, rather than touching hardware directly.

---

## 2. Common Examples of OS Security Weaknesses

This room focuses on three weaknesses commonly targeted by malicious users:

1. **Authentication and Weak Passwords**
2. **Weak File Permissions**
3. **Malicious Programs**

### 1. Authentication and Weak Passwords

**Authentication** = verifying your identity to a local or remote system. Three main methods:

| Factor | Example |
|---|---|
| **Something you know** | Password, PIN |
| **Something you are** | Fingerprint (biometric) |
| **Something you have** | Phone receiving an SMS code |

> [!warning] Passwords Are the Most Attacked Factor
> Because passwords are the most common authentication method, they're also the most attacked. Common user mistakes:
> - Easy-to-guess passwords
> - Reusing the same password across sites
> - Using personal details (birthdate, pet's name) — attackers know this tendency and account for it

**Top 20 most common passwords** (from NCSC's list of 100,000 most common leaked passwords):

| Rank | Password |
|---|---|
| 1 | `123456` |
| 2 | `123456789` |
| 3 | `qwerty` |
| 4 | `password` |
| 5 | `111111` |
| 6 | `12345678` |
| 7 | `abc123` |
| 8 | `1234567` |
| 9 | `password1` |
| 10 | `12345` |
| 11 | `1234567890` |
| 12 | `123123` |
| 13 | `000000` |
| 14 | `iloveyou` |
| 15 | `1234` |
| 16 | `1q2w3e4r5t` |
| 17 | `qwertyuiop` |
| 18 | `123` |
| 19 | `monkey` |
| 20 | `dragon` |

> [!note] The Trap of "Complex-Looking" Passwords
> Patterns like `qwerty`, `qwertyuiop`, and `1q2w3e4r5t` *look* complex but are extremely predictable — they just follow the keyboard layout. Sequential numbers (`123`, `1234`, ... `1234567890`) and dictionary words (`password`, `iloveyou`, `monkey`, `dragon`) round out the rest.

> [!success] Takeaway
> If an attacker guesses the password to one account (email, social media), they gain access to your private data through it. **Use complex, unique passwords per account.**

### 2. Weak File Permissions

Core principle: **least privilege** — a file should only be accessible to those who actually need it.

> [!example] Everyday Analogy
> Planning a trip with friends/family? You'd share trip-related files with the group going — not publicly with everyone. That's least privilege in action: **"who can access what?"**

| Weak Permissions Attack... | How |
|---|---|
| **Confidentiality** | Unauthorized users can access files they shouldn't be able to read |
| **Integrity** | Unauthorized users can modify/edit files they shouldn't be able to change |

### 3. Malicious Programs

Depending on type, malware can attack **confidentiality, integrity, and/or availability**.

| Malware Type | What It Does | CIA Pillar Attacked |
|---|---|---|
| **Trojan horse** | Gives the attacker access to your system — they can read or modify files | Confidentiality & Integrity |
| **Ransomware** | Encrypts your files, making them unreadable without a decryption password; attacker demands payment ("ransom") to restore access | Availability |

> [!note] How Encryption Weaponizes Availability
> Ransomware doesn't necessarily steal or leak your data — it just makes it **inaccessible** to you by encrypting it. The attacker holds the decryption key hostage, directly attacking your **availability**.

> [!question]- 🧪 Quick Quiz: OS Security Weaknesses
> 1. Name the three authentication factor categories, with one example each.
> 2. Why are patterns like `qwerty` or `1q2w3e4r5t` considered weak passwords despite looking complex?
> 3. What is the "principle of least privilege" in one sentence?
> 4. How can weak file permissions attack both confidentiality and integrity?
> 5. What's the key difference between how a Trojan horse and ransomware attack a system?
> 6. Which CIA pillar does ransomware primarily target, and how?
>
> **Answers**
> 1. Something you know (password/PIN), something you are (fingerprint), something you have (phone receiving SMS code).
> 2. They follow predictable keyboard layout patterns rather than being genuinely random — attackers know these patterns and account for them.
> 3. Files/resources should only be accessible to those who actually need access to do their work/task.
> 4. Confidentiality — unauthorized access to files they shouldn't read; Integrity — unauthorized modification of files they shouldn't be able to change.
> 5. A Trojan horse gives the attacker direct access to read/modify files (confidentiality/integrity); ransomware encrypts files, blocking the legitimate user's own access (availability) without necessarily reading or leaking the data.
> 6. Availability — by encrypting files, it makes them inaccessible until a ransom is paid for the decryption key.

---

## 🧠 Key Takeaways
- The OS sits between hardware and applications — apps never touch hardware directly, only through the OS's rules.
- Security in this context always maps back to the **CIA Triad**: Confidentiality, Integrity, Availability.
- **Weak authentication** (especially predictable passwords) is one of the most exploited weaknesses — use unique, non-pattern-based passwords per account.
- **Weak file permissions** violate the principle of **least privilege**, exposing files to unauthorized reading (confidentiality) or editing (integrity).
- **Malicious programs** vary in target: Trojans compromise confidentiality/integrity by granting attacker access; ransomware attacks availability by encrypting files and holding decryption hostage.

## 📝 Full Module Recap Quiz
> [!question]- End-to-End Review (test yourself without peeking at the sections above)
> 1. Explain the hardware → OS → application layering and why it matters for security.
> 2. Define the CIA triad and give a real-world example of an attack on each pillar.
> 3. List the three authentication factors and one weakness of relying solely on "something you know."
> 4. Why do seemingly complex passwords like `qwertyuiop` still make the "most common passwords" list?
> 5. Explain the principle of least privilege using a non-technical example.
> 6. Compare how a Trojan horse and ransomware attack a system differently, in terms of the CIA triad.

## 🔗 Related Notes
- [[What is an Operating System]]
- [[Windows Basics]]
- [[Linux CLI Basics]]
- [[Windows CLI Basics]]
- [[Offensive Security Intro]]
- [[Operating Systems MOC]]

## 📌 Next Steps
- [ ] Audit your own passwords against the top-20 list above — change any matches immediately
- [ ] Check file/folder sharing permissions on a personal cloud drive (Google Drive, OneDrive) for anything over-shared
- [ ] Revisit quiz sections for spaced repetition
