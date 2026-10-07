# Module 03: Network Categories, Internet Structure & ISPs

## 1. Geographical Classification of Networks

| Network Category | Full Form | Geographic Scope | Typical Transmission Media | Data Rate (Typical) | Ownership |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **PAN** | Personal Area Network | &lt; 10 meters (Single person workspace) | Bluetooth, Zigbee, Infrared, USB | 1 to 24 Mbps | Private |
| **LAN** | Local Area Network | Room, Office, Building, Campus (up to 1-2 km) | Twisted Pair (UTP/STP), Wi-Fi (802.11), Fiber | 100 Mbps to 10 Gbps | Single Organization |
| **MAN** | Metropolitan Area Network | Entire City or Town (5 to 50 km) | Optical Fiber (SONET/SDH), Coaxial, Wireless | 100 Mbps to 1 Gbps | Consortium / Public Utility |
| **WAN** | Wide Area Network | State, Country, Continent, Global (> 100 km) | Submarine Optical Fiber, Satellite Links, Microwave | Variable (Mbps to 100s Gbps) | Multiple Telecom Operators |
| **WLAN** | Wireless LAN | Building or hotspot area | Radio frequency (2.4 GHz / 5 GHz / 6 GHz) | 54 Mbps to 9.6 Gbps (Wi-Fi 6) | Private / Public hotspot |

---

## 2. Organization of the Global Internet
Internet kisi ek company ya government ki property nahi hai. Yeh **"Network of Networks"** hai jo hierarchical structure me organize hota hai.

### 2.1 3-Tier ISP (Internet Service Provider) Hierarchy
1. **Tier 1 ISPs (National & International Backbone Providers):**
   - Internet ki backbone banate hain.
   - Continental aur trans-oceanic submarine optical fiber cables own karte hain.
   - Inhe internet access karne ke liye kisi ko paise nahi dene hote (**Transit-Free Networks**).
   - Ek doosre ke sath **Free Peering Agreements** karte hain (unrestricted traffic exchange).
   - *Global Examples:* AT&T, Lumen Technologies (CenturyLink), Tata Communications, Verizon, NTT, Telia Carrier.
2. **Tier 2 ISPs (Regional Service Providers):**
   - Kisi specific state ya desh ke multi-city regions ko cover karte hain.
   - Tier 1 ISPs se bandwidth purchase karte hain (**Transit Fee pay karte hain**).
   - Cost bachane ke liye dusre Tier 2 ISPs ke sath **IXP** par traffic peer karte hain.
   - *Indian Examples:* Reliance Jio, Bharti Airtel, Vodafone Idea.
3. **Tier 3 ISPs (Local Access Providers / Last-Mile ISPs):**
   - Retail consumers aur local businesses ko direct internet connection provide karte hain (**Last-Mile Connectivity**).
   - Tier 2 ya Tier 1 se transit buy karte hain.
   - Connectivity options: Fiber to the Home (FTTH), DSL, Cable Broadband, 4G/5G Wireless.
   - *Examples:* ACT Fibernet, Hathway, local cable broadband operators.

---

## 3. Key Internet Interconnection Building Blocks
- **POP (Point of Presence):** ISP ka local access point jahan physical routers aur switches hote hain jisse customers (ya lower-tier ISPs) connect hote hain.
- **IXP (Internet Exchange Point):** Ek neutral physical hub jahan alag-alag ISPs aur Content Delivery Networks (CDNs jaise Google, Netflix, Cloudflare) aapas me direct connection banakar traffic exchange karte hain.
  - *Benefit:* Traffic ko third-party transit provider ke through ghumana nahi padta, jisse latency aur cost dono drastically kam ho jati hain.
- **Peering vs Transit:**
  - **Peering:** Do networks aapas me agreement karte hain ki wo ek dusre ke customers ka traffic free (ya shared cost) exchange karenge.
  - **Transit:** Ek customer network kisi bade provider ko paise deta hai pure global internet tak access pane ke liye.
