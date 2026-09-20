# 🛡️ Windows & Linux System Hardening

## Overview

This project documents security-hardening activities I completed across my Windows and Ubuntu virtual lab environments.

The work combines practical exercises from:

- **Assignment #3** — System Patching and Updates
- **Assignment #4** — Principle of Least Privilege
- **Assignment #6** — Linux Security Hardening
- **Assignment #14** — Firewall Rules and Network Defense

The goal was to apply multiple layers of security rather than relying on a single security control.

---

## 🧪 Lab Environment

| System | Environment | Security Activities |
| --- | --- | --- |
| WindowsLab | Windows virtual machine | Patching, user-account security, least privilege, firewall auditing |
| UbuntuLab | Ubuntu Linux virtual machine | Privilege auditing, permissions, SSH review, firewall configuration, patch review |

Both systems are hosted in **Oracle VirtualBox** as part of my cybersecurity home lab.

---

# Windows & Linux Hardening Steps

## 1. System Patching and Updates

**Source: Assignment #3**

One of the first steps in securing a system is ensuring that the operating system and installed software are kept updated.

Patching helps address known vulnerabilities, software bugs, and security weaknesses that could otherwise be exploited.

### Hardening Practice

Systems should be regularly checked for:

- Operating-system updates
- Security patches
- Application updates
- Driver or component updates where appropriate
- Failed or pending updates

### Why It Matters

Attackers frequently take advantage of known vulnerabilities for which patches already exist.

Keeping systems updated reduces exposure to known security weaknesses and forms an important part of vulnerability management.

---

## 2. Principle of Least Privilege

**Source: Assignment #4**

I practiced the **Principle of Least Privilege** by creating a Windows Standard User account named:

`Daily_User`

A standard account has fewer privileges than an administrator account and is therefore more appropriate for normal day-to-day activity.

📸 **Windows Standard User screenshot will be added here.**

### Security Benefit

Using a standard account for normal activity can reduce the impact of:

- Accidental system changes
- Unauthorized software installation
- Malicious programs attempting to make administrative changes
- Users modifying security-sensitive settings unnecessarily

Administrative privileges should only be used when they are actually required.

---

## 3. Linux Privileged Account Review

**Source: Assignment #6**

I checked the Ubuntu system for accounts with UID 0 using:

    awk -F: '$3 == 0 {print $1}' /etc/passwd

Only the `root` account was identified.

UID 0 provides root-level privileges, so unexpected UID 0 accounts could indicate excessive or unauthorized administrative access.

### Hardening Recommendation

Regularly review privileged accounts and remove unnecessary administrative access.

**Result:** ✅ No additional UID 0 accounts were identified.

---

## 4. Linux File Permission Review

**Source: Assignment #6**

I reviewed Linux file permissions as part of the hardening process.

I searched for files configured with `777` permissions using:

    find / -type f -perm 777 2>/dev/null

No files with `777` permissions were identified during the audit.

I also reviewed the permissions assigned to `/etc/shadow`.

The recorded permissions were:

    -rw-r-----

The file was not world-readable.

### Security Benefit

Restricting file permissions helps prevent unauthorized users from reading or modifying sensitive information.

The `/etc/shadow` file requires particularly strong protection because it contains sensitive password information.

---

## 5. Administrative Access Review

**Source: Assignment #6**

I reviewed membership in the Linux `sudo` group using:

    getent group sudo

Several accounts were listed with administrative privileges.

### Hardening Recommendation

Sudo access should be limited to users who genuinely require administrative privileges.

Administrative-group membership should also be reviewed periodically to ensure unnecessary access is removed.

This supports the **Principle of Least Privilege**.

---

## 6. Remote Access and SSH Review

**Source: Assignment #6**

I attempted to review the SSH root-login configuration using:

    grep "^PermitRootLogin" /etc/ssh/sshd_config

The SSH configuration file was not present because **OpenSSH Server was not installed** on the Ubuntu system.

Therefore, SSH was not enabled in this lab configuration.

### Security Lesson

A security audit should document the system as it actually exists.

I did not install or enable SSH simply to produce a different audit result. Instead, I documented the existing configuration and its security implications.

If SSH is enabled in the future, its configuration should be reviewed and remote root access should be appropriately restricted.

---

## 7. Ubuntu Firewall Hardening

**Sources: Assignments #6 and #14**

During my initial Linux security audit in **Assignment #6**, I checked UFW using:

    sudo ufw status

The firewall was initially reported as:

    Status: inactive

This was identified as an area for improvement.

During my later firewall exercise in **Assignment #14**, UFW was active.

The later configuration showed:

- **Status:** Active
- **Logging:** On (low)
- **Default incoming policy:** Deny
- **Default outgoing policy:** Allow
- **Routed traffic:** Disabled

📸 **Active UFW firewall screenshot will be added here.**

### Security Improvement

The change from an inactive firewall during the initial audit to an active firewall with a default-deny incoming policy demonstrates the progression of my lab's security configuration.

A default-deny incoming policy reduces unnecessary network exposure by blocking unsolicited inbound traffic unless it is specifically permitted.

---

## 8. Windows Firewall Review

**Source: Assignment #14**

I reviewed Windows Defender Firewall rules using PowerShell.

The audit included both inbound and outbound rules across different network profiles.

Examples of rules reviewed included:

- Wi-Fi Direct Spooler Use (Out)
- Network Discovery SSDP-Out
- Network Discovery WSD Events-Out
- Wi-Fi Direct Spooler Use (In)
- Remote Assistance TCP-Out
- Core Networking Packet Too Big ICMPv6-Out

📸 **Windows firewall PowerShell screenshot will be added here.**

### Security Finding

One rule reviewed, **Wi-Fi Direct Spooler Use (In)**, allowed inbound traffic on the **Public** profile.

Because public networks are less trusted, inbound rules on the Public profile should be reviewed carefully.

### Hardening Recommendation

If the service is not required, the rule should be disabled or restricted according to operational requirements.

Firewall rules should follow the Principle of Least Privilege by allowing only the traffic required for legitimate system functions.

---

## 🌐 Network Defense Context

Firewall hardening is only one part of network defense.

For example, vulnerabilities involving services such as **SMB on TCP port 445** demonstrate why unnecessary network exposure should be reduced.

However, a firewall should not be treated as the only security control.

Effective protection also requires:

- Security patching
- Secure system configuration
- Access control
- Account security
- Monitoring
- Vulnerability management

This represents a **Defense in Depth** approach.

---

## 🔐 Security Principles Demonstrated

### Principle of Least Privilege

Users, applications, and network services should receive only the access required to perform their legitimate functions.

I applied this concept through:

- Windows Standard User accounts
- Linux privileged-account reviews
- Sudo membership reviews
- Firewall-rule analysis

### Defense in Depth

Multiple security controls should work together rather than relying on one defensive measure.

This project combines:

- Patching
- Account controls
- File permissions
- Administrative-access reviews
- Firewall protection
- Secure configuration
- System auditing

---

## 📊 Hardening Progression

| Area | Initial Finding | Hardening Approach |
| --- | --- | --- |
| System Updates | Updates require regular review | Maintain patching and update checks |
| Windows User Access | Administrative privileges should be limited | Use a Standard User for daily activity |
| Linux UID 0 Accounts | Only root identified | Continue privileged-account monitoring |
| Linux File Permissions | No 777 files identified; `/etc/shadow` restricted | Maintain secure permissions |
| Sudo Access | Several sudo members identified | Periodically review administrative access |
| SSH | OpenSSH Server not installed | Review configuration if SSH is enabled later |
| Ubuntu Firewall | Initially inactive | Later active with default-deny incoming policy |
| Windows Firewall | Existing rules reviewed | Investigate and restrict unnecessary exposure |

---

## 🧰 Skills Demonstrated

- Windows System Hardening
- Linux System Hardening
- Patch Management
- Windows User Administration
- Principle of Least Privilege
- Linux Privilege Auditing
- File Permission Analysis
- Sudo Access Review
- SSH Security Review
- Windows Defender Firewall
- Ubuntu UFW
- PowerShell
- Linux Command Line
- Firewall Rule Analysis
- Network Defense
- Defense in Depth
- Security Auditing
- Security Documentation

---

## 📁 Related Portfolio Projects

This hardening project is supported by additional work elsewhere in this repository, including:

- Virtual Cybersecurity Home Lab
- Linux Hardening Checklist
- Account Security Checklist
- Firewall Rules & Network Defense Audit
- Incident Response Quick Guide
- SSH Authentication Log Investigation

Together, these projects demonstrate the progression from basic system administration into practical cybersecurity auditing and defensive security.

---

## Conclusion

This project demonstrates how I applied security-hardening concepts across both Windows and Linux environments.

Rather than relying on one security control, I used patching, account restrictions, permission reviews, administrative-access auditing, firewall configuration, and security analysis to strengthen the systems.

The exercises also helped me understand that hardening is an ongoing process. Systems should be regularly reviewed as configurations, software, users, and security requirements change.
