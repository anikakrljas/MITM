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

## 🔎 Gathering Network Information

Before starting ARP spoofing, we need to collect some basic network information.

Check the IP address of the Kali machine:

```hostname -I```

```ip route | grep default```

## ⚡ ARP Spoofing with arpspoof

Start ARP spoofing using the arpspoof tool included in the dsniff package.

Terminal 1 – Spoof the Target

```arpspoof -i wlan0 -t TARGET_IP ROUTER_IP```

This tells the target machine that the attacker (Kali) is the router.

---

Terminal 2 – Spoof the Router

```arpspoof -i wlan0 -t ROUTER_IP TARGET_IP```

This tells the router that the attacker (Kali) is the target machine.

---

Terminal 3 – Enable Packet Forwarding

```echo 1 > /proc/sys/net/ipv4/ip_forward```

This allows Kali to forward packets between the router and the target, preventing the network connection from breaking.

## ✅ Verifying the Attack

After ARP spoofing is running, if the target checks its ARP table using: arp -a.

The MAC address of the router should now appear as the MAC address of the Kali machine, indicating that the ARP poisoning was successful.

## 📸 ARP Spoofing Demonstration

The following screenshots demonstrate how ARP poisoning changes the MAC address associated with the router on the target machine.

---

### 1. Kali Linux Network Interface

This screenshot shows the Kali machine network configuration.  
The MAC address of Kali is **08:00:27:63:b0:05** and the IP address is **192.168.100.4**.

![Kali Network Interface](![viber_slika_2026-03-12_16-45-26-561](https://github.com/user-attachments/assets/07409e0a-c693-4b48-9ff5-3553e9cdc598))

---

### 2. ARP Table on Target Machine (Before the Attack)

Before launching the ARP spoofing attack, the target machine correctly resolves the router's IP address **192.168.100.1** to its legitimate MAC address **52-55-c0-a0-04-01**.

![ARP Table Before Attack](![viber_slika_2026-03-12_16-47-41-108](https://github.com/user-attachments/assets/c943404c-9e1f-41a9-b846-da0ff0634d5e))

---

### 3. ARP Table on Target Machine (After the Attack)

After running `arpspoof`, the MAC address associated with the router IP **192.168.100.1** changes to **08-00-27-63-b0-05**, which is the MAC address of the Kali machine.

This indicates that the target machine now believes Kali is the router, demonstrating a successful **ARP poisoning / Man-in-the-Middle attack**.

![ARP Table After Attack](![viber_slika_2026-03-12_16-47-40-778](https://github.com/user-attachments/assets/efd11be9-2472-449d-a67e-7c92128622df))

---

### ✅ Result

The change of the router's MAC address in the ARP table proves that the attacker successfully inserted themselves between the router and the target machine.
