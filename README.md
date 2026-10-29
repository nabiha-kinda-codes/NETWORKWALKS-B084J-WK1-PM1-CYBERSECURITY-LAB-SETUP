<div align="center">

# 🔐 My Cybersecurity Lab Setup

**Creating a safe, isolated virtual lab to practice ethical hacking and penetration testing**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Tool-VirtualBox-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-Virtual%20Machine-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/YOUR%20NAME-C00000?style=flat-square" />
</p>

---

## 📌 Project Overview

This is my first hands-on cybersecurity project: building a **virtual hacking lab** with VirtualBox and Kali Linux on my own computer.

Instead of practicing on my real system, I run Kali Linux inside a virtual machine. That way I can scan, test, and experiment freely, and if something breaks, I can simply restore a saved snapshot instead of reinstalling anything.

The lab sits on its own private virtual network, so I can add more machines later and use them as practice targets for authorized testing.

---


## 🎯 Objectives

By the end of this project, I wanted to:

- Install VirtualBox on my computer.
- Import Kali Linux as a virtual machine.
- Build a private **NAT Network** for the lab.
- Connect the Kali VM to that network.
- Give Kali a fixed (static) IP address.
- Confirm the network and DNS are working.
- Save a clean snapshot to fall back on.
- Write down every step of the process.
- Get the lab ready for my next cybersecurity projects.

---

## 🛡️ Purpose of the Lab

This lab is my safe space for learning and for authorized security testing.

I plan to use it for things like:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Trying out new security tools

⚠️ **Important:** Only use this lab on systems you own or have clear permission to test. Never use these tools against systems you are not authorized to touch.

---

## 🏗️ Lab Architecture

![](1_title.jpg)


More virtual machines can join the same network later as practice targets.

---

## ⚙️ Lab Configuration

| 🧩 Component       | ⚙️ Configuration   |
| ------------------ | ------------------  |
| 🧰 Hypervisor      | VirtualBox [7.2.6] |
| 🐉 Security OS     | Kali Linux [2025.4]|
| 🌐 Virtual Network | NAT Network        |
| 📡 Network Address | 10.0.0.0/24        |
| 🐧 Kali IP Address | 10.0.0.2/24        |
| 🚪 Default Gateway | 10.0.0.1           |
| 🌍 DNS Server      | 10.0.0.1           |

---

# 🪜 Lab Setup Procedure

## Step 1. Install 7-Zip

I installed 7-Zip so I could unpack the Kali Linux virtual machine download, which comes as a compressed `.7z` archive.

**Tool:** 7-Zip

---

## Step 2. Install VirtualBox

Next I installed VirtualBox, which runs the virtual machines for the lab.

---

## Step 3. Create the NAT Network

In VirtualBox I created a dedicated NAT Network for the lab.

Configuration:
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled

![](2_network_settings.jpg)

I chose a **NAT Network** because every VM attached to it can talk to the others, and they can all still reach the internet through the host.

This means any attacker or target VMs I add later will be able to communicate inside the lab.


---

## Step 4. Import Kali Linux

I downloaded the Kali Linux virtual machine from the official Kali website and imported it into VirtualBox.

Then I set the VM's network adapter like this:

```text
Adapter 1
Attached to: NAT Network
Network:     NatNetwork
```

Once the VM was imported and booted, Kali's desktop came up successfully:

![](3_kali_linux.jpg)
A shared folder can also be set up to move files between my main computer and the Kali VM.



---

## Step 5. Configure the Kali Linux Network

Inside Kali, I opened the network connection settings and gave the machine a fixed IPv4 address instead of leaving it on automatic.

My configuration:

```text
Method:      Manual
IP Address:  10.0.0.2
Netmask:     24 (255.255.255.0)
Gateway:     10.0.0.1
DNS:         10.0.0.1
```

> 💡 **Tip:** To open these settings, **right-click** the network icon in Kali's top panel and choose **Edit Connections**.

A fixed IP makes the lab easier to document, and I can always find the Kali machine at the same address.

![](4kali_linux_netwrk.jpg)

---

## Step 6. Create a Clean VM Snapshot

When everything was working, I took a VirtualBox snapshot of the VM.

Snapshot name:

```text
Clean Kali - Network Setup
```

This snapshot is my clean starting point for the whole lab.

If a future experiment breaks something, I can roll the VM back to this exact working state.


---

# 🔎 Lab Verification

| ✅ Test                        | 🧾 Command                      | 🎯 Expected Result              |
| ----------------------------- | ------------------------------- | ------------------------------- |
| 🌐 Check IP address           | `ip a`                          | 10.0.0.2/24 shown on the adapter |
| 📡 Test gateway               | `ping 10.0.0.1`                 | Replies received                |
| 🌍 Test Internet connectivity | `ping 8.8.8.8`                  | Replies received                |
| 🔎 Test DNS resolution        | `nslookup google.com`           | Domain resolves to an IP        |
| 🧰 Verify Nmap                | `nmap --version`                | Nmap version displayed          |
| 🔄 Verify snapshot            | Restore snapshot and run `ip a` | Same settings as before         |

### Example Results

```text
IP Address:
10.0.0.2/24

Gateway:
10.0.0.1

DNS:
10.0.0.1
```

---

# 🐞 Problems Encountered & Solutions

Writing down problems, even small ones, is part of doing a project properly.

## Problem 1. Couldn't Find "Edit Connections" in Kali

When I wanted to change Kali's network settings, I **left-clicked** the network icon in the top panel. That only opened a small quick menu, and there was no option to edit the connection.

**Solution:** I **right-clicked** the network icon instead and chose **Edit Connections**, which opened the full settings window where I could set the static IP.


---

# 💡 What I Learned

This project taught me how to build and configure a virtual environment for practicing cybersecurity.

These are the main things I took away:

### 1. NAT vs NAT Network

Regular NAT gives each VM its own isolated connection to the internet, so VMs can't see each other.

A NAT Network puts multiple VMs on one shared private network where they can talk to each other and still get internet access, which is exactly what a multi-machine lab needs.

### 2. Virtual Machine Networking

I learned how VirtualBox network adapters attach a VM to different kinds of networks, and how that choice decides which machines can communicate.

### 3. Static IP Configuration

I learned how to set and check an IPv4 address, netmask, gateway, and DNS server in Kali Linux.

### 4. VM Snapshots

I learned to take a clean snapshot **before** trying anything risky, so there is always a safe point to return to.

### 5. Documentation

I learned that writing down commands, settings, screenshots, problems, and fixes is a big part of real cybersecurity work, not just an extra.

---

# 🔐 Security & Ethical Use

This lab is for learning purposes only. I will only test systems I own or have permission to test.

---

# 🔗 Tools & Resources

- **7-Zip:** [https://7-zip.org/download.html](https://7-zip.org/download.html)
- **VirtualBox:** [https://virtualbox.org/wiki/Downloads](https://virtualbox.org/wiki/Downloads)
- **Kali Linux:** [https://kali.org/get-kali](https://kali.org/get-kali)

---

# 👤 Author

**Nabiha Imran**\
Cybersecurity Student

LinkedIn: https://www.linkedin.com/in/nabiha-imran-3502753b1/ 

---

## 📌 Project Information

**Program Name:** Cybersecurity at Networkwalks | **Week:** 01 | **Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub
