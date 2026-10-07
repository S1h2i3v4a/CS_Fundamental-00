# Module 06: Controlled Access & Channelization Protocols

## 1. Classification of Multiple Access Protocols
Multiple Access sublayer ko teen broad categories me classify kiya jata hai:
1. **Random Access (Contention):** ALOHA, CSMA, CSMA/CD, CSMA/CA (Stations compete; collisions possible).
2. **Controlled Access (Collision-Free):** Reservation, Polling, Token Passing (Stations coordinate; zero collisions).
3. **Channelization:** FDMA, TDMA, CDMA (Shared bandwidth mathematically divided).

---

## 2. Controlled Access Protocols

### 2.1 Reservation Method
- Time ko discrete frames me divide kiya jata hai. Har data frame se pehle ek **Reservation Frame** hota hai jisme $N$ stations ke liye $N$ small bit-intervals hote hain.
- Agar station $i$ ko transmit karna hai, to wo slot $i$ me bit `1` send karti hai.
- Reservation interval khatam hone ke baad sabhi stations ko pata chal jata hai ki kin stations ne slot reserve kiya hai. Stations apne ordered sequence me bina collision ke frames transmit karti hain.

### 2.2 Polling (Primary-Secondary Architecture)
Polling centralized master-slave topology par kaam karta hai:
- **Primary Station (Controller):** Link ko control karta hai.
- **Secondary Stations:** Sirf Primary ke order par data bhej ya le sakti hain.
- **Poll Frame:** Primary secondary se poochta hai: *"Kya tumhare paas data hai?"* Secondary data frame bhejti hai ya `NAK` bhejti hai.
- **Select Frame:** Primary data bhejne se pehle poochta hai: *"Kya tum receive karne ke liye ready ho?"* Secondary `ACK` bhejti hai.
- **Drawback:** Primary station failure se pura network down ho jata hai (Single Point of Failure) aur polling overhead efficiency kam karta hai.

### 2.3 Token Passing (Logical Ring Architecture)
Stations ek **Logical Ring** me connected hoti hain (e.g., IEEE 802.5 Token Ring, IEEE 802.4 Token Bus).
- Ek special bit-pattern frame jise **Token** kehte hain, continuously ring me circulate karta hai.
- **Transmission Rule:** Sirf wahi station transmit kar sakti hai jiske paas Token ho!
- Station token ko capture karti hai, apna data frame inject karti hai, aur frame transmit hone ke baad token ko next logical neighbor ko release kar deti hai.
- **Token Hold Time (THT):** Maximum time limit jisme station token hold kar sakti hai taaki channel starvation na ho.

---

## 3. Channelization Protocols: FDMA vs TDMA vs CDMA

```
+-----------------------------------------------------------------------------------------+
| Protocol | Allocation Method         | Guard Mechanism    | Synchronization Needed?     |
+-----------------------------------------------------------------------------------------+
| FDMA     | Distinct Frequency Bands  | Guard Bands (Hz)   | No (Continuous Transmission)|
| TDMA     | Distinct Time Slots       | Guard Times (μs)   | Yes (Precise Clock Sync)    |
| CDMA     | Distinct Orthogonal Codes | Code Orthogonality | Chip-Level Synchronization  |
+-----------------------------------------------------------------------------------------+
```

### 3.1 Frequency Division Multiple Access (FDMA)
Available bandwidth ko non-overlapping frequency bands me divide kiya jata hai. Har station ko ek dedicated channel assign hota hai. Interference avoid karne ke liye bands ke beech **Guard Bands** rakhe jate hain.

### 3.2 Time Division Multiple Access (TDMA)
Pura frequency band sabhi stations share karti hain, lekin different time slots me. Har station apne assigned time slot me data burst transmit karti hai. Frame synchronization maintain karne ke liye **Guard Times** aur preamble bits use hoti hain.

### 3.3 Code Division Multiple Access (CDMA)
CDMA me sabhi stations ek sath, pure frequency spectrum par transmit karti hain! Har station ko ek unique orthogonal mathematical code (**Chip Sequence**) assign kiya jata hai.

---

## 4. Orthogonal Walsh Codes & CDMA Mathematics

### 4.1 Walsh Matrix Construction
Walsh matrices recursive block matrix rule se banti hain:
$$W_1 = [+1]$$
$$W_{2N} = egin{bmatrix} W_N & W_N \ W_N & -W_N \end{bmatrix}$$

For $N = 2$:
$$W_2 = egin{bmatrix} +1 & +1 \ +1 & -1 \end{bmatrix}$$

For $N = 4$:
$$W_4 = egin{bmatrix} +1 & +1 & +1 & +1 \ +1 & -1 & +1 & -1 \ +1 & +1 & -1 & -1 \ +1 & -1 & -1 & +1 \end{bmatrix}$$

Where rows represent chip sequences for 4 stations:
- Station 1: $W_1 = [+1, +1, +1, +1]$
- Station 2: $W_2 = [+1, -1, +1, -1]$
- Station 3: $W_3 = [+1, +1, -1, -1]$
- Station 4: $W_4 = [+1, -1, -1, +1]$

### 4.2 Orthogonality Properties
1. **Self Dot Product (Autocorrelation):**
   $$W_i \cdot W_i = N \quad (	ext{e.g., } 1^2 + 1^2 + 1^2 + 1^2 = 4)$$
2. **Cross Dot Product (Cross-correlation with another code):**
   $$W_i \cdot W_j = 0 \quad (	ext{for } i 
e j)$$

### 4.3 Data Encoding Rules
- Data Bit `0` is represented as $-1$.
- Data Bit `1` is represented as $+1$.
- Idle / Silent (No data) is represented as $0$.

Station $i$ ka transmitted signal vector:
$$S_i = d_i \cdot W_i$$

Composite Channel Signal $C$:
$$C = \sum_{i=1}^{N} S_i = S_1 + S_2 + \dots + S_N$$

### 4.4 Receiver Decoding (Dot Product)
Agar receiver ko Station $k$ ka data decode karna hai, to wo composite signal $C$ ka dot product Station $k$ ke code $W_k$ ke sath nikal kar $N$ se divide karta hai:
$$d_k = rac{C \cdot W_k}{N}$$

Kyunki sabhi doosre stations orthogonal hain ($W_j \cdot W_k = 0$), unke signals zero ho jate hain aur sirf station $k$ ka signal recover hota hai:
$$C \cdot W_k = (d_k W_k + \sum_{j 
e k} d_j W_j) \cdot W_k = d_k (W_k \cdot W_k) + 0 = d_k \cdot N$$

---

## 5. AKTU Core Solved Numerical: 4-Station CDMA Decoding

> **Problem Statement (AKTU Semester Exam 10 Marks):**  
> Four stations $S_1, S_2, S_3, S_4$ share a CDMA channel using the 4-bit Walsh sequences:  
> $W_1 = [+1, +1, +1, +1]$, $W_2 = [+1, -1, +1, -1]$, $W_3 = [+1, +1, -1, -1]$, $W_4 = [+1, -1, -1, +1]$.  
> At a given moment:  
> - Station 1 transmits data bit `1`  
> - Station 2 transmits data bit `0`  
> - Station 3 is silent (no data)  
> - Station 4 transmits data bit `1`  
> 
> 1. Find the composite signal $C$ on the common channel.  
> 2. Show the mathematical calculation to decode the data sent by Station 2 at the receiver.  
> 3. Show how the receiver detects that Station 3 was silent.

### Step-by-Step Solution:

#### 1. Data Bit Conversion:
- $d_1 = 	ext{Bit } 1 \implies +1$
- $d_2 = 	ext{Bit } 0 \implies -1$
- $d_3 = 	ext{Silent} \implies 0$
- $d_4 = 	ext{Bit } 1 \implies +1$

#### 2. Transmitted Vectors:
$$S_1 = (+1) 	imes [+1, +1, +1, +1] = [+1, +1, +1, +1]$$
$$S_2 = (-1) 	imes [+1, -1, +1, -1] = [-1, +1, -1, +1]$$
$$S_3 = (0) 	imes [+1, +1, -1, -1] = [0, 0, 0, 0]$$
$$S_4 = (+1) 	imes [+1, -1, -1, +1] = [+1, -1, -1, +1]$$

#### 3. Composite Channel Signal $C$:
$$C = S_1 + S_2 + S_3 + S_4$$
$$C = [(1 - 1 + 0 + 1), (1 + 1 + 0 - 1), (1 - 1 + 0 - 1), (1 + 1 + 0 + 1)]$$
$$\mathbf{C = [+1, +1, -1, +3]}$$

#### 4. Decoding Data for Station 2:
Receiver calculates dot product $C \cdot W_2$:
$$C \cdot W_2 = [+1, +1, -1, +3] \cdot [+1, -1, +1, -1]$$
$$C \cdot W_2 = (1 	imes 1) + (1 	imes -1) + (-1 	imes 1) + (3 	imes -1)$$
$$C \cdot W_2 = 1 - 1 - 1 - 3 = -4$$

Now divide by $N = 4$:
$$d_2 = rac{-4}{4} = -1 \implies \mathbf{	ext{Data Bit } 0 	ext{ Recovered!}}$$

#### 5. Decoding Data for Station 3 (Silent Detection):
Receiver calculates dot product $C \cdot W_3$:
$$C \cdot W_3 = [+1, +1, -1, +3] \cdot [+1, +1, -1, -1]$$
$$C \cdot W_3 = (1 	imes 1) + (1 	imes 1) + (-1 	imes -1) + (3 	imes -1)$$
$$C \cdot W_3 = 1 + 1 + 1 - 3 = 0$$

Now divide by $N = 4$:
$$d_3 = rac{0}{4} = 0 \implies \mathbf{	ext{Result 0 Confirms Station 3 was SILENT!}}$$
