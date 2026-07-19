---
title: Windows Basics
source: https://tryhackme.com/room/windowsbasics
platform: TryHackMe
module: Operating Systems
difficulty: Easy
duration: 45 min
tags: [cybersecurity, tryhackme, windows, gui, file-explorer, task-manager, windows-security, beginner]
status: in-progress
---

# 🪟 Windows Basics

> [!info] Room Info
> **Difficulty:** Easy · **Time:** ~45 min · **Module:** Operating Systems
> Goal: Navigate the Windows GUI, manage files, personalize settings, and use core system/security tools (Task Manager, Windows Security, Defender Firewall).

---

## 1. Introduction

Every OS has its own "personality" — this room puts the concepts from [[What is an Operating System|What is an Operating System?]] into practice on **Microsoft Windows**, the most familiar OS for most people.

> [!quote] Scenario
> You're a new employee at fictional company **TryHatMe**. On your first day, you log into your workstation, learn the Windows desktop, open tools from the Start menu, navigate company folders, adjust settings, check Task Manager, and review basic security.

### Learning Objectives
- Navigate the Windows GUI: desktop, taskbar, Start menu
- Use File Explorer to browse folders, understand file paths, organize files
- Check system settings and personalize the environment via the Settings app
- Use basic system tools — **Task Manager** and **Windows Security** — to monitor performance and verify protection

### Prerequisites
- [[Inside a Computer System]]
- [[Computer Types]]
- [[What is an Operating System]]

---

## 2. Exploring the Windows Workspace

### A Brief History
Early computers ran **MS-DOS** — a black screen where you typed commands, no icons. In 1985, **Windows 1.0** introduced a basic GUI on top of DOS: windows, menus, mouse controls. Windows has been building on that foundation ever since, evolving from a simple "shell" into a full OS.

### Logging In and Authentication

Before reaching the desktop, you must **authenticate** — this verifies identity and determines what you're allowed to do afterward.

| Account Type | Permissions |
|---|---|
| **Guest** | Restricted, temporary access; minimal permissions, no system setting changes |
| **Standard** | Everyday tasks — run apps, change personal settings; no system-wide changes |
| **Administrator** | Full control — software installs, configuration changes, user management |

> [!tip] Airport Analogy Continues
> Login screen = **airport security checkpoint**. Desktop = the **airport terminal** — the first area you access after clearing security, with everything else branching out from there.

### The Windows Desktop — Core Areas

| Area | Purpose |
|---|---|
| **Desktop** | Main workspace — files, folders, shortcuts live here |
| **Taskbar** | Control strip — access to apps, system tools, settings, notifications |

**Taskbar/Desktop components:**

| # | Component | Function |
|---|---|---|
| 1 | Desktop icons | Shortcuts (Recycle Bin, folders, frequently used apps) — customizable |
| 2 | Start menu | Primary access to apps, settings, power options (log out/restart/power off) |
| 3 | Search | Find apps, files, folders, settings by keyword |
| 4 | Task View | See all open windows, switch between them |
| 5 | Pinned apps/folders | Quick access to most-used items |
| 6 | Network & audio settings | Customizable |
| 7 | Date & Time | Full calendar + settings access |
| 8 | Notifications | App/system notifications, quick settings access |

> [!tip] Start Menu Analogy
> If the Desktop = airport terminal, the **Start menu** = the departure board / information desk — everything available (apps, files, folders, settings, power options) at a glance.

### Built-in Tools and Apps
Windows ships with tools like **Notepad** (text editing) and **File Explorer** (file management) — available immediately via Start menu/search. Analogy: these are the **airport's amenities/services** — already there to help you get things done.

### Getting System Information
The **Settings app** includes an **"About your PC"** section — an overview of security, device, and OS information. This is the go-to spot to understand what machine you're working with (device name, RAM, Windows version/edition, etc.).

### File Exploration and Management

Windows uses a **hierarchical folder structure** — folders can contain other folders/files, keeping things organized as systems grow. Common top-level locations: **Desktop, Documents, Downloads**.

> [!tip] File Explorer Analogy
> File Explorer = the **directory/floor map** of the airport terminal — helps you navigate between areas and locate what you need.

**Navigating a folder in File Explorer:**
1. Open the target folder
2. It opens in File Explorer
3. Options available for viewing, sharing, editing folders/files
4. Clicking the folder name shows the **full path** (e.g. `C:\Users\Administrator\Desktop\TryHatMe Onboarding`)
5. Folder contents are displayed
6. Built-in search lets you search within the folder

> [!question]- 🧪 Quick Quiz: Exploring the Windows Workspace
> 1. What did early Windows (1.0) add on top of MS-DOS?
> 2. Name the three main Windows account types and one thing each can/can't do.
> 3. In the airport analogy, what does the login screen represent, and what does the Desktop represent?
> 4. What's the difference between the Desktop and the Taskbar?
> 5. Where would you go to find your PC's installed RAM and Windows version?
> 6. What does clicking a folder's name in File Explorer reveal?
>
> **Answers**
> 1. A basic GUI — windows, menus, and mouse control on top of the DOS command-line environment.
> 2. Guest (minimal, temporary, no system changes), Standard (everyday tasks, no system-wide changes), Administrator (full control — installs, config, user management).
> 3. Login screen = airport security checkpoint; Desktop = the airport terminal, the first area reached after clearing security.
> 4. Desktop = the main workspace for files/folders/shortcuts; Taskbar = the control strip for accessing apps/tools/settings/notifications.
> 5. The **Settings app → About your PC** section.
> 6. The folder's full file path (e.g. `C:\Users\Administrator\Desktop\TryHatMe Onboarding`).

---

## 3. Configuring and Securing Windows

> [!tip] Airport Analogy: App Lifecycle
> **Updating** an app/OS ≈ changing flights or reserving a seat. **Installing** ≈ scheduling a new flight. **Removing** ≈ canceling a booking you no longer need.

### Updating

| Update Type | How It Works |
|---|---|
| **Windows Update** (built-in) | Keeps OS + native apps + security features current; accessed via Settings; can auto-install |
| **Built-in apps** | May update automatically in the background |
| **Third-party apps** | Often have their own update mechanism, or prompt on launch, or require manual download of a new installer |

### Installing Applications

| Method | Notes |
|---|---|
| **Microsoft Store** | Curated, safer option — **not available by default on Windows Server** |
| **From the Internet** | Download an installer (`.exe`/`.msi`) directly from a trusted vendor's site |

### Uninstalling Applications
Multiple removal paths: **Microsoft Store**, **Add or remove programs** (Settings), **Uninstall a program** (Control Panel), or an app's **own built-in uninstaller**.

### Two Ways to Configure Windows

| Tool | Description |
|---|---|
| **Windows Settings** | Modern, centralized location for system/device/personalization/security config |
| **Control Panel** | Legacy interface — still needed for certain older administrative tools |

### Task Manager

Real-time monitoring of what's happening on the system — running apps, background processes, CPU/memory usage.

| Tab | Shows |
|---|---|
| **Processes** | Running apps/background processes + resource usage |
| **Performance** | Graphs/stats for CPU, memory, network |
| **Users** | Currently logged-in users + resources used |
| **Details** | Technical view of running processes, including PIDs |
| **Services** | Windows services + running/stopped status |

### Native Windows Security

**Windows Security** — central dashboard for built-in protection, enabled by default:

| Section | Purpose |
|---|---|
| **Virus & threat protection** | Detects/removes malware via real-time protection + custom scans |
| **Firewall & network protection** | Controls inbound/outbound network traffic |
| **App & browser control** | Protects against unsafe apps, files, websites |
| **Device security** | Hardware-based protections |

**Running a custom scan (walkthrough):** Windows Security → Virus & Threat protection → Scan options → Custom scan → Scan now → select target folder.

### Windows Defender Firewall

Built-in firewall monitoring network connections, applying rules to allow/deny traffic. Operates across three **network profiles**:

| Profile | Used For |
|---|---|
| **Domain** | System connected to an organization's domain network |
| **Private** | Trusted networks — home, lab |
| **Public** | Untrusted networks — public Wi-Fi |

**Advanced settings** show: an overview of inbound/outbound/connection rules, a detailed per-rule view (name, group, profile, status, action), and the ability to create new rules or filter the current view.

> [!question]- 🧪 Quick Quiz: Configuring and Securing Windows
> 1. Map "installing," "updating," and "removing" an app to their airport-booking analogy equivalents.
> 2. Why might the Microsoft Store not be available on a Windows Server machine?
> 3. What's the key difference between Windows Settings and Control Panel?
> 4. Which Task Manager tab would you check to see a process's PID?
> 5. Name the four sections of Windows Security and what each protects against.
> 6. Which Windows Defender Firewall network profile would you use on public Wi-Fi, and why does that matter?
>
> **Answers**
> 1. Installing = scheduling a new flight; updating = changing flights/reserving a seat; removing = canceling a booking no longer needed.
> 2. Windows Server is built for server roles, not general consumer use, so it doesn't ship with the consumer-focused Microsoft Store by default.
> 3. Windows Settings is the modern, centralized configuration tool; Control Panel is the legacy interface still needed for certain older admin tasks.
> 4. **Details** tab.
> 5. Virus & threat protection (malware), Firewall & network protection (unauthorized network access), App & browser control (unsafe apps/files/sites), Device security (hardware-based protections).
> 6. **Public** — untrusted networks like public Wi-Fi need stricter default rules since you don't control or trust who else is on the network.

---

## 4. Conclusion

You navigated the Windows interface, examined system properties, learned application management (install/update/uninstall), worked with files/folders, and reviewed security tools — all through a hands-on "first day at TryHatMe" scenario using **Windows Server 2019**.

### Key Terminology Recap

| Term | Definition |
|---|---|
| **Desktop** | Main workspace for files, folders, shortcuts |
| **Taskbar** | Control strip for apps, tools, settings, notifications |
| **Start Menu** | Primary access to apps, settings, power options |
| **Search** | Quick access to apps/settings/files by keyword |
| **File Explorer** | Built-in tool to browse/manage/organize files and folders |
| **Windows Update** | Built-in tool keeping OS, native apps, and security features current |
| **Microsoft Store** | Native app for installing trusted applications |
| **Windows Settings** | Centralized modern configuration location |
| **Control Panel** | Legacy configuration interface |
| **Task Manager** | Real-time system monitoring tool |
| **Windows Security** | Central dashboard for built-in security tools |
| **Windows Defender Firewall** | Built-in firewall protecting against unauthorized network traffic |

### Further Learning
Next rooms in the module move into the **CLI** (command-line interface):
- [[Linux CLI Basics]]
- [[Windows CLI Basics]]

---

## 🧠 Key Takeaways
- Windows evolved from **MS-DOS** (text-only) → **Windows 1.0** (basic GUI) → today's full-featured OS.
- Account type determines what you can do: **Guest < Standard < Administrator**.
- Desktop = main workspace; Taskbar = control strip; Start Menu = quick-access hub for everything.
- App lifecycle = **Install → Update → Uninstall**, each with multiple methods (Store, direct download, Settings, Control Panel).
- **Task Manager** monitors real-time system activity across 5 tabs: Processes, Performance, Users, Details, Services.
- **Windows Security** = 4-part protection dashboard (Virus & threat, Firewall & network, App & browser, Device security).
- **Windows Defender Firewall** applies different rules depending on network profile: Domain, Private, Public.

## 📝 Full Module Recap Quiz
> [!question]- End-to-End Review (test yourself without peeking at the sections above)
> 1. Trace the evolution of Windows from MS-DOS to today in a couple of sentences.
> 2. Explain the airport analogy end-to-end: security checkpoint, terminal, departure board, floor map, airport amenities.
> 3. What are the three Windows account types, ranked by privilege, and what can each do?
> 4. List all three ways to install an application on Windows and all four ways to uninstall one.
> 5. Name all five Task Manager tabs and what each shows.
> 6. Name all four Windows Security sections and their focus areas.
> 7. What are the three Windows Defender Firewall network profiles, and when would you use each?

## 🔗 Related Notes
- [[What is an Operating System]]
- [[Inside a Computer System]]
- [[Computer Types]]
- [[Client-Server Basics]]
- [[Linux CLI Basics]]
- [[Windows CLI Basics]]
- [[Operating Systems MOC]]

## 📌 Next Steps
- [ ] On your own Windows machine, locate About your PC, Task Manager, and Windows Security to reinforce muscle memory
- [ ] Continue to Linux CLI Basics or Windows CLI Basics
- [ ] Revisit quiz sections for spaced repetition
