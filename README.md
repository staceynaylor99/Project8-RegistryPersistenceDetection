Registry Persistence Detection (Project 8)

This project demonstrates how Sysmon detects registry-based persistence using Event ID 13.
Attackers often modify Registry Run Keys to make malware start automatically when a user logs in.

Objectives

Simulate registry persistence using a fake updater executable

Capture Sysmon Event ID 13 logs

Analyze the event fields that reveal persistence behavior

Document findings in SOC-style format

What I Did

Used PowerShell to create a Registry Run Key under:
HKCU\Software\Microsoft\Windows\CurrentVersion\Run

Set it to point to a fake executable name (StartupNotFakeUpdater)

Triggered Sysmon logging for registry modifications

Located Event ID 13 inside the Sysmon Operational log

Captured and documented the event details

Key Findings

Sysmon successfully captured:

Event ID 13 — Registry Value Set

Image: The process that created the key (svchost.exe or powershell.exe)

TargetObject: The exact registry path modified

Details: Value written to the Run key

User: Account responsible

ProcessGuid: Tracks related process activity

These fields reveal persistence attempts clearly and provide defenders visibility into suspicious registry activity.

Why This Matters

Attackers use registry Run keys to:

Launch malware at startup

Maintain long-term access

Hide persistence inside legitimate Windows mechanisms

Detecting Event ID 13 gives SOC analysts early warning of persistence mechanisms used in real intrusions.

Files Included

DetectionNotes.md — Detailed analysis

/screenshots/event13-registry-persistence.png — Recorded Sysmon event

Skills Demonstrated

Registry persistence detection

Sysmon log analysis

Threat behavior interpretation

SOC-style documentation
