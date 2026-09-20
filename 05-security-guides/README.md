# 🚨 Incident Response Quick Guide

## Overview

This quick guide provides a structured response for the **first 30 minutes of a suspected cybersecurity incident**.

The goal is to help a responder act quickly while avoiding actions that could destroy evidence, interfere with an investigation, or make the incident more difficult to understand.

The guide focuses on four priorities:

- Document what happened
- Notify the appropriate personnel
- Limit further damage when authorized
- Preserve evidence for investigation

> **Important:** Do not delete files, shut down systems, or run commands that modify evidence unless the organization's incident-response procedure specifically directs you to do so.

---

# ⏱️ First 30 Minutes

| # | Action |
| --- | --- |
| 1 | **Record the discovery time.** Write down when the suspicious activity was first noticed or reported. |
| 2 | **Document what you observe.** Record error messages, unusual behavior, alerts, filenames, IP addresses, usernames, or other visible indicators. |
| 3 | **Notify the appropriate person or security team.** Follow the organization's incident-reporting procedure and provide the information collected so far. |
| 4 | **Do not shut down or restart the affected system.** Important volatile evidence may exist in memory or active network connections. |
| 5 | **Isolate the system only if authorized.** If instructed by the incident-response procedure, disconnect the affected device from the network without unnecessarily modifying the system. |
| 6 | **Record system information.** Document the hostname, logged-in user, IP address, device location, and other identifying information. |
| 7 | **Review active processes and logged-in users.** Identify unusual processes or unexpected user sessions without terminating them unless authorized. |
| 8 | **Review network activity.** Record active connections and listening ports that may help identify suspicious communication. |
| 9 | **Preserve available evidence.** Protect logs, screenshots, alerts, and other relevant information from accidental modification or deletion. |
| 10 | **Maintain an action log.** Record what was done, when it was done, and who performed each action throughout the response. |

---

# ❌ What NOT to Do

During an incident, rushed actions can destroy evidence or make an investigation more difficult.

## 1. Do Not Immediately Shut Down or Restart the Computer

Shutting down or restarting a system can destroy **volatile information** stored in memory.

This may include:

- Running processes
- Active user sessions
- Network connections
- Temporary system information

Preserving this information may help investigators understand what occurred.

---

## 2. Do Not Delete Suspicious Files

A suspicious file may be important evidence.

Deleting it could prevent investigators from determining:

- What the file contained
- How it entered the system
- When it was created
- Whether it executed
- What other systems or files it interacted with

Suspicious files should be preserved and handled according to the organization's incident-response procedures.

---

## 3. Do Not Change or Reset Passwords Without Authorization

Changing credentials immediately may interfere with the investigation.

It can:

- Change system evidence
- Disrupt active monitoring
- Affect account access
- Alert an attacker that suspicious activity has been discovered

Credential changes should be coordinated with the authorized incident-response team.

---

## 4. Do Not Randomly Run Cleanup or Antivirus Tools

Running cleanup tools without a response plan can modify or remove evidence before it has been properly collected.

Security tools may:

- Delete suspicious files
- Quarantine evidence
- Modify timestamps
- Terminate processes
- Change system information

Evidence preservation should be considered before remediation begins.

---

# 💻 Useful Commands

Commands used during incident response should be selected carefully.

The following commands can help collect basic system information without intentionally removing files or cleaning the system.

## Windows

### View Network Connections

    netstat -ano

This can display:

- Active network connections
- Listening ports
- Protocols
- Process IDs (PIDs)

### View Running Processes

    tasklist

This displays processes currently running on the Windows system.

### View Logged-In Users

    query user

This can help identify active user sessions.

---

## Linux

### View Network Connections and Listening Ports

    ss -tulpen

This can display network sockets, listening services, and related process information.

### View Running Processes

    ps aux

This displays running processes and associated users.

---

# 🔬 Evidence Collection Priority

Some digital evidence is more temporary than other evidence.

During an investigation, evidence that can disappear quickly should generally receive priority.

A practical collection order is:

1. **RAM / Volatile Memory**
2. **Running Processes and Logged-In Users**
3. **Active Network Connections**
4. **Network Configuration**
5. **Temporary System Information**
6. **Files and Storage**
7. **System and Application Logs**

This helps preserve information that may otherwise disappear if the system is powered off, restarted, or significantly modified.

---

# 🧾 Documentation During an Incident

Good documentation is essential during incident response.

Record information such as:

- Date and time of discovery
- Person who discovered the incident
- Affected system or device
- Hostname
- IP address
- Logged-in user
- Visible alerts or error messages
- Suspicious processes
- Active network connections
- Actions performed
- Time each action was performed
- Person responsible for each action
- People or teams notified

Documentation can help establish an accurate timeline of the incident.

---

# 🔐 Evidence Preservation

Digital evidence should be protected from unnecessary modification.

Important practices include:

- Avoid deleting suspicious files.
- Avoid unnecessary system changes.
- Record actions taken during the response.
- Preserve relevant logs.
- Capture important observations.
- Follow authorized evidence-handling procedures.
- Maintain clear documentation of evidence collection and handling.

The goal is to preserve the integrity of the evidence so that it remains useful during further investigation.

---

# 🛡️ Incident Response Priorities

A responder should focus on:

**Identify → Document → Report → Preserve → Contain When Authorized → Investigate → Recover**

Containment and recovery actions should follow established procedures so that the need to protect systems is balanced with the need to preserve evidence.

---

# ⚠️ Example Scenario

A user reports that their computer is behaving unusually and unknown network connections are visible.

Instead of immediately restarting the computer or deleting suspicious files, the responder should first:

1. Record when the issue was reported.
2. Document the symptoms.
3. Record system and user information.
4. Review active processes and network connections.
5. Notify the appropriate security personnel.
6. Preserve relevant evidence.
7. Follow authorized containment procedures.

This approach provides investigators with more information than immediately attempting to clean the affected system.

---

# 🧠 Security Principles Demonstrated

## Evidence Preservation

Incident response must consider how responder actions can affect digital evidence.

## Chain of Custody Awareness

Actions involving evidence should be documented so that investigators can understand who handled the evidence and what was done.

## Least Privilege

Only authorized personnel should perform sensitive containment, remediation, or evidence-handling actions.

## Defense in Depth

Incident response works alongside preventive and detective controls such as:

- Firewalls
- Security updates
- Access controls
- Authentication
- Logging
- Monitoring
- Endpoint protection

---

# 🧰 Skills Demonstrated

- Incident Response
- Digital Evidence Preservation
- Incident Documentation
- Windows Command Line
- Linux Command Line
- Network Connection Analysis
- Process Analysis
- User Session Review
- Evidence Prioritization
- Chain of Custody Awareness
- Security Monitoring
- Incident Containment Awareness
- Technical Documentation
- Cybersecurity Best Practices

---

# 📁 Related Portfolio Work

This guide connects with other projects in my cybersecurity portfolio, including:

- Virtual Cybersecurity Home Lab
- Windows & Linux System Hardening
- Firewall Rules & Network Defense Audit
- Linux Hardening Checklist
- Account Security Checklist
- SSH Authentication Log Investigation

Together, these projects demonstrate a progression from **system configuration and prevention** to **monitoring, incident response, and investigation**.

---

# Conclusion

This quick guide demonstrates a structured approach to the early stages of cybersecurity incident response.

The most important lesson is that responding to an incident does not mean immediately trying to fix everything. A responder must first document what is happening, preserve important evidence, notify the appropriate personnel, and avoid unnecessary actions that could interfere with an investigation.

A careful first response can significantly improve the quality of the investigation and support more effective containment and recovery.
