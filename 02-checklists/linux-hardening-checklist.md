# 🐧 Linux Hardening Checklist

## Overview

This checklist documents a Linux security audit I performed on my Ubuntu virtual machine as part of my cybersecurity home lab.

The purpose of the audit was to review common Linux security areas including privileged accounts, file permissions, administrative access, account status, SSH configuration, firewall protection, SUID files, system updates, and password-expiration settings.

---

## ✅ Linux Security Checklist

| # | Security Check | Command | Finding |
| --- | --- | --- | --- |
| 1 | Check for unauthorized UID 0 accounts | `awk -F: '$3 == 0 {print $1}' /etc/passwd` | Only the `root` account was identified with UID 0. |
| 2 | Search for files with 777 permissions | `find / -type f -perm 777 2>/dev/null` | No files with 777 permissions were identified. |
| 3 | Review `/etc/shadow` permissions | `ls -l /etc/shadow` | Permissions were `-rw-r-----`; the file was not world-readable. |
| 4 | Review sudo-group membership | `getent group sudo` | Several accounts were listed with administrative access. |
| 5 | Review inactive or locked accounts | Account-status command | Local account status was reviewed using an equivalent command because the original `passwd -S -a` option was unsupported in the lab environment. |
| 6 | Review SSH root-login configuration | `grep "^PermitRootLogin" /etc/ssh/sshd_config` | The SSH configuration file was not present because OpenSSH Server was not installed. |
| 7 | Review firewall status | `sudo ufw status` | UFW was inactive during the initial audit. |
| 8 | Search for SUID files | `find / -perm -4000 -type f 2>/dev/null` | Several SUID files were identified and reviewed as expected system utilities. |
| 9 | Check for available updates | `sudo apt list --upgradable` | Several package updates were available. |
| 10 | Review password-expiration settings | `sudo chage -l teisha-gae` | Password-aging settings for the account were reviewed. |

---

## 1. Privileged Account Review

### Check

Identify accounts with a UID of `0`.

### Command

    awk -F: '$3 == 0 {print $1}' /etc/passwd

### Finding

Only the `root` account was returned.

### Security Significance

UID 0 provides root-level privileges in Linux. Unexpected accounts with UID 0 could indicate excessive privileges or unauthorized administrative access.

**Result:** ✅ No additional UID 0 accounts were identified.

---

## 2. World-Writable File Review

### Check

Search for files configured with `777` permissions.

### Command

    find / -type f -perm 777 2>/dev/null

### Finding

No files with `777` permissions were identified during the audit.

### Security Significance

Permissions of `777` allow all users to read, write, and execute a file. Excessive permissions can increase the risk of unauthorized modification.

**Result:** ✅ No 777-permission files were identified.

---

## 3. `/etc/shadow` Permission Review

### Check

Review the permissions assigned to `/etc/shadow`.

### Command

    ls -l /etc/shadow

### Finding

The permissions were:

    -rw-r-----

The file was not world-readable.

### Security Significance

`/etc/shadow` contains sensitive password information. Restricting access helps prevent unauthorized users from obtaining password hashes.

**Result:** ✅ Restricted permissions were present.

---

## 4. Administrative Access Review

### Check

Identify users with membership in the `sudo` group.

### Command

    getent group sudo

### Finding

Several accounts were listed as members of the sudo group.

### Security Significance

Members of the sudo group can perform administrative actions. This access should only be provided to users who require elevated privileges.

**Recommendation:** Regularly review sudo membership and remove unnecessary administrative access.

---

## 5. Local Account Status Review

### Check

Review local accounts for inactive or locked status.

The original checklist command was not supported in my Ubuntu environment, so I used an equivalent account-status command to complete the review.

### Security Significance

Unused, inactive, or unnecessary accounts can increase a system's attack surface. Account status should therefore be reviewed regularly.

**Recommendation:** Disable or remove unnecessary accounts according to organizational policy.

---

## 6. SSH Security Review

### Check

Review the SSH configuration for root-login settings.

### Command

    grep "^PermitRootLogin" /etc/ssh/sshd_config

### Finding

The SSH configuration file was not present because OpenSSH Server was not installed on the Ubuntu system.

### Security Significance

The result demonstrated that security auditing should document the system's actual configuration rather than changing the environment simply to obtain an expected result.

**Result:** SSH was not enabled in this lab configuration.

---

## 7. Firewall Review

### Check

Review the status of Ubuntu's Uncomplicated Firewall (UFW).

### Command

    sudo ufw status

### Finding

UFW was **inactive** during this initial security audit.

### Security Significance

A host-based firewall can help restrict unnecessary network traffic and reduce system exposure.

**Recommendation:** Enable and configure UFW where appropriate, allowing only required network traffic.

> **Note:** > **Note:** This finding represents the system during my initial Linux security audit. In a later firewall-hardening exercise, UFW was active with a default-deny incoming policy, demonstrating the progression of my lab configuration.

---

## 8. SUID File Review

### Check

Identify files with the SUID permission.

### Command

    find / -perm -4000 -type f 2>/dev/null

### Finding

Several SUID files were identified. The files reviewed were expected system utilities requiring elevated privileges for specific functions.

### Security Significance

SUID files execute with the privileges of the file owner. Unexpected or unnecessary SUID files can create security risks and should be investigated.

**Recommendation:** Periodically review SUID files for unexpected changes.

---

## 9. System Update Review

### Check

Identify available package updates.

### Command

    sudo apt list --upgradable

### Finding

Several package updates were available.

### Security Significance

Keeping software updated is an important part of vulnerability management because updates can contain security patches for known weaknesses.

**Recommendation:** Apply approved security updates and patches regularly.

---

## 10. Password-Expiration Review

### Check

Review password-aging information for the user account.

### Command

    sudo chage -l teisha-gae

### Finding

The password-aging configuration for the account was reviewed.

### Security Significance

Password-aging settings allow administrators to review and manage password-expiration requirements for local accounts.

**Recommendation:** Configure password policies according to the security requirements of the organization or environment.

---

## 🔐 Security Principles Demonstrated

This Linux hardening exercise demonstrates several important cybersecurity principles:

- **Least Privilege** — Administrative access should be limited to users who require it.
- **Secure Permissions** — Sensitive files should not be accessible to unauthorized users.
- **Attack Surface Reduction** — Unnecessary services, accounts, and privileges should be minimized.
- **Defense in Depth** — Firewalls, access controls, patching, and account security work together to protect a system.
- **Patch Management** — Systems should be reviewed regularly for security updates.
- **Security Auditing** — System configurations should be checked and documented rather than assumed to be secure.

---

## 📁 Supporting Evidence

Screenshots from this Linux audit are also demonstrated in the **Virtual Cybersecurity Home Lab** project in this repository.

Evidence includes:

- UID 0 account review
- `/etc/shadow` permission review
- Sudo-group review
- SSH configuration review
- UFW firewall-status review
- Ubuntu package-update review

---

## 🧰 Skills Demonstrated

- Linux Administration
- Linux Command Line
- System Hardening
- User and Privilege Auditing
- File Permission Analysis
- Sudo Access Review
- SSH Security Review
- UFW Firewall Auditing
- SUID Analysis
- Patch Management
- Password Policy Review
- Principle of Least Privilege
- Defense in Depth

---

## Conclusion

Completing this checklist gave me practical experience reviewing the security configuration of an Ubuntu system.

Instead of only identifying whether individual checks passed or failed, I examined why each configuration matters and documented recommendations where improvements were needed.

This exercise strengthened my understanding of Linux hardening, system administration, access control, patch management, and security auditing.
