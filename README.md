# Cybersecurity Lab Setup with VirtualBox and Kali Linux

A private virtual lab for practicing network security and penetration testing in a safe, repeatable environment.

![Virtualization](https://img.shields.io/badge/Hypervisor-VirtualBox-0070C0?style=flat-square)
![OS](https://img.shields.io/badge/OS-Kali%20Linux-E87500?style=flat-square)
![Network](https://img.shields.io/badge/Network-NAT%20Network-238F89?style=flat-square)
![Purpose](https://img.shields.io/badge/Purpose-Education-404040?style=flat-square)

---

## Overview

This project documents how I built a virtual lab on my own computer using VirtualBox and Kali Linux. The lab is meant for learning security tools and techniques without putting any real system at risk.

Every machine in the lab sits on a private virtual network. This keeps lab traffic separate from my home or office network and makes it easy to add more virtual machines later.

[Add 1-2 sentences about why you built this lab or what you plan to practice in it.]

---

## Goals

- Install VirtualBox on the host computer.
- Import Kali Linux as a virtual machine.
- Create a private NAT Network for the lab.
- Give the Kali VM a fixed IP address.
- Confirm that the VM can reach the gateway, the internet, and DNS.
- Save a clean snapshot to return to if something breaks.
- Record the whole process, including the problems I faced.

---

## What the Lab Is For

- Network scanning and reconnaissance
- Vulnerability assessment
- Traffic and packet analysis
- Web application testing
- Trying out security tools

**Important:** Use this lab only on systems that you own or have written permission to test. Never use these tools against systems you are not authorized to test.

---

## Lab Layout

![Lab layout](1-screenshot-title-image.png)

[Describe your layout in one or two lines, for example: one Kali VM connected to a NAT Network, with room for more target VMs later.]

---

## System Details

| Item | Value |
|------|-------|
| Host operating system | [e.g. Windows 11] |
| Host RAM | [e.g. 16 GB] |
| Host processor | [e.g. Intel Core i5] |
| Hypervisor | VirtualBox [version] |
| Guest operating system | Kali Linux [version] |
| RAM given to Kali | [e.g. 4096 MB] |
| Network type | NAT Network |
| Network range | [e.g. 10.0.0.0/24] |
| Kali IP address | [e.g. 10.0.0.2] |
| Gateway | [e.g. 10.0.0.1] |
| DNS server | [e.g. 8.8.8.8] |
| Reserved for future VMs | [e.g. 10.0.0.3 to 10.0.0.99] |

---

## Setup Steps

### Step 1: Install 7-Zip

The Kali VM image is downloaded as a compressed `.7z` file, so I installed 7-Zip to extract it.

### Step 2: Install VirtualBox

I downloaded VirtualBox from the official website and installed it with the default options.

### Step 3: Create the NAT Network

In VirtualBox, I opened the network manager and created a new NAT Network with these settings:

- Name: [NatNetwork]
- IPv4 prefix: [10.0.0.0/24]
- DHCP: [Enabled / Disabled]
- IPv6: [Enabled / Disabled]

![NAT Network settings](2-screenshot-network-settings-1.png)

I chose a NAT Network because VMs on it can talk to each other and still reach the internet. This is what a lab with several machines needs.

### Step 4: Import Kali Linux

I downloaded the Kali Linux VM image from the official Kali website, extracted it, and opened it in VirtualBox.

VM settings:

```
RAM: [e.g. 4096 MB]
Network adapter: Adapter 1
Attached to: NAT Network
Network name: [NatNetwork]
```

![Kali Linux VM](3-screenshot-kali-linux.png)

[Optional: mention a shared folder or any other setting you changed.]

### Step 5: Set a Fixed IP on Kali

I changed the network settings in Kali to use a static address:

```
IP address:  [10.0.0.2]
Subnet mask: [255.255.255.0]
Gateway:     [10.0.0.1]
DNS:         [8.8.8.8]
```

A fixed address makes the lab easier to document and lets me refer to the same machine in later projects.

![Kali network settings](4-screenshot-kali-network-settings.png)

### Step 6: Take a Clean Snapshot

Once everything was working, I took a snapshot named:

```
[Clean Kali - Network Setup]
```

If a later experiment breaks the VM, I can restore this snapshot and start again from a working state.

---

## Verification

| Check | Command | Expected result |
|-------|---------|-----------------|
| IP address | `ip a` | Shows the static IP |
| Gateway | `ping [gateway IP]` | Replies received |
| Internet | `ping 8.8.8.8` | Replies received |
| DNS | `nslookup [any domain]` | Domain resolves |
| Nmap | `nmap --version` | Version is printed |
| Snapshot | Restore it, then run `ip a` | Original settings return |

Results from my lab:

```
IP address: [your result]
Gateway:    [your result]
DNS:        [your result]
```

---

## Problems and Fixes

[Write only the problems you really faced. Copy the format below for each one.]

### Problem 1: [Title]

What happened: [describe the issue]

How I fixed it: [describe the fix]

```
[command used, if any]
```

### Problem 2: [Title]

What happened: [describe the issue]

How I fixed it:

1. [step]
2. [step]
3. [step]

---

## What I Learned

- **NAT vs NAT Network:** [explain in your own words]
- **VM networking:** [explain in your own words]
- **Static IP configuration:** [explain in your own words]
- **Snapshots:** [explain in your own words]
- **Documentation:** [explain in your own words]

---

## Ethical Use

This lab is for learning only. I will test only systems I own or have permission to test.

---

## Links

- 7-Zip: https://7-zip.org/download.html
- VirtualBox: https://virtualbox.org/wiki/Downloads
- Kali Linux: https://kali.org/get-kali

---

## Author

**[Your Full Name]**
[Your Batch / ID]
LinkedIn: [Your LinkedIn URL]

Program: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity and Pentesting Lab Setup
