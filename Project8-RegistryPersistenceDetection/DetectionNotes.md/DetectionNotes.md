Detection Notes – Registry Persistence via Run Key (Sysmon Event ID 13)
Overview

This project shows how attackers create persistence on a Windows machine by adding a value to the Run registry key. Anything placed in this Run location launches automatically every time the user logs in.
Sysmon Event ID 13 captures these registry modifications, allowing defenders to spot suspicious persistence early.

How I Triggered the Event

I simulated an attacker adding a program to the Run key.
To do this, I added a fake updater entry:

TNotFakeUpdater


This created a new Run key value under the current user’s registry hive.

Sysmon monitored this action and generated Event ID 13.

What Sysmon Captured (Event ID 13 – RegistryEvent)

Sysmon recorded the details of the registry modification, including:

Key Details

Event ID: 13

Action: A registry value was set

RuleName: T1060,RunKey (MITRE ATT&CK persistence mapping)

TargetObject:
The exact registry path where the Run key value was created

Value Name:
TNotFakeUpdater

Process Image:
C:\Windows\System32\lsass.exe (Windows system process applying the registry update)

User:
Shows which user account the modification came from

Timestamp:
Exact moment the persistence mechanism was added

Why This Matters in Cybersecurity

Run key persistence is one of the most common techniques used by malware and threat actors because:

It runs automatically on every login

It blends in with normal Windows behavior

It requires no special privileges

It is often used by RATs, droppers, and credential-stealing tools

Sysmon Event ID 13 gives defenders visibility into:

Unauthorized program persistence

Malware setting itself to run every boot

Privilege escalation attempts followed by persistence

Any unexpected modification to key registry paths

This type of log is important because it can reveal the first step of long-term compromise.

MITRE ATT&CK Mapping

T1060 – Registry Run Keys / Startup Folder
Attackers use Run keys to maintain persistence after a reboot or user logon.

Artifacts Included

event13-registry-persistence.png
Screenshot of Sysmon Event ID 13 showing the registry value modification

DetectionNotes.md
Full written analysis of what happened and why it matters

Summary

This test shows how Sysmon helps detect registry-based persistence attempts.
Even though this was a harmless simulation, the event structure is identical to how real attackers operate.
A SOC analyst would investigate this event immediately, because unexpected Run key modifications are often early signs of infection or privilege abuse.