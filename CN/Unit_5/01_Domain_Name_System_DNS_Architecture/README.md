# Module 01: Domain Name System (DNS) Architecture

> **Course:** Computer Networks (BCS603) — Unit 5: Application Layer  
> **Source Material:** Gateway Classes (Dr. Nidhi Parashar Ma'am) Slides 5–13  
> **Topic:** DNS Architecture, Hierarchical Name Space, Recursive vs Iterative Resolution, Resource Records & Caching  

---

## 1. Domain Name System (DNS) Overview

### 1.1 Kyun Zaroorat Padi DNS Ki? (Motivation & Core Purpose)
Internet par har ek machine ko identify karne ke liye **IP Address** (jaise `142.250.190.46` for Google) use hota hai. Lekin insaan ke liye numerical IP addresses yaad rakhna lagbhag impossible hai. Humein human-readable domain names (e.g., `www.google.com`, `www.aktu.ac.in`) yaad rehte hain.
- **DNS ek Distributed, Hierarchical Database Engine hai** jo human-friendly domain names ko machine-readable binary/decimal IP addresses mein translate karta hai.
- **Port Number & Transport Layer Protocol:**
  - **UDP Port 53:** Normal DNS queries aur replies ke liye use hota hai (fast, lightweight, single-packet query $\le 512$ bytes).
  - **TCP Port 53:** Zone transfers (primary aur secondary DNS server ke beech database sync) aur jab response 512 bytes se exceed kare.

```
+------------------+     DNS Query: www.aktu.ac.in      +-------------------+
|   Client Host    | ---------------------------------> |    DNS Server     |
|   (Web Browser)  | <--------------------------------- |    (Port 53)      |
+------------------+     DNS Reply: 14.139.233.10       +-------------------+
```

---

## 2. Hierarchical Domain Name Space

DNS ka database centralized nahi hai (agar centralized hota to single point of failure aur global bottleneck ban jata). Isliye ise ek **Inverted Tree Structure** ke form mein organize kiya gaya hai:

```
                          [ . ] (Root Domain)
                         /     \         \
                      .com     .edu      .in (TLD - Top Level Domains)
                     /   \       \         \
                google  amazon   mit      aktu.ac (Second-Level Domains)
                 /                          \
               www                          www (Subdomains / Hosts)
```

### 2.1 Three Main Divisions of Domain Name Space (AKTU Exam Question)
1. **Generic Domains (gTLD):** Organizations ke nature ke according define hote hain:
   - `.com`: Commercial entities (e.g., amazon.com)
   - `.edu`: Educational institutions (e.g., mit.edu)
   - `.gov`: Government organizations (e.g., india.gov)
   - `.mil`: Military installations
   - `.org`: Non-profit organizations (e.g., wikipedia.org)
   - `.net`: Network support centers / ISPs
2. **Country Domains (ccTLD):** 2-letter country code ke basis par divide hote hain:
   - `.in`: India, `.us`: United States, `.uk`: United Kingdom, `.jp`: Japan, `.au`: Australia.
3. **Inverse Domains (PTR / Reverse DNS):**
   - Jab IP Address pata ho aur Domain Name find karna ho (Pointer Query). Yeh security verification aur spam detection mein use hota hai (`in-addr.arpa` domain).

---

## 3. DNS Resolution Mechanics: Recursive vs Iterative

Jab user browser mein `https://www.aktu.ac.in` type karta hai, to translation process step-by-step kaise perform hota hai?

### 3.1 Step-by-Step Resolution Flow
1. **Browser / OS Cache:** Sabse pehle local browser cache aur operating system `hosts` file check hoti hai.
2. **Local DNS Server (Resolver):** Agar cache mein entry nahi hai, to client apne ISP / Local DNS server ko query bhejta hai.
3. **Root DNS Server (`.`):** Local DNS server Root server ko contact karta hai. Root server exact IP nahi janta, lekin `.in` TLD server ka address de deta hai.
4. **TLD DNS Server (`.in`):** Local DNS server `.in` server ko query bhejta hai. TLD server `aktu.ac.in` ke Authoritative server ka referral deta hai.
5. **Authoritative DNS Server:** Yeh actual domain owner ka server hota hai jiske paas original mapping hoti hai. Yeh `www.aktu.ac.in` ka final IP address (`14.139.233.10`) return karta hai.
6. **Local Cache & Client Reply:** Local DNS server is IP ko apne cache mein save karta hai (with TTL) aur client browser ko bhej deta hai.

### 3.2 Recursive vs Iterative Query Comparison (AKTU Favorite)

| Parameter | Recursive Query | Iterative Query |
| :--- | :--- | :--- |
| **Definition** | Resolver server se request karta hai: *"Mujhe complete final IP la kar do, main intermediate lookup nahi karunga."* | Server resolver se kehta hai: *"Mujhe exact IP nahi pata, lekin agla behtar server yeh raha, khud jao aur pucho."* |
| **Workload Location** | Receiving DNS server par heavy load hota hai kyunki use pure internet par chain traverse karni padti hai. | Client / Local DNS server par load hota hai; authoritative server sirf referral address dekar free ho jata hai. |
| **Typical Usage** | Client (Browser) se Local DNS Server ke beech. | Local DNS Server se Root, TLD, aur Authoritative servers ke beech. |

---

## 4. DNS Caching & Time-To-Live (TTL)

- **Caching:** Jab bhi koi DNS response pass hota hai, Local DNS Server aur Host use temporary memory mein store kar lete hain. Agli baar same domain request aane par global network traversal zero ho jata hai.
- **Time-To-Live (TTL):** Har DNS Resource Record ke sath ek 32-bit integer hota hai jo seconds mein cache validity define karta hai:
  $$\text{Cache Expiry} = \text{Timestamp}_{\text{received}} + \text{TTL}$$
  TTL expire hote hi record discard ho jata hai, taaki agar server ka IP change hua ho to stale/purana IP user ko na mile.

---

## 5. DNS Resource Records (RR) Anatomy

DNS database plain text nahi hota, yeh structured Resource Records mein store hota hai:
$$\text{Format:} \quad \langle \text{Name}, \text{Value}, \text{Type}, \text{TTL} \rangle$$

| Record Type | Description | Practical Example |
| :---: | :--- | :--- |
| **A** | Hostname to IPv4 mapping (32-bit address) | `aktu.ac.in  IN  A  14.139.233.10` |
| **AAAA** | Hostname to IPv6 mapping (128-bit address) | `aktu.ac.in  IN  AAAA  2404:6800:4009::` |
| **CNAME** | Canonical Name (Alias to actual domain) | `www.aktu.ac.in  IN  CNAME  aktu.ac.in` |
| **MX** | Mail Exchange server for domain (with priority) | `aktu.ac.in  IN  MX  10  mail.aktu.ac.in` |
| **NS** | Authoritative Name Server for zone | `aktu.ac.in  IN  NS  ns1.aktu.ac.in` |
| **PTR** | Pointer record for reverse lookup (IP $\to$ Domain) | `10.233.139.14.in-addr.arpa  IN  PTR  aktu.ac.in` |
| **SOA** | Start of Authority (zone admin, serial number) | Defines primary server, admin email, refresh rates |

---

## 6. Vector Architecture Diagram

![DNS Architecture](diagrams/transport_layer_ports_and_multiplexing.svg)

---

## 7. AKTU Semester Exam PYQ Corner

> **AKTU Question (2018-19, 10 Marks):**  
> *"What is the purpose of Domain Name System? Discuss the three main divisions of domain name space. Differentiate between recursive and iterative resolution."*  
>  
> **Exam Tip:** DNS answer likhte waqt Inverted Tree diagram zaroor banayein (Root $\to$ TLD $\to$ SLD $\to$ Host), UDP Port 53 mention karein, aur 3 divisions (Generic, Country, Inverse) ko tabular format mein explain karein.
