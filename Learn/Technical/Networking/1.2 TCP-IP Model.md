# 📄 **1.2 — TCP/IP Model (Hacker Version) — Full Detailed Notes**

---

# 🧠 **What is the TCP/IP Model?**

TCP/IP (Transmission Control Protocol / Internet Protocol) is the **real-world** model of how data moves across the internet.

It has **4 layers** (not 7):

|TCP/IP Layer|OSI Equivalent|Purpose|
|---|---|---|
|Application|OSI 5–7|Apps, protocols, communication|
|Transport|OSI 4|TCP/UDP|
|Internet|OSI 3|IP addressing, routing|
|Network Access|OSI 1–2|Physical & data link|

---

# 🔥 Why Hackers Use TCP/IP More

Because real-world attacks focus on:

- **TCP**
- **UDP**
- **IP**
- **Ports**
- **Packets**

This is where scanning, spoofing, MITM, and routing attacks happen.

---

# 🧱 **TCP/IP Layers Explained (Hacker Version)**

---

# 🟦 **Layer 1 — Network Access Layer (Link Layer)**

Equivalent to **OSI Layer 1 + 2**.

### **What happens here:**

- Frames transmitted between devices on the same network
- Uses MAC addresses
- Physical transmission: WiFi, Ethernet, fiber

### **Things you MUST know:**

- MAC addresses
- ARP
- Switches vs hubs
- WiFi monitor mode

### **Attacks on this layer:**

✔ ARP Poisoning  
✔ MAC Spoofing  
✔ WiFi Deauthentication  
✔ Packet injection  
✔ Switch spoofing

### **Tools:**

- `macchanger`
- `ettercap`
- `bettercap`
- Aircrack-ng
- Wireshark

---

# 🟩 **Layer 2 — Internet Layer (IP Layer)**

Equivalent to **OSI Layer 3**.

### **What happens here:**

- Adds source and destination **IP addresses**
- Handles routing between networks
- Finds the path to send packets

### **Key protocols:**

- IP
- ICMP (ping)
- ARP (connects IP to MAC)

### **Attacks on this layer:**

✔ IP spoofing  
✔ ICMP flooding  
✔ MITM via ARP poisoning  
✔ Routing attacks  
✔ VPN bypass techniques

### **Tools:**

- `traceroute`
- `ip route`
- `arpspoof`
- Wireshark
- `tcpdump`

---

# 🟧 **Layer 3 — Transport Layer**

Equivalent to **OSI Layer 4**.

This is where **TCP** and **UDP** live.

### **TCP: (Reliable & Connection-based)**

- 3-way handshake (SYN → SYN/ACK → ACK)
- Guarantees packet delivery
- Used for: HTTP, SSH, FTP, SMTP, HTTPS

### **UDP: (Fast & Connectionless)**

- No handshake
- No reliability
- Used for: DNS, VoIP, gaming

---

### **Transport Layer Attacks:**

✔ **Port Scanning (Nmap)**  
✔ **SYN Flood (DoS attack)**  
✔ **UDP Flood**  
✔ **TCP spoofing**  
✔ **Packet manipulation**  
✔ **Session hijacking**  
✔ **RST injection**

### **Tools:**

- Nmap
- Hping3
- Netcat
- Scapy
- Wireshark

🔥 This layer is EXTREMELY IMPORTANT for penetration testing.

---

# 🟨 **Layer 4 — Application Layer**

Equivalent to **OSI Layer 5–7**.

All "hacker favorite" things live here:

- HTTP & HTTPS
- DNS
- SSH
- FTP
- SMTP
- APIs
- Browsers

### **Attacks:**

✔ SQL Injection  
✔ XSS  
✔ CSRF  
✔ SSRF  
✔ Directory Traversal  
✔ Command Injection  
✔ Broken Authentication  
✔ File Upload Exploits

### **Tools:**

- Burp Suite
- SQLmap
- Nikto
- Browser DevTools

🔥 **99% of bug bounties are here.**

---

# 🧠 **How Packets Actually Flow (Step-by-Step)**

Here’s what happens when you visit a website:

### **1️⃣ Application Layer**

Your browser sends:

```
GET /index.html HTTP/1.1 Host: example.com
```

### **2️⃣ Transport Layer**

- Browser chooses **TCP**
- Opens connection to port **80** or **443**
- Performs the **3-way handshake**

### **3️⃣ Internet Layer**

- Adds source/destination IP  
    Example:

`Source IP: 192.168.1.20 Dest IP: 93.184.216.34`

### **4️⃣ Network Access Layer**

- Converts packet into **frames**
- Uses MAC address to reach the router

Then the router repeats similar steps until data reaches the server.

---

# 📌 **How Hackers Use TCP/IP Internally**

|Layer|Hacker Actions|
|---|---|
|App|exploit web apps|
|Transport|scan ports, hijack sessions|
|Internet|spoof IP, route attacks|
|Network Access|MITM, ARP spoof|

---

# 🎯 Final Quick Summary (For Memory)

**TCP/IP = actual internet**  
**OSI = only for understanding concepts**

- **Layer 4 (Transport)** → attackers scan, flood, hijack
- **Layer 3 (Internet)** → attackers spoof IP, reroute packets
- **Layer 1–2 (Link)** → attackers do MITM, ARP poisoning
- **Layer 7 (App)** → attackers break websites