# 🔐 Cybersecurity Lab Environment Setup

**Building an isolated virtual lab for penetration testing and ethical hacking practice**

![Skill](https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000) ![VirtualBox](https://img.shields.io/badge/Ver-Virtualbox%20[YOUR%20VERSION]-0070C0?style=flat-square&labelColor=000000) ![Kali](https://img.shields.io/badge/Kali%20Linux-v[YOUR%20VERSION]-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white) ![Skill](https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000) ![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000) ![Pentest](https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white) ![NetworkWalks](https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000) ![Ethical Hacking](https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white) ![Author](https://img.shields.io/badge/[YOUR%20NAME]-C00000?style=flat-square)

---

## 📌 Project Overview

This project focuses on setting up a **virtual cybersecurity and penetration-testing laboratory** using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

---

## 🎯 Objectives

The main objectives of this project are to:

- Install and configure VirtualBox.
- Install/import Kali Linux as a virtual machine.
- Create a private **NAT Network** for the cybersecurity lab.
- Configure network connectivity for Kali Linux.
- Assign a consistent IP address to the Kali VM.
- Verify network connectivity and DNS resolution.
- Take a clean VM snapshot for recovery.
- Document the complete setup process.
- Prepare the environment for future cybersecurity projects.

---

## 🛡️ Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

⚠️ **Important:** This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

---

## 🏗️ Lab Architecture

<!-- Replace with your own architecture/title image (upload it as 1-screenshot-title-image.png) -->
[![Lab Architecture](1-screenshot-title-image.png)](1-screenshot-title-image.png)

Additional target machines can be added to the same virtual network in future projects.

---

## ⚙️ Lab Configuration

<!-- Edit every value below to match YOUR system -->

| 🧩 Component       | ⚙️ Configuration         |
|-------------------|--------------------------|
| 🖥️ Host OS        | [YOUR HOST OS]           |
| 🧠 Host RAM        | [YOUR HOST RAM]          |
| ⚡ Processor       | [YOUR PROCESSOR]         |
| 🧰 Hypervisor      | VirtualBox [VERSION]     |
| 🐉 Security OS     | Kali Linux [VERSION]     |
| 🧠 Kali RAM        | [e.g. 2048 MB]           |
| 🌐 Virtual Network | NAT Network              |
| 📡 Network Address | [e.g. 10.0.0.0/24]       |
| 🐧 Kali IP Address | [e.g. 10.0.0.2/24]       |
| 🚪 Default Gateway | [e.g. 10.0.0.1]          |
| 🌍 DNS Server      | [e.g. 8.8.8.8]           |
| 🔮 Future VM Range | [e.g. 10.0.0.3–10.0.0.99]|

---

# 🪜 Lab Setup Procedure

## Step 1. Install 7-Zip

7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a `.7z` archive.

**Tool:** 7-Zip

---

## Step 2. Install VirtualBox

VirtualBox was installed as the hypervisor.

---

## Step 3. Create the NAT Network

A dedicated NAT Network was created in VirtualBox.

Configuration: Network Name: [NatNetwork] IPv4 Prefix: [10.0.0.0/24] DHCP: [Enabled] IPv6: [Disabled]

[![NAT Network Settings](2-screenshot-network-settings-1.png)](2-screenshot-network-settings-1.png)

A **NAT Network** was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This will allow future attacker and target VMs to communicate within the lab.

---

## Step 4. Import Kali Linux

The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:

```
Adapter 1
Attached to: NAT Network
Network:     [NatNetwork]
Adapter Type: [Intel PRO/1000 MT Desktop]
```

The VM was allocated:

```
RAM: [2048 MB]
```

[![Kali Linux](3-screenshot-kali-linux.png)](3-screenshot-kali-linux.png)

<!-- Keep the next line only if you really configured a shared folder -->
A shared folder was also configured for transferring required files between the host operating system and the Kali VM.

---

## Step 5. Configure the Kali Linux Network

The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:

```
IP Address: [10.0.0.2]
Subnet Mask: [255.255.255.0]
Gateway: [10.0.0.1]
DNS: [8.8.8.8]
```

A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.

[![Kali Network Settings](4-screenshot-kali-network-settings.png)](4-screenshot-kali-network-settings.png)

---

## Step 6. Create a Clean VM Snapshot

After completing the initial configuration, a VirtualBox snapshot was created.

Example snapshot name:

```
Clean Kali - Network Setup
```

The snapshot represents the clean baseline of the laboratory.

If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.

---

# 🔎 Lab Verification

| ✅ Test                       | 🧾 Command                       | 🎯 Expected Result               |
|------------------------------|---------------------------------|---------------------------------|
| 🌐 Check IP address           | `ip a`                          | Correct Kali IP displayed       |
| 📡 Test gateway               | `ping [GATEWAY IP]`             | Successful replies              |
| 🌍 Test Internet connectivity | `ping 8.8.8.8`                  | Successful replies              |
| 🔎 Test DNS resolution        | `nslookup networkwalks.com`     | Domain resolves                 |
| 🧰 Verify Nmap                | `nmap --version`                | Nmap version displayed          |
| 🔄 Verify snapshot            | Restore snapshot and run `ip a` | Baseline configuration restored |

### Example Results

```
IP Address:
[YOUR KALI IP/24]

Gateway:
[YOUR GATEWAY]

DNS:
[YOUR DNS]
```

---

# 🐞 Problems Encountered & Solutions

Documenting problems is an important part of the project.

<!-- Write ONLY the problems you actually faced. Below are two common examples; delete or replace as needed. -->

## Problem 1. [Your Problem Title]

[Describe what happened.]

[Describe how you solved it.]

```
[command you used, if any]
```

> **Important:** Network interface and connection names may differ between systems. Students should first identify their actual connection name before running an `nmcli` command.

---

## Problem 2. [Your Problem Title]

[Describe what happened.]

The issue was resolved by:

1. [Step 1]
2. [Step 2]
3. [Step 3]

[Result after the fix.]

---

# 💡 What I Learned

Through this project, I learned how to create and configure a virtual environment for cybersecurity practice.

The most important concepts I learned include:

### 1. NAT vs NAT Network

A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple VMs connected to the same virtual network to communicate with one another while providing network address translation for external connectivity.

This makes it useful for building a multi-machine cybersecurity laboratory.

### 2. Virtual Machine Networking

I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network configuration affects communication between machines.

### 3. Static IP Configuration

I learned how to configure and verify IPv4 addressing, subnet masks, gateways, and DNS settings in Kali Linux.

### 4. VM Snapshots

I learned that a clean snapshot should be created **before performing risky or experimental activities**.

This provides a known-good recovery point for future cybersecurity exercises.

### 5. Documentation

I learned that documenting commands, configuration, screenshots, problems, and solutions is an important part of a professional cybersecurity project.

---

# 🔐 Security & Ethical Use

This laboratory is intended strictly for education purposes only.

---

# 🔗 Tools & Resources

- **7-Zip:** [https://7-zip.org/download.html](https://7-zip.org/download.html)
- **VirtualBox:** [https://virtualbox.org/wiki/Downloads](https://virtualbox.org/wiki/Downloads)
- **Kali Linux:** [https://kali.org/get-kali](https://kali.org/get-kali)

---

# 👤 Author

**[YOUR FULL NAME]**  
Cybersecurity Professional [YOUR BATCH/ID]

LinkedIn: [YOUR LINKEDIN URL]

---

## 📌 Project Information

**Program Name:** Cybersecurity at Networkwalks | **Week:** 01 | **Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub
