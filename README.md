# DarkWolf Pentesting Toolkit 🛡️
> 🔍 Advanced Network Reconnaissance & Vulnerability Scanning with Nmap  
> Made with 💻 Kali Linux | 🔨 Real Pentesting Labs | ⚔️ Ethical Hacking Only | 
> Created by: **Muhammad Saqlain Shoukat (Dark Wolf)** |
> YouTube: [@CodingChatRoom](https://www.youtube.com/@CodingChatRoom)  

---

![Nmap](https://img.shields.io/badge/Tool-Nmap-blue?style=flat-square)
![License](https://img.shields.io/badge/Use-Ethical%20Only-green?style=flat-square)
![Status](https://img.shields.io/badge/Stage-Active%20Development-orange?style=flat-square)

---

## 📁 Table of Contents

- [📖 About](#-about)
- [⚙️ Requirements](#️-requirements)
- [🚀 Commands & Explanations](#-commands--explanations)
  - [1. Host Discovery](#1-host-discovery)
  - [2. Port Scanning](#2-port-scanning)
  - [3. Version & OS Detection](#3-version--os-detection)
  - [4. Brute Force (SSH)](#4-brute-force-ssh)
  - [5. Vulnerability Scanning](#5-vulnerability-scanning)
- [🧠 Real World Usage](#-real-world-usage)
- [⚠️ Legal Notice](#️-legal-notice)
- [👨‍💻 Author](#-author)
- [📜 License](#-license)

---

## 📖 About

**DarkWolf Pentesting Toolkit** is a practical and powerful set of Nmap-based penetration testing commands curated for real-world network exploitation scenarios. It focuses on reconnaissance, service enumeration, brute-force, and vulnerability scanning — all using industry-standard methodologies.

---

## ⚙️ Requirements

- ✅ Kali Linux 2023.1+
- ✅ Nmap 7.90+
- ✅ Wordlists (`rockyou.txt`, `usernames.txt`)
- 🔐 Permission to scan target network

---

## 🚀 Commands & Explanations

### 1. 🎯 Host Discovery

```bash
nmap -sn 192.168.1.0/24
```
* **Purpose:** Ping sweep to discover active hosts.
* **Use Case:** Initial phase of reconnaissance to map out the subnet.

---

### 2. 📡 Port Scanning

```bash
nmap 192.168.1.10
```
* **Purpose:** Default scan for 1000 most common TCP ports.
* **Tip:** Fast and lightweight.

```bash
nmap -p- 192.168.1.10
```
* **Purpose:** Scan all 65535 TCP ports.
* **Use Case:** Catch hidden services running on non-standard ports.

```bash
nmap -sS 192.168.1.10
```
* **Purpose:** TCP SYN scan (stealth scan).
* **Why:** Less noisy than full TCP connections (ideal for evading detection).

---

### 3. 🧠 Version & OS Detection

```bash
nmap -sV 192.168.1.10
```
* **Purpose:** Detect versions of running services.

```bash
nmap -A 192.168.1.10
```
* **Purpose:** Aggressive scan with OS detection, version detection, script scanning, and traceroute.
* **Warning:** Very loud — easily detected by firewalls and IDS.

```bash
nmap -Pn 192.168.1.10
```
* **Purpose:** Treat all hosts as up — skip ICMP discovery (for hosts behind firewalls blocking ping).

---

### 4. 🔐 Brute Force (SSH)

```bash
nmap -p 22 --script ssh-brute \
--script-args userdb=/usr/share/wordlists/usernames.txt,passdb=/usr/share/wordlists/rockyou.txt \
192.168.1.10
```
* **Purpose:** Brute force SSH login using Nmap NSE script.
* **Wordlists Used:** `rockyou.txt` for passwords, custom usernames list.
* **Note:** Effective for weak credential attacks.

---

### 5. 🛡️ Vulnerability Scanning

```bash
nmap --script vuln 192.168.1.10
```
* **Purpose:** Run a collection of Nmap vulnerability detection scripts.
* **Use Case:** Find known CVEs, misconfigurations, and vulnerable software.

```bash
nmap -sS -sV -A -T4 -p- 192.168.1.10
```
* **Ultimate Command:** Full stealth scan with version detection, aggressive scan, speed boost, and full port range.
* **Flags Explained:**
  * `-sS`: Stealth SYN scan  
  * `-sV`: Version detection  
  * `-A`: Aggressive mode  
  * `-T4`: Faster execution  
  * `-p-`: All ports

---

## 🧠 Real World Usage

These commands are frequently used in penetration testing engagements for:

* ✅ Asset discovery and mapping internal networks
* ✅ Identifying vulnerable services and open ports
* ✅ Brute forcing weak SSH credentials
* ✅ Initial attack surface enumeration

---

## ⚠️ Legal Notice

> This toolkit is **strictly for educational and authorized penetration testing** only.  
> You must have **explicit permission** to scan any target.  
> Misuse of these tools can result in legal consequences.

---

## 👨‍💻 Author

**Muhammad Saqlain Shoukat (Dark Wolf)**  
🐺 YouTube: [@CodingChatRoom](https://www.youtube.com/@CodingChatRoom)  
💻 Platform: Kali Linux

---

## 📜 License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).
