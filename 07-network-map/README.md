# 🌐 Home Lab Network Map

## Overview

This project documents the network configuration of my **Oracle VirtualBox cybersecurity home lab**, which includes Windows and Ubuntu virtual machines used for networking, system administration, security hardening, firewall analysis, and cybersecurity practice.

The purpose of this network map is to demonstrate my understanding of:

- Virtual networking
- IPv4 addressing
- Subnet masks
- Default gateways
- NAT networking
- DNS resolution
- ARP
- Routing
- Network connectivity
- Listening ports
- Basic network reconnaissance

---

# 🧪 Lab Environment

My cybersecurity home lab includes:

| System | Platform | Network Mode |
| --- | --- | --- |
| WindowsLab | Windows VM | VirtualBox NAT |
| UbuntuLab | Ubuntu Linux VM | VirtualBox NAT |
| Host Computer | Windows | Physical host running Oracle VirtualBox |

Oracle VirtualBox provides virtual networking that allows the virtual machines to access external networks while remaining separated from the physical network environment.

---

# 🪟 WindowsLab Network Configuration

The Windows virtual machine was configured with the following IPv4 information:

| Setting | Value |
| --- | --- |
| IPv4 Address | `10.0.2.15` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `10.0.2.2` |
| Network Mode | NAT |

The default gateway was successfully reachable during connectivity testing.

### Gateway Test

    ping 10.0.2.2

A successful response confirmed connectivity between the Windows virtual machine and its VirtualBox NAT gateway.

---

# 🐧 UbuntuLab Network Configuration

The Ubuntu virtual machine used the `enp0s3` network interface.

The recorded configuration included:

| Setting | Value |
| --- | --- |
| Interface | `enp0s3` |
| Interface State | UP |
| IPv4 Address | `10.0.2.15/24` |
| Broadcast Address | `10.0.2.255` |
| Default Gateway | `10.0.2.2` |
| MAC Address | `08:00:27:3b:ce:e1` |
| Network Mode | NAT |

The routing table showed a default route through:

    10.0.2.2

with the Ubuntu system using:

    10.0.2.15

as its source IPv4 address.

---

# 🔄 Why Both VMs Can Show `10.0.2.15`

Both WindowsLab and UbuntuLab recorded the IPv4 address:

    10.0.2.15

This does not necessarily indicate an IP-address conflict in this lab.

With the VirtualBox NAT configuration used during these exercises, each virtual machine can operate within its own NAT context.

As a result, the same private IPv4 address can appear on separate virtual machines without the systems behaving as though they are two devices using the same address on one normal shared LAN.

This distinction is important when interpreting virtual network configurations.

---

# 🌍 VirtualBox NAT

NAT stands for **Network Address Translation**.

In this lab, VirtualBox NAT provides the virtual machines with network connectivity without directly placing them onto the same physical network as the host computer.

The virtual machines communicate through a VirtualBox-provided NAT environment.

A simplified traffic path is:

    Virtual Machine
          ↓
    VirtualBox NAT
          ↓
    Host Network Connection
          ↓
       Internet

This provides a useful environment for cybersecurity practice because networking concepts can be explored within virtual machines without requiring them to operate as ordinary devices directly attached to the physical LAN.

---

# 🗺️ Network Diagram

📸 **Home lab network map will be added here.**

> The final diagram will represent WindowsLab and UbuntuLab in their respective VirtualBox NAT contexts rather than depicting both `10.0.2.15` addresses on a single shared LAN.

---

# 🔎 ARP Analysis

On WindowsLab, I reviewed the ARP table to examine devices and network addresses known to the system.

The ARP review identified:

    7 devices

ARP helps systems associate IPv4 addresses with MAC addresses on the local network segment.

Reviewing the ARP table is useful for:

- Understanding local network communication
- Identifying neighboring network devices
- Troubleshooting connectivity
- Supporting network investigations

---

# 🧭 Routing Analysis

The Windows routing table included the VirtualBox gateway:

    10.0.2.2

The Ubuntu routing configuration also showed a default route through:

    10.0.2.2

Routing tables help determine where network traffic should be sent when communicating with local and remote networks.

Understanding routing is important for cybersecurity because unexpected routes can affect how traffic moves through a system.

---

# 🔍 DNS Resolution

I also tested DNS resolution during the networking exercises.

Examples of resolved addresses included:

| Domain | Recorded IPv4 Address |
| --- | --- |
| Google | `192.178.50.46` |
| Microsoft | `150.171.109.114` |

DNS converts human-readable domain names into IP addresses that computers can use for network communication.

DNS analysis can also support security investigations involving suspicious domains or network connections.

---

# 🚪 Listening Port Analysis

During the Windows networking review, I identified the following listening endpoint:

    0.0.0.0:445

The connection state was:

    LISTENING

and the recorded process ID was:

    PID 552

TCP port **445** is commonly associated with SMB network services.

A listening service increases the system's network attack surface, making it important to determine whether the service is necessary, patched, securely configured, and appropriately protected by firewall rules.

This finding connects directly with my Firewall Rules & Network Defense Audit.

---

# 🔥 Firewall Context

The networking exercises also included reviewing Windows firewall information.

Firewall controls are important because they help determine which network connections are allowed or blocked.

Network information such as:

- Listening ports
- Active services
- IP addresses
- Network profiles
- Firewall rules

should be evaluated together when assessing network exposure.

---

# 🛡️ Security Relevance

Understanding network configuration is an important cybersecurity skill because security investigations frequently involve identifying:

- Source and destination IP addresses
- Open or listening ports
- Default gateways
- DNS activity
- Network routes
- Active connections
- Network interfaces
- Firewall rules

These details can help analysts determine how systems communicate and where potential security exposure may exist.

---

# 🧰 Skills Demonstrated

- Oracle VirtualBox
- Virtual Networking
- NAT Networking
- IPv4 Addressing
- Subnetting Fundamentals
- Default Gateway Analysis
- Windows Networking
- Linux Networking
- DNS Resolution
- ARP Analysis
- Routing Table Analysis
- Network Connectivity Testing
- Listening Port Analysis
- SMB Security Awareness
- Firewall Awareness
- Network Troubleshooting
- Network Security Fundamentals
- Technical Documentation

---

# 📁 Related Portfolio Work

This network map connects with other projects in my cybersecurity portfolio, including:

- Virtual Cybersecurity Home Lab
- Windows & Linux System Hardening
- Linux Hardening Checklist
- Firewall Rules & Network Defense Audit
- Incident Response Quick Guide
- SSH Authentication Log Investigation

Together, these projects demonstrate how networking, system administration, security configuration, monitoring, and incident investigation work together in a cybersecurity environment.

---

# Conclusion

This project demonstrates my ability to examine and document the network configuration of Windows and Linux virtual machines in a cybersecurity home lab.

Through the lab, I practiced IPv4 addressing, gateway testing, NAT networking, DNS resolution, ARP analysis, routing, listening-port analysis, and network-security concepts.

The network map provides a visual representation of the lab environment and supports the technical evidence documented throughout the rest of my cybersecurity portfolio.
