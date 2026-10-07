# Module 02: Network Topologies & Design Trade-offs

## 1. Topologies ka Parichay
Network Topology kisi computer network ke devices (nodes) aur unke connecting physical links ke geometric arrangement ya layout ko darshata hai. Topologies ko do perspectives se analyze kiya jata hai:
1. **Physical Topology:** Cables aur hardware ka actual physical layout.
2. **Logical Topology:** Data path aur flow jis tarike se packets travel karte hain.

---

## 2. Mathematical Comparison Matrix

Agar kisi network me $n$ nodes hain:

| Parameter | Mesh Topology | Star Topology | Bus Topology | Ring Topology | Tree / Hybrid Topology |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Physical Links** | $rac{n(n-1)}{2}$ | $n$ | $1 	ext{ backbone} + n 	ext{ drops}$ | $n$ | Hierarchical ($n-1$ tree links) |
| **I/O Ports per Node** | $n - 1$ | $1$ | $1 	ext{ tap/transceiver}$ | $2$ (In & Out) | $1$ per leaf node, Multi on hubs |
| **Fault Tolerance** | Maximum (Robust) | Good (1 cable cut affects only 1 node) | Worst (Backbone break stops whole bus) | Poor (Single break breaks ring) | Good isolation within sub-branches |
| **Single Point of Failure** | None | Central Hub / Switch | Backbone cable / Terminator | Any repeater / cable link | Root switch / Central backbone |
| **Cabling Expense** | Highest | Moderate | Lowest | Low | Moderate to High |
| **Installation Difficulty** | Most Complex | Easy (Plug & Play) | Easy initially | Moderate | Moderate to High |

---

## 3. Topologies ka Deep Dive

### 3.1 Mesh Topology (Fully Connected Network)
- **Concept:** Har ek device har dusri device ke sath direct dedicated point-to-point link se judi hoti hai.
- **Formulas:**
  - Total Links: $L = rac{n(n-1)}{2}$
  - Ports per device: $P = n - 1$
  - Example: Agar $n = 6$ nodes hain, to links $= rac{6 	imes 5}{2} = 15$, aur har computer par 5 network cards (ports) chahiye!
- **Advantages:**
  - *No Traffic Congestion:* Dedicated links hone se link share nahi hota.
  - *Robustness:* Ek link break hone par sirf un do computers ka direct communication rukta hai, baaki network 100% chalta rehta hai.
  - *Security & Privacy:* Data sirf sender aur receiver ke dedicated link par jata hai, teesra koi sniff nahi kar sakta.
  - *Easy Fault Isolation:* Kharab link turant identify ho jata hai.
- **Disadvantages:**
  - Massive cabling cost aur hardware cost ($n-1$ I/O ports har system par).
  - Practical only for small number of nodes ya critical military/nuclear backbones.

### 3.2 Star Topology (Modern Ethernet Standard)
- **Concept:** Sabhi devices ek central controller (Hub ya Switch) se dedicated point-to-point link ke through connect hoti hain. Devices aapas me directly communicate nahi karti; har transmission central device ke through route hota hai.
- **Formulas:** Links $= n$, Ports per node $= 1$.
- **Advantages:**
  - Less expensive than mesh.
  - Easy to install and reconfigure. Kisi naye node ko add karne ke liye sirf central hub me ek wire plug karna hota hai.
  - Robust: Agar ek device ki cable break ho jaye to sirf wahi device disconnect hoti hai, baaki network normal chalta hai.
- **Disadvantages:**
  - *Single Point of Failure:* Agar central hub/switch fail ho gaya to pura network crash ho jata hai.
  - Cable requirement bus topology se zyada hoti hai.

### 3.3 Bus Topology (Multipoint Backbone)
- **Concept:** Ek lambi common cable (Backbone) hoti hai jise drop lines aur taps (BNC T-connectors) ke zariye sabhi nodes share karte hain. Cable ke dono ends par signal reflection rokne ke liye **Terminators** lage hote hain.
- **Advantages:** Minimum cabling requirement, low initial cost.
- **Disadvantages:**
  - Difficult reconnection and fault isolation.
  - Signal attenuation: Lambi wire me signal degrade hota hai.
  - Cable break anywhere collapses the entire network.
  - Heavy traffic me collision bahut badh jata hai.

### 3.4 Ring Topology
- **Concept:** Har device apne do immediate neighbors ke sath dedicated point-to-point link banati hai. Data circular fashion me ek disha me (unidirectional) travel karta hai. Har node me ek **Repeater** laga hota hai jo bit ko regenerate karta hai.
- **Token Passing:** Collision avoid karne ke liye ring me ek special frame (Token) ghumta hai. Jiske paas token hoga wahi transmit kar sakta hai.
- **Dual Ring Solution (FDDI):** Single point of failure ko solve karne ke liye counter-rotating secondary ring use ki jati hai.

### 3.5 Tree & Hybrid Topologies
- **Tree Topology:** Star topologies ka hierarchical variation. Ek central root hub hota hai jisse secondary hubs jude hote hain (e.g., Campus networks).
- **Hybrid Topology:** Do ya do se adhik alag topologies ka combination (e.g., Star-Bus ya Star-Ring).

---

## 4. AKTU Solved Numerical
**Question (AKTU 2023-24):** Ek office me 8 computers hain.
1. Mesh topology me kitne physical cables aur total I/O ports lagenge?
2. Star topology me kitne cables lagenge?

**Solution:**
Yahan $n = 8$.
1. **Mesh Topology:**
   - Total physical links $= rac{n(n-1)}{2} = rac{8 	imes 7}{2} = 28 	ext{ cables}$.
   - Har system par ports $= n - 1 = 7 	ext{ ports}$.
   - Total network ports $= 8 	imes 7 = 56 	ext{ ports}$.
2. **Star Topology:**
   - Total cables $= n = 8 	ext{ cables}$.
   - Har system par port $= 1 	ext{ port}$. Hub par 8 ports required.
