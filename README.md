# 🕵️ Man-in-the-Middle (MITM) Attack – Educational Demonstration

![Security](https://img.shields.io/badge/Cybersecurity-Education-blue)
![Purpose](https://img.shields.io/badge/Purpose-Learning-green)
![License](https://img.shields.io/badge/Use-Educational%20Only-orange)

🔐 This repository demonstrates the concept of a **Man-in-the-Middle (MITM) attack** in a controlled environment for **educational and research purposes**.

The goal of this project is to help students, cybersecurity beginners, and network enthusiasts understand **how certain network protocols can be abused when they lack proper security mechanisms**, and how these attacks can be detected and mitigated.

---

# ⚠️ Disclaimer

All demonstrations and materials in this repository are intended **strictly for educational purposes**.

The techniques shown here should only be used in:

- controlled laboratory environments
- private networks you own
- systems where you have **explicit authorization**

Any misuse of this information against systems without permission may be **illegal and unethical**.

The purpose of this repository is to **learn how attacks work in order to better defend against them**.

---

# 📚 What is a Man-in-the-Middle Attack?

A **Man-in-the-Middle (MITM)** attack occurs when an attacker secretly intercepts communication between two devices on a network.

Normally communication happens directly:
Client → Server.
During a MITM attack it becomes:
Client → Attacker → Server

<img width="1083" height="724" alt="mitm_diagram_resized_border" src="https://github.com/user-attachments/assets/dcbb927e-2199-4262-9da2-ce3ae5e65cc3" />

This allows the attacker to potentially:

- 👀 intercept network traffic
- 📡 monitor communications
- ✏️ modify transmitted data
- 🎭 impersonate one of the communicating parties

Because both sides believe they are communicating directly with each other, the attack can remain **undetected without proper protections**.

---
# 🌐 Why ARP is Important in MITM Attacks

Many MITM attacks in **local networks (LAN)** rely on weaknesses in the **Address Resolution Protocol (ARP)**.

ARP is responsible for mapping:
IP Address → MAC Address
inside a local network.

For example:
192.168.1.1 → AA:BB:CC:DD:EE:FF.
However, ARP was designed **without authentication mechanisms**, meaning that devices generally **trust ARP replies automatically**.

Because of this design limitation, attackers can manipulate ARP tables on devices inside the network.

---

# 🛡️ Protection Against MITM Attacks

Although Man-in-the-Middle attacks can be dangerous, there are several ways to reduce the risk and protect network communication.

### 🔒 Use HTTPS

Always prefer websites that use **HTTPS (Hypertext Transfer Protocol Secure)**.

HTTPS encrypts communication between the client and the server using **TLS/SSL**, which prevents attackers from easily reading or modifying transmitted data even if they intercept the traffic.

---

### 📶 Be Careful on Public Wi-Fi Networks

Public networks (such as those in cafés, airports, hotels, or universities) are common targets for MITM attacks.

When connecting to public Wi-Fi:

- avoid logging into sensitive accounts
- avoid accessing banking or personal services
- ensure websites are using **HTTPS**

Attackers on the same network may attempt to intercept traffic using techniques such as **ARP spoofing**.

---

### 🔐 Use a VPN

A **Virtual Private Network (VPN)** encrypts your internet traffic and creates a secure tunnel between your device and the VPN server.

This helps protect your data from attackers who might be monitoring the local network.

---

### 🔄 Keep Systems and Software Updated

Regularly updating your **operating system, browsers, and applications** is important because updates often include:

- security patches
- vulnerability fixes
- improved network security mechanisms

Outdated software can contain vulnerabilities that attackers may exploit.

---

### 📊 Use Network Monitoring Tools

Network monitoring and security tools can help detect suspicious activity such as:

- unusual ARP traffic
- duplicate IP or MAC addresses
- abnormal network behavior

Examples include:

- intrusion detection systems (IDS)
- packet analyzers
- network monitoring platforms

These tools can help administrators identify **potential MITM attempts** early.

<img width="1024" height="1024" alt="ChatGPT Image Mar 11, 2026, 06_18_30 PM" src="https://github.com/user-attachments/assets/7638b920-be0d-473a-a250-e6e7c435005b" />

---

Understanding how MITM attacks work is an important step toward building **more secure networks and safer communication systems**.

---
# 🧪 ARP Spoofing / ARP Poisoning

One of the most common ways to perform a local MITM attack is **ARP Spoofing**.

The basic idea:

1️⃣ The attacker sends **forged ARP replies** to devices on the network.  

2️⃣ The victim associates the attacker's **MAC address** with another device's IP address (usually the router).  

3️⃣ Traffic intended for the router is instead sent to the attacker.  

4️⃣ The attacker forwards the traffic to the real router while **intercepting or modifying the packets**.

---
# 🧪 Basic Lab Preparation

Before running the demonstration in a **controlled lab environment**, it is necessary to check network information and install the required tools.

---

## 🖥️ Checking the ARP Table on Windows

On a **Windows** machine you can view the ARP table using the following command:

```arp -a```


## 🐧 Installing Required Tools on Kali Linux

On Kali Linux, we need to install a package that contains network analysis tools.

```sudo su```
```sudo apt install dsniff```

The dsniff package includes several tools used for network traffic analysis and security testing.
