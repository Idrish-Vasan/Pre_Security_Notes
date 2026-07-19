---
title: Offensive Security Intro
source: https://tryhackme.com/room/offensivesecurityintro
platform: TryHackMe
difficulty: Easy
duration: 15 min
tags: [cybersecurity, tryhackme, offensive-security, pentesting, gobuster, enumeration, beginner]
status: in-progress
---
# 🎯 Offensive Security Intro

> [!info] Room Info
> **Difficulty:** Easy · **Time:** ~15 min · **Platform:** [[TryHackMe]]
> Goal: Hack a fake bank website (legally, in a safe lab) and get a taste of what an ethical hacker actually does.

---

## Task 1 — What is Offensive Security?

> [!quote]
> "To outsmart a hacker, you need to think like one."

**Offensive Security** = simulating a hacker's actions (breaking into systems, exploiting bugs, finding loopholes) to discover vulnerabilities *before* real attackers do — with the end goal of improving defenses.

This sits opposite **[[Defensive Security]]**, which focuses on detecting and responding to attacks rather than initiating them.

> [!question]- Knowledge Check
> **Q:** Which term describes simulating a hacker's actions to find vulnerabilities in a system?
> **A:** Offensive Security

---

## Task 2 — Hacking Your First Machine

> [!tip] Lab Environment
> This task deploys a live target: **FakeBank**, a deliberately vulnerable practice web app. Split-screen view shows the room content on the left, target machine on the right.

### The Scenario
Companies often have hidden **admin portals** for staff (e.g., a bank employee transferring funds between accounts). If these pages aren't properly secured/hidden, an attacker can discover and abuse them.

### Tool: Gobuster
**[Gobuster](https://github.com/OJ/gobuster)** is a command-line brute-forcing tool used for **directory/file enumeration** — it takes a wordlist and tries each entry as a URL path against a target, reporting which ones exist.

### Step-by-Step Walkthrough

**1. Open a terminal** on the lab machine (Terminal icon on the desktop).

**2. Brute-force hidden directories:**

```bash
gobuster -u http://fakebank.thm -w wordlist.txt dir
```

| Flag | Meaning |
|------|---------|
| `-u` | Target URL/domain to scan |
| `-w` | Wordlist file to iterate through |
| `dir` | Mode: directory/file brute-forcing |

**Sample output:**
```
=====================================================
Gobuster v2.0.1              OJ Reeves (@TheColonial)
=====================================================
[+] Mode         : dir
[+] Url/Domain   : http://fakebank.thm/
[+] Threads      : 10
[+] Wordlist     : wordlist.txt
[+] Status codes : 200,204,301,302,307,403
[+] Timeout      : 10s
=====================================================
/images (Status: 301)
/bank-transfer (Status: 200)
=====================================================
```

> [!success] Result
> Gobuster reveals a hidden page: **`/bank-transfer`** — an unsecured admin function for moving money between accounts.

**3. Exploit it:**
- Navigate to `http://fakebank.thm/bank-transfer` in the browser.
- Transfer **$2000** from account `2276` → your account `8881`.
- Refresh the account page to confirm the new balance.

> [!warning] Why This Matters
> This mirrors a real-world **broken access control / hidden endpoint** vulnerability — a page with no authentication that exposes sensitive financial functionality. Real pentesters find these and report them responsibly (see [[Responsible Disclosure]]).

---

## Task 3 — Careers in Cyber Security

### Getting Started
No secret formula — pick an area of security that interests you, practice hands-on regularly, and build the habit of learning consistently.

> [!example] Real Success Stories
> - Paul: construction worker → security engineer
> - Kassandra: music teacher → security professional
> - Brandon: used TryHackMe in school → first cyber job

### Offensive Security Career Paths

| Role | Description |
|------|-------------|
| **Penetration Tester** | Tests products/systems to find exploitable vulnerabilities |
| **Red Teamer** | Simulates a real adversary attacking the org; reports from an attacker's POV |
| **Security Engineer** | Designs, monitors, and maintains security controls/networks/systems |

See also: [[Cyber Security Careers]] (linked follow-up room)

---

## 🧠 Key Takeaways
- Offensive security = ethically thinking/acting like an attacker to find and fix flaws first.
- **Enumeration** (e.g., directory brute-forcing with Gobuster) is often the first real step of an attack/test — finding what's exposed before exploiting it.
- Hidden ≠ secure. Obscurity (an unlisted `/bank-transfer` page) is not a substitute for actual access control/authentication.
- Multiple career tracks exist in offensive security: pentesting, red teaming, security engineering.

## 🔗 Related Notes
- [[Gobuster]]
- [[Directory Enumeration]]
- [[Broken Access Control]]
- [[Defensive Security]]
- [[Cyber Security Careers]]

## 📌 Next Steps
- [ ] Continue to the next room in the path
- [ ] Try Gobuster against a personal lab target with a custom wordlist (e.g. SecLists)
- [ ] Read up on OWASP's Broken Access Control category
