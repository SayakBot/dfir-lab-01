# 🔍 DFIR Lab #001 — Investigating a Malware-Infected Windows VM

> A beginner-level Digital Forensics & Incident Response lab write-up. I set up a deliberately infected Windows 10 VM and investigated what the malware did — step by step, with every command included.

---

## 📖 Read the Full Write-up

👉 **[View the Blog Post](https://SayakBot.github.io/dfir-lab-01/dfir-malware-investigation-blog.html)**  
*(Deploy this repo with GitHub Pages to make this link live)*

---

## 🧪 Lab Overview

| Detail | Info |
|---|---|
| **Difficulty** | Beginner |
| **Environment** | Windows 10 VM (VirtualBox + FlareVM) |
| **Malware Type** | Emotet (controlled sample from MalwareBazaar) |
| **Time Taken** | ~4 hours across 2 sessions |
| **Key Techniques** | Live triage, memory forensics, disk artifact analysis, timeline reconstruction |

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| VirtualBox + FlareVM | Isolated analysis environment |
| FTK Imager | RAM acquisition |
| Volatility 3 | Memory forensics (pslist, malfind, netstat) |
| Autoruns (Sysinternals) | Persistence mechanism detection |
| Sysmon | Detailed process/network event logging |
| Eric Zimmerman Tools | Prefetch parsing (PECmd), Registry Explorer |

---

## 📋 Investigation Steps

1. **Environment Setup** — Isolated Windows 10 VM with host-only networking and clean baseline snapshot
2. **Live Triage** — Running processes, active network connections, persistence via Autoruns
3. **Memory Forensics** — RAM dump with FTK Imager, analysis with Volatility 3 (malfind revealed process hollowing)
4. **Disk Artifacts** — Windows Event Logs, Sysmon logs, Prefetch files, Registry investigation, static binary analysis
5. **Timeline Reconstruction** — Cross-referenced all evidence sources into a coherent attack timeline
6. **Lessons Learned** — Documented mistakes and improvements for future investigations

---

## 🚨 Key Findings

- **Fake svchost.exe** running from `AppData\Local\Temp` (masquerading as legitimate Windows process)
- **Registry persistence** under `HKCU\...\Run\WindowsUpdate`
- **Process hollowing** into `explorer.exe` (PID 3412) detected by Volatility's `malfind` plugin
- **C2 beaconing** — outbound connection attempts to 3 external IPs on ports 443/8080
- **UPX-packed binary** — compressed to evade static antivirus detection

---

## ⚠️ Disclaimer

All malware samples used in this lab were obtained from controlled research repositories (MalwareBazaar) and executed **only** inside an isolated virtual machine with no internet access. This lab is for **educational purposes only**.

---

## 📂 Repo Structure

```
dfir-lab-01/
├── dfir-malware-investigation-blog.html   # Full write-up (GitHub Pages)
├── README.md                              # This file
└── notes/
    └── iocs.md                            # Indicators of Compromise collected
```

---

## 🚀 Deploy on GitHub Pages

1. Fork or clone this repo
2. Go to **Settings → Pages**
3. Set source to `main` branch, root `/`
4. Your blog will be live at `https://YOUR-USERNAME.github.io/dfir-lab-01/`

---

*This is Lab #001 in an ongoing series of personal DFIR projects. Still learning — feedback always welcome.*
