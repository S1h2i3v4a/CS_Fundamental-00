# Module 01: Network Layer Foundations, Packet Switching & Virtual Circuits vs Datagram

## 1. Responsibilities of the Network Layer (Layer 3)
OSI Reference Model me **Network Layer** ka primary task hota hai packets ko **Source Host se Destination Host** tak end-to-end deliver karna (**Host-to-Host Delivery**), chahe wo hazaron intermediate routers aur heterogeneous networks se hokar guzrein.

```
OSI Layer Responsibilities Comparison:
Data Link Layer : Hop-to-Hop / Node-to-Node delivery (between adjacent nodes on same link using MAC)
Network Layer   : Source-to-Destination / Host-to-Host delivery (across independent networks using IP)
Transport Layer : Process-to-Process / End-to-End delivery (between specific applications using Port)
```

### 1.1 Core Network Layer Services:
1. **Packetizing (Encapsulation & Decapsulation):** Upper layer (Transport layer) ke data stream ya segments ko receive karke Network layer headers attach karke **Datagrams / Packets** banata hai.
2. **Logical Addressing (IPv4 / IPv6):** Global internetwork par uniquely identify karne ke liye har device ko ek 32-bit ya 128-bit universal logical address assign karta hai.
3. **Routing (Control Plane):** Multiple possible paths me se sabse optimal (shortest delay, lowest cost, highest bandwidth) path decide karna using routing algorithms (Dijkstra, Bellman-Ford, OSPF, BGP).
4. **Forwarding / Switching (Data Plane):** Packet ke header ko read karke router ke incoming interface se appropriate outgoing interface par dispatch karna using Forwarding Table.
5. **Fragmentation & Reassembly:** Jab large datagram aise physical network me enter karta hai jiska Maximum Transmission Unit (MTU) chhota ho, to datagram ko multiple smaller fragments me split karna.

---

## 2. Store-and-Forward Packet Switching Architecture
Internet routers **Store-and-Forward** mechanism par operate karte hain:
- Router incoming link se packet ki saari bits ko pehle apne input buffer memory me store karta hai.
- Packet ke header ka checksum verify karta hai. Agar frame corrupt ho, to use silently drop kar deta hai.
- Forwarding table lookup karke destination route find karta hai aur packet ko output link par transmit karta hai.

---

## 3. Connection-Oriented vs Connectionless Network Service

Network Layer do fundamentally different switching paradigms par design ho sakti hai:

```
+-------------------------------------------------------------------------------------------------+
| Paradigm            | Protocol Example     | Circuit Setup? | Path Followed  | Reliability      |
+-------------------------------------------------------------------------------------------------+
| Datagram            | IPv4, IPv6 (Internet)| None (Instant) | Independent    | Best-effort      |
| Virtual Circuit     | ATM, Frame Relay, X.25| Mandatory 3-Way| Pinned / Fixed | Guaranteed order |
+-------------------------------------------------------------------------------------------------+
```

### 3.1 Datagram Networks (Connectionless / The Internet Model)
- **No Setup Phase:** Sender bina kisi prior signaling ya negotiation ke data packet ko network me inject kar deta hai.
- **Independent Routing:** Har datagram independent entity hota hai aur complete Source IP aur Destination IP carry karta hai. Intermediate routers har packet ke liye dynamic independent decision lete hain.
- **Out-of-Order Delivery:** Network me congestion ya link metric changes ke karan Packet 1 path R1-R3 se ja sakta hai jabki Packet 2 path R2-R4 se ja sakta hai. Packet 2 destination par Packet 1 se pehle pahunch sakta hai! (Reassembly aur reordering Transport Layer TCP par chhod di jaati hai).
- **Extreme Robustness:** Agar intermediate router R1 crash ho jaye, to remaining packets automatically R2 se route ho jate hain. Pura session break nahi hota!

### 3.2 Virtual Circuit Networks (Connection-Oriented / The Telecom Model)
- **Three Distinct Phases:**
  1. **VC Setup:** Sender ek special *Setup Frame* bhejta hai. Intermediate switches path ke along entries create karti hain aur ek **Virtual Circuit Identifier (VCI)** assign karti hain.
  2. **Data Transfer:** Saare packets usi pre-established pinned path se travel karte hain. Packets me 32-bit IP ki bajay chhota VCI tag hota hai. Guaranteed in-order arrival!
  3. **VC Teardown:** Data finish hone par *Release Frame* resources (buffer & VCI table) ko free kar deta hai.
- **Vulnerability:** Agar pinned path ka koi router crash ho jata hai, to wo Virtual Circuit terminate ho jata hai aur call drop ho jati hai!

---

## 4. Master 10-Point Comparison: Datagram vs Virtual Circuit

| Feature | Datagram Network (Internet / IP) | Virtual Circuit Network (ATM / X.25) |
| :--- | :--- | :--- |
| **Circuit Setup** | Not required | Mandatory prior setup phase |
| **Addressing Overhead** | Full 32/128-bit Dest IP in every packet | Small 16-bit VCI tag per packet |
| **State Information** | Routers are **Stateless** (No call state) | Routers are **Stateful** (Store per-VC state) |
| **Packet Sequence** | May arrive out-of-order | Strictly in-order delivery guaranteed |
| **Router Failure Impact** | High fault tolerance (Reroutes dynamically) | All VCs passing through crashed router die |
| **Quality of Service (QoS)**| Difficult to guarantee (Best-effort) | Easy to guarantee (Pre-allocated bandwidth) |
| **Congestion Control** | Reactive (Difficult) | Proactive (Call admission control) |
| **Cost & Complexity** | Simple network core, smart end-systems | Complex network core, simple dumb terminals |

---

## 5. Routing vs Forwarding (Control Plane vs Data Plane)

AKTU BCS603 exam me aksar 2-marks ya 5-marks me yeh question poocha jata hai:

```
                     +---------------------------------------+
                     | Routing Algorithm (Control Plane)     |
                     | Determines end-to-end optimal paths   |
                     | (Dijkstra, Bellman-Ford, OSPF, BGP)   |
                     +-------------------+-------------------+
                                         | Updates
                                         v
+------------------------+      +-------------------+      +-------------------------+
| Packet arrives on      | ---> | Forwarding Table  | ---> | Packet dispatched on    |
| Input Port             |      | (Data Plane / HW) |      | Output Port             |
+------------------------+      +-------------------+      +-------------------------+
```

1. **Routing (Control Plane):** Yeh network-wide logic hai jo decide karti hai ki packet source se destination tak kis overall raste se jayega. Yeh software-driven routing algorithms ke zariye routing table build karta hai.
2. **Forwarding (Data Plane):** Yeh local router ka hardware action hai jisme router packet ke destination header ko read karke forwarding table se match karta hai aur packet ko input port se correct output port par switch karta hai (Microsecond level forwarding engine).
