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

- [📖 About](#about)
- [⚙️ Requirements](#requirements)
- [🚀 Commands & Explanations](#commands--explanations)
  - [1. Host Discovery](#1-host-discovery)
  - [2. Port Scanning](#2-port-scanning)
  - [3. Version & OS Detection](#3-version--os-detection)
  - [4. Brute Force (SSH)](#4-brute-force-ssh)
  - [5. Vulnerability Scanning](#5-vulnerability-scanning)
- [🧠 Real World Usage](#real-world-usage)
- [🔓 Vulnerabilities](#common-ports--their-vulnerabilities)
- [⚠️ Legal Notice](#legal-notice)
- [👨‍💻 Author](#author)
- [📜 License](#license)


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

## 🔓 Common Ports & Their Vulnerabilities

| Port | Service | Version Example         | Vulnerability/CVE                | How Hackers Exploit It |
|------|---------|--------------------------|----------------------------------|-------------------------|
| 21   | FTP     | vsftpd 2.3.4             | CVE-2011-2523 (Backdoor Shell)   | Attackers exploit this version's hidden backdoor by sending a crafted smiley `:)` in the username to get root shell. |
| 22   | SSH     | OpenSSH < 7.4            | CVE-2018-15473 (Username Enumeration) | Hackers enumerate valid users before brute forcing, saving time and avoiding detection. |
| 23   | Telnet  | Any                      | Unencrypted Protocol             | Credentials can be sniffed in plaintext using Wireshark or MITM attacks. |
| 25   | SMTP    | Exim < 4.91              | CVE-2019-10149 (RCE)             | Attackers send crafted email headers to execute code remotely and escalate privilege. |
| 53   | DNS     | BIND 9.x                 | CVE-2015-5477 (DoS)              | Used to crash DNS servers with malformed packets, often in DDoS chains. |
| 80   | HTTP    | Apache 2.4.49            | CVE-2021-41773 (Path Traversal RCE) | Hackers exploit improper URL sanitization to access sensitive files like `/etc/passwd` or execute code. |
| 110  | POP3    | Dovecot 2.2.x            | CVE-2017-14461 (Auth Bypass)     | Hackers gain unauthorized access by bypassing authentication mechanisms. |
| 139  | NetBIOS | Windows SMB              | CVE-1999-0519 (Null Session)     | Allows attackers to enumerate users and shares without login. |
| 445  | SMB     | Windows 7/XP             | CVE-2017-0144 (EternalBlue)      | Used in WannaCry ransomware; allows remote code execution via SMBv1. |
| 3306 | MySQL   | MySQL < 5.7              | CVE-2016-6662 (Config File Injection) | Remote attackers write to my.cnf to inject malicious code. |
| 3389 | RDP     | Windows RDP              | CVE-2019-0708 (BlueKeep)         | Exploits RDP to execute code without credentials — leads to wormable attacks. |
| 5432 | Postgres| PostgreSQL < 9.3         | CVE-2013-1899 (DoS/Code Exec)    | Attackers can modify data, escalate privileges, or crash the service. |
| 8080 | HTTP    | Apache Tomcat < 9.0.30   | CVE-2020-1938 (Ghostcat)         | Exploits AJP protocol to access sensitive files or run code remotely. |

> 🔐 Note: Always check for real-time CVE updates at [https://cve.mitre.org](https://cve.mitre.org)


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
