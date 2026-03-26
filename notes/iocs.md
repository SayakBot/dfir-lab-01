# IoCs — Lab #001 Malware Investigation

> Indicators of Compromise collected during the investigation of a malware-infected Windows 10 VM.

---

## File IoCs

| Type | Value | Notes |
|---|---|---|
| File Path | `C:\Users\User\AppData\Local\Temp\svchost.exe` | Malicious binary masquerading as Windows svchost |
| File Hash (SHA-256) | `[REDACTED — replace with your actual hash]` | Hash of the collected malware sample |
| Packer | UPX | Binary was UPX-packed to evade AV |

---

## Registry IoCs

| Key | Value Name | Value Data |
|---|---|---|
| `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` | `WindowsUpdate` | Path to fake svchost.exe in Temp |

---

## Network IoCs

| Type | Value | Port | Notes |
|---|---|---|---|
| IP Address | [IP 1] | 443 | C2 beacon attempt (blocked — host-only network) |
| IP Address | [IP 2] | 8080 | C2 beacon attempt (blocked) |
| IP Address | [IP 3] | 443 | C2 beacon attempt (blocked) |

---

## Memory IoCs

| Type | Detail |
|---|---|
| Process Hollowing | `explorer.exe` PID 3412 — injected PE header found in executable memory region with no disk backing |
| Mutex | Unique mutex string extracted via `strings` on process memory dump |

---

## Behavior IoCs (MITRE ATT&CK Mapping)

| Behavior | ATT&CK Technique |
|---|---|
| Fake svchost in Temp | T1036.005 — Masquerading: Match Legitimate Name or Location |
| Registry Run Key persistence | T1547.001 — Boot or Logon Autostart: Registry Run Keys |
| Process Hollowing | T1055.012 — Process Injection: Process Hollowing |
| C2 Beaconing | T1071 — Application Layer Protocol |
| System Recon (systeminfo, net user) | T1082 — System Information Discovery |
