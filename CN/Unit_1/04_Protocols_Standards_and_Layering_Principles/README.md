# Module 04: Protocols, Standards and Layering Principles

## 1. Protocol ke 3 Key Elements
Ek network protocol communication rules aur conventions ka set hota hai. Har protocol ke teen core components hote hain:
1. **Syntax (Data Format):** Structure ya format of data, yaani data bits kaise arrange honge.
   - Example: Pehle 8 bits sender address, agle 8 bits receiver address, aur baaki 48 bits data payload honge.
2. **Semantics (Meaning of Bits):** Har section/field ke bits ka kya matlab hai aur unpar kya action lena hai.
   - Example: Agar address field me all `1`s hain, to iska matlab Broadcast address hai; system copy karke sabhi processes ko dega.
3. **Timing (Speed & Sequencing):** Data kab bheja jana chahiye aur kitni speed se transfer hoga.
   - Example: Flow control mechanisms (sender fast hai aur receiver slow hai, to speed match karna taaki data buffer overflow na ho).

---

## 2. Standards: De Jure vs De Facto

| Category | Meaning | Origin / Authority | Real-world Example |
| :--- | :--- | :--- | :--- |
| **De Facto Standards** | "By Fact" ya "By Convention" | Kisi formally approved body ke bina, market adoption aur historical popularity se standard ban gaya. | TCP/IP protocol suite (initially ARPANET deployment), QWERTY keyboard layout, IBM PC architecture. |
| **De Jure Standards** | "By Law" ya "By Regulation" | Formal recognized standard bodies dwara officially research, review aur legislate karke approve kiya gaya. | OSI Reference Model (ISO 7498), IEEE 802.3 (Ethernet), ITU-T V.90 modem standard. |

---

## 3. Leading Standards Organizations
AKTU exam me 2-mark ya 5-mark short note ke liye essential organizations:
- **ISO (International Organization for Standardization):** Global federation of national standards bodies. Designed OSI 7-layer reference model.
- **ITU-T (International Telecommunication Union - Telecommunication Standardization Sector):** UN specialized agency for telecom standards (e.g., V-series modems, X.25, X.400).
- **IEEE (Institute of Electrical and Electronics Engineers):** Computer communication ke physical aur data link layer standards (LAN/MAN):
  - *IEEE 802.3:* Standard for Ethernet.
  - *IEEE 802.11:* Standard for Wireless LAN (Wi-Fi).
  - *IEEE 802.15:* Wireless Personal Area Network (Bluetooth / Zigbee).
- **IETF (Internet Engineering Task Force):** Open international community of network designers and researchers. Internet protocols ko develop karti hai via **RFC (Request for Comments)** documents.
- **ANSI (American National Standards Institute):** US standards organization (e.g., ASCII character encoding).

---

## 4. Layering Principles & Service Access Points (SAPs)

### 4.1 Layered Architecture Kyun Chahiye?
- **Modularity:** Complex communication tasks ko independent manageable layers me divide karta hai.
- **Abstraction & Information Hiding:** Layer $N$ ko sirf isse matlab hota hai ki Layer $N-1$ use kya service deti hai, na ki wo service internally kaise implement hui hai.
- **Ease of Maintenance:** Agar physical cable ko copper se optical fiber me upgrade kiya jaye, to application layer (e.g., Browser) ko modify nahi karna padta.

### 4.2 Services vs Protocols
- **Service:** Ek layer apne theek upar wali layer ko jo capability/functionality provide karti hai use service kehte hain (Vertical interface communication).
- **Protocol:** Do alag-alag machines par baithkar kaam karne wali same layers (Peer entities) ke beech conversation rules ko protocol kehte hain (Horizontal virtual communication).

### 4.3 Service Access Point (SAP)
SAP do adjacent layers ke beech ka logical interface point hota hai jahan lower layer upper layer ko service offer karti hai:
- Network layer aur Transport layer ke beech: **Transport SAP (TSAP) ya Port Number** (e.g., Port 80 for HTTP).
- Data Link layer aur Network layer ke beech: **Network SAP (NSAP) ya IP Protocol Field / EtherType** (e.g., EtherType `0x0800` for IPv4).
- Physical layer aur Data Link layer ke beech: **Physical SAP (MAC Service Interface)**.

### 4.4 Service Primitives (Operations)
Adjacent layers ke beech data exchange 4 basic primitives se hota hai:
1. **Request:** Upper layer lower layer se service execute karne ko kehti hai.
2. **Indication:** Lower layer receiving side par upper layer ko notify karti hai ki event hua hai.
3. **Response:** Upper layer receiving side par request acknowledge karti hai.
4. **Confirm:** Lower layer sending side par original requester ko acknowledge karti hai ki service complete ho gayi.
