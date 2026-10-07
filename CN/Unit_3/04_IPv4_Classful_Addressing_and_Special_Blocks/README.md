# Module 04: IPv4 Classful Addressing & Special Purpose Blocks

## 1. IPv4 Addressing Foundations
IPv4 address ek **32-bit (4-Byte)** universal logical address hota hai jo internetwork par connected har network interface card (NIC) ko uniquely identify karta hai.

- **Total Address Space:** $2^{32} = 4,294,967,296$ addresses (~4.3 Billion).
  $$	ext{Binary: } [11000000]_{192} . [10101000]_{168} . [00000001]_{1} . [00001010]_{10} \implies \mathbf{192.168.1.10}$$

---

## 2. The Classful Addressing Architecture
Original Internet architecture me address space ko 5 classes me divide kiya gaya tha: **Class A, B, C, D, aur E**.

```
Class A : [0]  Network (7 bits)   | Host ID (24 bits = 16.7M hosts)
Class B : [10] Network (14 bits)  | Host ID (16 bits = 65,534 hosts)
Class C : [110] Network (21 bits) | Host ID (8 bits = 254 hosts)
Class D : [1110] Multicast Group Address (28 bits)
Class E : [1111] Reserved for Experimental / Future use
```

### 2.1 Class Characteristics Table:

| Class | Leading Bits | 1st Octet Decimal Range | NetID Bits | HostID Bits | Total Networks | Usable Hosts per Network ($2^H - 2$) | Default Subnet Mask |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **A** | `0` | $1 - 126$ ($0$ & $127$ reserved) | 8 bits (7 net) | 24 bits | $2^7 - 2 = 126$ | $2^{24} - 2 = \mathbf{16,777,214}$ | `255.0.0.0` (`/8`) |
| **B** | `10` | $128 - 191$ | 16 bits (14 net) | 16 bits | $2^{14} = 16,384$ | $2^{16} - 2 = \mathbf{65,534}$ | `255.255.0.0` (`/16`) |
| **C** | `110` | $192 - 223$ | 24 bits (21 net) | 8 bits | $2^{21} = 2,097,152$ | $2^8 - 2 = \mathbf{254}$ | `255.255.255.0` (`/24`) |
| **D** | `1110`| $224 - 239$ | — | — | — (Multicast) | — (Multicast Group) | None |
| **E** | `1111`| $240 - 255$ | — | — | — (Reserved) | — (Experimental/R&D) | None |

---

## 3. Why Subtract 2 in Usable Hosts ($2^H - 2$)?
Har IP network me do specific addresses kisi host interface ko assign **nahi kiye ja sakte**:
1. **Network Address (Host ID = All 0s):**
   - Pure network ko refer karne ke liye use hota hai (e.g., `192.168.1.0`).
2. **Directed Broadcast Address (Host ID = All 1s):**
   - Us network ke sabhi hosts ko ek sath message bhejne ke liye use hota hai (e.g., `192.168.1.255`).

Isliye usable host capacity hamesha hoti hai:
$$\mathbf{	ext{Usable Hosts} = 2^{	ext{Host Bits}} - 2}$$

---

## 4. Special-Purpose IPv4 Address Blocks

```
+-------------------------------------------------------------------------------------------------+
| Special Address Block    | Scope / Destination            | Router Forwarding Action           |
+-------------------------------------------------------------------------------------------------+
| 0.0.0.0 / 8              | "This Host" (Bootstrapping)    | Never forwarded                    |
| 127.0.0.0 / 8            | Loopback / Localhost           | Never leaves host NIC stack        |
| 255.255.255.255          | Limited Broadcast (Local LAN)  | Blocked by routers (NEVER crosses) |
| NetID + All 1s           | Directed Broadcast             | Forwarded to destination network   |
| 169.254.0.0 / 16         | APIPA (Auto-IP on DHCP fail)   | Never forwarded across routers     |
+-------------------------------------------------------------------------------------------------+
```

### 4.1 Loopback Block (`127.0.0.0/8`):
- `127.0.0.1` se lekar `127.255.255.255` tak.
- Jab koi host `127.0.0.1` par packet bhejta hai, to OS ka network stack packet ko physical cable par bhejne ki bajay internally wapas input queue me inject kar deta hai.
- **Use:** Local client-server software testing (e.g., local web server `http://localhost:8080`).

---

## 5. RFC 1918 Private IP Address Blocks
Internet par public IPv4 exhaustion ko delay karne ke liye IETF ne teen address blocks **Private Networks** ke liye reserve kiye:

1. **Class A Private Block:**
   `10.0.0.0` to `10.255.255.255` (`10.0.0.0/8`, Total = $1$ Class A net = $16,777,216$ IPs).
2. **Class B Private Block:**
   `172.16.0.0` to `172.31.255.255` (`172.16.0.0/12`, Total = $16$ contiguous Class B nets = $1,048,576$ IPs).
3. **Class C Private Block:**
   `192.168.0.0` to `192.168.255.255` (`192.168.0.0/16`, Total = $256$ contiguous Class C nets = $65,536$ IPs).

- **Non-Routable Property:** Public internet routers in private addresses ko route nahi karte aur drop kar dete hain. Inhe internet access karne ke liye **NAT (Network Address Translation)** ki zaroorat hoti hai.

---

## 6. Major Flaws of Classful Addressing (The Motivation for CIDR)
Classful addressing bohot inefficient thi:
- Ek company jise 300 IP addresses chahiye the, use Class C (254 hosts) chhota padta tha, isliye use pura Class B network (65,534 hosts) assign kiya jata tha!
- Company 300 IP use karti thi aur baaki **65,234 IP addresses permanently waste ho jaate the**!
- Is massive wastage ke karan 1993 me **Classless Addressing (CIDR)** introduce kiya gaya.
