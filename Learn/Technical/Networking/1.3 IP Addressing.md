## 📄 **1.3 IP Addressing**

### 🔹 IPv4

|Property|Value|
|---|---|
|Size|32-bit|
|Format|`A.B.C.D`|
|Total addresses|~4.29 billion|
|Example|`192.168.1.5`|

📌 **How IPv4 works**

- Each device on a network must have a **unique IP**
- IP addresses are **not permanent** — DHCP can assign dynamically
- Split into **Network ID** + **Host ID**

🔸 Example  
`192.168.1.5 / 24`

- Network part: `192.168.1`
- Host part: `5`

---

### 🔹 IPv6

|Property|Value|
|---|---|
|Size|128-bit|
|Format|8 hex groups|
|Example|`2001:0db8:85a3:0000:0000:8a2e:0370:7334`|
|Purpose|Solve IPv4 exhaustion, better security|

📌 **IPv6 Security Advantage**

- Supports encryption and authentication built-in (IPSec)

---

### 🔹 Public vs Private IP

|Type|Visibility|Used In|Example|
|---|---|---|---|
|Public|Internet|Externally accessible|`103.31.45.18`|
|Private|Local Network|LAN only|`192.168.x.x`, `10.x.x.x`, `172.16–31.x.x`|

💀 **Hacker Insight**

- Attacks normally target **public IP**
- **Private IP leaks** can reveal internal structure

---

### 🔹 Classes & CIDR

|Class|Range|Networks|Default Mask|
|---|---|---|---|
|A|0–127|Very large|`/8`|
|B|128–191|Medium|`/16`|
|C|192–223|Small|`/24`|
|D|224–239|Multicast|—|
|E|240–255|Experimental|—|

CIDR = **Classless Inter-Domain Routing**

- Notation: `/n` (n = number of bits in network portion)
- Example: `192.168.1.7 / 26` → first 26 bits = network

🧠 For hackers:  
CIDR helps recognize how many **hosts** & **subnets** exist → useful in network mapping.