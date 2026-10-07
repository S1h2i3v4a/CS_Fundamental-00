# Module 07: Addressing in Computer Networks

## 1. Computer Networks ke 4 Addressing Levels

TCP/IP network architecture me data communication ko facilitate karne ke liye 4 distinct addressing levels use hote hain:

| Address Level | Corresponding Layer | Address Length | Typical Format | Scope of Delivery | Mutable across Path? |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Physical (MAC) Address** | Data Link Layer | **48 bits** (6 Bytes) | Hexadecimal (`00:1A:2B:3C:4D:5E`) | Hop-to-Hop (Node-to-Node) | **YES**, changes at every router hop |
| **Logical (IP) Address** | Network Layer | **32 bits** (IPv4) / **128 bits** (IPv6) | Dotted-decimal (`192.168.1.1`) | Source-to-Destination (Host-to-Host) | **NO**, remains constant end-to-end |
| **Port Address** | Transport Layer | **16 bits** (2 Bytes) | Decimal integer (0 to 65535) | End-to-End (Process-to-Process) | Constant for specific socket session |
| **Specific Address** | Application Layer | Variable | URL, Email, FQDN | User interface & service discovery | Translated to IP via DNS |

---

## 2. Deep Dive into Addressing Levels

### 2.1 Physical / MAC Address
- Hardware network interface card (NIC) ki ROM me manufacturer dwara hardcode kiya jata hai (isliye ise **Burned-In Address / Hardware Address** bhi kehte hain).
- Structure of 48-bit MAC Address:
  - First 24 bits: **OUI (Organizationally Unique Identifier)** — IEEE dwara manufacturer ko assign kiya jata hai (e.g., Intel, Cisco, Realtek).
  - Last 24 bits: **NIC Specific Serial Number** — Manufacturer dwara card ko uniquely assign kiya jata hai.
- **Hop-to-Hop Mutation:** Jab packet host A se router R1 aur phir host B tak travel karta hai:
  - Frame 1: Source MAC = Host A, Destination MAC = Router R1 interface.
  - Frame 2: Source MAC = Router R1 exit interface, Destination MAC = Host B.
  - IP addresses remain unchanged!

### 2.2 Logical / IP Address
- Physical network se independent universal addressing scheme.
- Har internet-connected host ko uniquely identify karta hai.
- **IPv4 (32 bits):** 4 bytes separated by dots (e.g., `172.16.254.1`). Total address space: $2^{32} pprox 4.3 	ext{ billion}$.
- **IPv6 (128 bits):** 16 bytes separated by colons in hex notation (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`). Total address space: $2^{128}$.
- Structure: Divided into **NetID (Network identifier)** aur **HostID (Host identifier)** using Subnet Masks.

### 2.3 Port Address (16 bits)
- Ek host machine par ek sath multiple applications run kar sakti hain (e.g., Browser, Zoom call, Telegram).
- Transport layer ko yeh pata lagane ke liye ki incoming packet kis application ka hai, Port Numbers use hote hain ($2^{16} = 65,536$ total ports):
  1. **Well-Known Ports (0 to 1023):** IANA dwara standard universal services ke liye reserved:
     - Port 20, 21: FTP
     - Port 22: SSH
     - Port 23: Telnet
     - Port 25: SMTP
     - Port 53: DNS
     - Port 80: HTTP
     - Port 443: HTTPS
  2. **Registered Ports (1024 to 49151):** Proprietary applications (e.g., MySQL 3306, Microsoft SQL 1433, Oracle 1521).
  3. **Dynamic / Private / Ephemeral Ports (49152 to 65535):** Client operating system dwara temporary outbound connections ke liye randomly allocate kiye jate hain.
- **Socket Address:**
  $$	ext{Socket Address} = 	ext{IP Address} + 	ext{Port Number} \quad (	ext{e.g., } 192.168.1.50:8080)$$

---

## 3. Delivery Scenarios Compared (AKTU PYQ Favorite)
1. **Hop-to-Hop Delivery (Data Link Layer):** Frame ko ek physical node se uske immediate adjacent physical node tak transmit karta hai using MAC addresses.
2. **Host-to-Host Delivery (Network Layer):** Packet ko original source computer se final target computer tak deliver karta hai across multiple routers using IP addresses.
3. **Process-to-Process Delivery (Transport Layer):** Target computer ke andar chal rahe specific running process (thread/application) tak message deliver karta hai using Port addresses.
