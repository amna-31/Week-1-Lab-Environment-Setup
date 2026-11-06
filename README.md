# Cybersecurity Lab Setup: Kali Linux, Windows 10 and Android on VirtualBox

A private virtual lab for practicing network security and penetration testing in a safe, repeatable environment.

![Hypervisor](https://img.shields.io/badge/Hypervisor-VirtualBox-0070C0?style=flat-square)
![Attacker](https://img.shields.io/badge/Attacker-Kali%20Linux%202026.1-E87500?style=flat-square)
![Targets](https://img.shields.io/badge/Targets-Windows%2010%20%7C%20Android-238F89?style=flat-square)
![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-404040?style=flat-square)
![Purpose](https://img.shields.io/badge/Purpose-Education-C00000?style=flat-square)

---

## Overview

This project documents how I built a virtual security lab on my own computer using VirtualBox. The lab has one Kali Linux machine for testing and three other virtual machines (two Windows 10 and one Android) that can act as targets.

All machines use a private virtual network in the 10.0.0.0/24 range. This keeps lab traffic away from my real network and lets the machines reach each other while still having internet access.

The goal of this first project is to get the lab running and confirm that every machine has a working network connection. Later projects will build on it for scanning, enumeration and other authorized testing.

---

## Goals

- Install VirtualBox on the host computer.
- Create a private NAT Network for the lab.
- Import Kali Linux and connect it to the NAT Network.
- Give Kali a fixed IP address.
- Add Windows 10 and Android virtual machines to the lab.
- Confirm that each machine has an IP address and a gateway.
- Confirm that DNS and internet access work.
- Record the problems I faced and how I fixed them.

---

## What the Lab Is For

- Network scanning and reconnaissance
- Vulnerability assessment
- Traffic and packet analysis
- Web application testing
- Trying out security tools against my own machines

**Important:** Use this lab only on systems that you own or have written permission to test. Never use these tools against systems you are not authorized to test.

---

## Lab Layout

```
                 NAT Network  (10.0.0.0/24)
                 Gateway: 10.0.0.1
                          |
     ---------------------------------------------------
     |                |                |               |
 Kali Linux      Windows 10 #1    Windows 10 #2    Android VM
 10.0.0.2        10.0.0.3         10.0.0.4         10.0.0.5
 (static)
```

| Machine | IP address | Network adapter | How it was set |
|---------|------------|-----------------|----------------|
| Kali Linux 2026.1 | 10.0.0.2 | NAT Network: NatNetwork | Static, set manually |
| Windows 10 (VM 1) | 10.0.0.3 | NAT Network: NatNetwork1 | Received from the network |
| Windows 10 (VM 2) | 10.0.0.4 | NAT Network: NatNetwork1 | Received from the network |
| Android VM | 10.0.0.5 | Virtual Wi-Fi (VirtWifi) | Received from the network |

---

## System Details

| Item | Value |
|------|-------|
| Host operating system | [YOUR HOST OS] |
| Host RAM | [YOUR HOST RAM] |
| Host processor | [YOUR PROCESSOR] |
| Hypervisor | VirtualBox [YOUR VERSION] |
| Attacker machine | Kali Linux 2026.1 (VirtualBox image, amd64) |
| RAM given to Kali | [YOUR KALI RAM] |
| Target machines | Windows 10 (two VMs), Android (one VM) |
| Network type | NAT Network |
| Network range | 10.0.0.0/24 |
| Gateway | 10.0.0.1 |
| DNS server (Kali) | 8.8.8.8 |
| Network adapter | Intel PRO/1000 MT Desktop (82540EM) |

---

## Setup Steps

### Step 1: Install VirtualBox

I downloaded VirtualBox from the official website and installed it on the host computer.

### Step 2: Create the NAT Network

In VirtualBox, I created a NAT Network that uses the 10.0.0.0/24 range, with 10.0.0.1 as the gateway.

I chose a NAT Network instead of plain NAT because machines on a NAT Network can talk to each other and still reach the internet. A plain NAT adapter keeps every VM isolated from the others, which is not what a multi-machine lab needs.

### Step 3: Import Kali Linux and Attach It to the Network

I downloaded the ready-made Kali Linux VirtualBox image (version 2026.1) from the official Kali website, extracted it, and opened it in VirtualBox.

In the VM settings, under Network, Adapter 1 was set like this:

```
Enable Network Adapter: ticked
Attached to:            NAT Network
Name:                   NatNetwork
Adapter Type:           Intel PRO/1000 MT Desktop (82540EM)
Promiscuous Mode:       Allow All
Virtual Cable Connected: ticked
```

Promiscuous Mode was set to Allow All so that Kali can see traffic on the virtual network, which is needed later for packet analysis.

![Kali adapter settings in VirtualBox](Kali_network_config.png)

### Step 4: Set a Fixed IP Address on Kali

Inside Kali, I opened the wired connection settings, went to the IPv4 tab, and changed the method from automatic to Manual:

```
Method:   Manual
Address:  10.0.0.2
Netmask:  24
Gateway:  10.0.0.1
DNS:      8.8.8.8
```

A fixed address makes the lab easier to document and means I can always find the Kali machine at the same address.

![Kali IPv4 settings](Kali_network_settings.png)

### Step 5: Test Kali's Connection

After saving the settings, I pinged google.com from the Kali terminal. The name resolved and replies came back, which confirmed that the gateway, internet access and DNS all work.

![Kali ping test](Kali_network_working.png)

### Step 6: Add the Target Machines

I created the target VMs and connected them to the same 10.0.0.0/24 network.

**Windows 10 (VM 1):** attached to NatNetwork1, received 10.0.0.3. I ran `ipconfig` and then pinged google.com to confirm internet access.

![Windows 10 VM 1](windows_10_config.png)

**Windows 10 (VM 2):** attached to NatNetwork1, received 10.0.0.4.

![Windows 10 VM 2](Windows10.png)

**Android VM:** connected through the virtual Wi-Fi network (VirtWifi), received 10.0.0.5 with 10.0.0.1 as the gateway.

![Android network details](Android_network_settings.png)

---

## Verification

| Machine | Check | Result |
|---------|-------|--------|
| Kali Linux | `ping google.com` | Name resolved to 142.250.200.174, replies received (4 of 5 packets) |
| Windows 10 (VM 1) | `ipconfig` | IPv4 10.0.0.3, mask 255.255.255.0, gateway 10.0.0.1 |
| Windows 10 (VM 1) | `ping google.com` | Name resolved to 142.251.37.142, 3 of 3 replies, 0% loss |
| Windows 10 (VM 2) | `ipconfig` | IPv4 10.0.0.4, mask 255.255.255.0, gateway 10.0.0.1 |
| Android VM | Network details | IP 10.0.0.5, gateway 10.0.0.1 |

---

## Problems and Fixes

### Problem 1: No internet by name after setting a static IP on Kali

**What happened:** After I set the manual IP address, pinging google.com from Kali failed with a "Temporary failure" error. This error means the name could not be resolved. At that time the DNS server field was set to 10.0.0.1, the gateway address.

![Kali ping failure](Kali_network_error.png)

**How I fixed it:** I changed the DNS server in the Kali connection settings from 10.0.0.1 to 8.8.8.8 (Google's public DNS) and saved. After that, google.com resolved and the ping worked (see Step 5).

**Lesson:** When a ping to a name fails, test with an IP address too. If the IP works but the name does not, the problem is DNS and not the network connection itself.

### Problem 2: `ifconfig` is not recognized on Windows

**What happened:** On the Windows 10 VM, I typed `ifconfig` in PowerShell, which I normally use on Linux. PowerShell returned a "not recognized" error.

**How I fixed it:** Windows uses `ipconfig` instead. Running `ipconfig` displayed the IPv4 address, subnet mask and gateway as expected.

---

## What I Learned

- **NAT vs NAT Network:** With a normal NAT adapter, each VM is isolated and can only reach the internet. A NAT Network puts several VMs on one private network, so they can reach each other as well as the internet. This is what makes a multi-machine lab possible.
- **Static IP configuration:** I learned to set the address, netmask, gateway and DNS by hand in Kali. Every one of these values must be correct, because a single wrong value, like my DNS entry, can break name resolution.
- **Troubleshooting step by step:** I learned to separate problems: first check the IP address, then the gateway, then the internet, then DNS.
- **Platform differences:** Kali uses `ip a` and `ifconfig`-style tools, Windows uses `ipconfig`, and Android shows the same details in its Wi-Fi settings.
- **Promiscuous mode:** Setting it to Allow All lets the Kali VM see the lab's network traffic, which I will need for packet analysis.
- **Documentation:** Keeping screenshots and notes of both the errors and the fixes makes the project easier to repeat and to explain to others.

---

## Next Steps

- Take a clean snapshot of every VM before doing any testing.
- Check that the machines can reach each other, for example by pinging 10.0.0.3 from Kali.
- Run the first network scans from Kali against my own target VMs.
- Add intentionally vulnerable machines for practice.

---

## Ethical Use

This lab is for learning only. I will test only systems I own or have permission to test.

---

## Links

- VirtualBox: https://virtualbox.org/wiki/Downloads
- Kali Linux: https://kali.org/get-kali
- 7-Zip (to extract the Kali VM archive): https://7-zip.org/download.html

---

## Author

**[YOUR FULL NAME]**
[YOUR BATCH / ID]
LinkedIn: [YOUR LINKEDIN URL]

Program: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity and Pentesting Lab Setup
