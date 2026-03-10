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
Client → Server
During a MITM attack it becomes:
Client → Attacker → Server

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
192.168.1.1 → AA:BB:CC:DD:EE:FF
However, ARP was designed **without authentication mechanisms**, meaning that devices generally **trust ARP replies automatically**.

Because of this design limitation, attackers can manipulate ARP tables on devices inside the network.

---
# 🧪 ARP Spoofing / ARP Poisoning

One of the most common ways to perform a local MITM attack is **ARP Spoofing**.

The basic idea:

1️⃣ The attacker sends **forged ARP replies** to devices on the network.  

2️⃣ The victim associates the attacker's **MAC address** with another device's IP address (usually the router).  

3️⃣ Traffic intended for the router is instead sent to the attacker.  

4️⃣ The attacker forwards the traffic to the real router while **intercepting or modifying the packets**.
