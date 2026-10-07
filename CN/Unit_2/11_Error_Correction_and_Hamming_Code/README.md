# Module 11: Error Correction & Hamming Code Architecture

## 1. Error Detection vs Forward Error Correction (FEC)
- **Error Detection:** Receiver sirf yeh detect karta hai ki frame corrupt hua hai, aur use discard karke sender se retransmission maangta hai (ARQ). (Best for wired/reliable low-error links).
- **Forward Error Correction (FEC):** Receiver bina retransmission maange, khud apne mathematical algorithm ke through corrupted bit ko locate karke **correct** kar leta hai! (Crucial for satellite links, deep-space communication, aur real-time streaming jahan RTT bohot high hota hai).

---

## 2. Hamming Distance Foundations
Do binary codewords ke beech **Hamming Distance $d(x, y)$** un bit positions ki sankhya hoti hai jinme dono bits differ karti hain (i.e., Hamming distance is the number of 1s in $x \oplus y$).

### 2.1 The Two Fundamental Theorems:
1. **To Detect $d$ Errors:**
   Minimum Hamming distance between all valid codewords must be at least:
   $$\mathbf{d_{min} \ge d + 1}$$
   *(E.g., to detect 2 errors, $d_{min} \ge 3$)*
2. **To Correct $t$ Errors:**
   Minimum Hamming distance must be at least:
   $$\mathbf{d_{min} \ge 2t + 1}$$
   *(E.g., to correct a single 1-bit error ($t=1$), $d_{min} \ge 2(1) + 1 = 3$)*

---

## 3. The Redundancy Inequality ($2^r \ge m + r + 1$)
Maan lijiye message me $m$ data bits hain aur hum $r$ redundant parity bits add karte hain. Total transmitted codeword length $n = m + r$.

- Single-bit error hone par codeword ki kisi bhi $n$ bit position me se koi ek bit flip ho sakti hai ($n$ invalid error states).
- Ek state "No Error" ki hoti hai ($1$ state).
- Total states jo $r$ parity bits ko distinguish karni hain: $n + 1 = m + r + 1$.
- $r$ parity bits maximum $2^r$ unique syndromes encode kar sakti hain.

Therefore:
$$\mathbf{2^r \ge m + r + 1}$$

### Redundancy Table:
| Data Bits ($m$) | Min Parity Bits ($r$) | Total Codeword ($n = m + r$) | Codeword Name |
| :--- | :--- | :--- | :--- |
| 1 | 2 ($2^2 \ge 1+2+1=4$) | 3 | Hamming (3, 1) |
| 4 | 3 ($2^3 = 8 \ge 4+3+1=8$) | 7 | **Hamming (7, 4)** |
| 11 | 4 ($2^4 = 16 \ge 11+4+1=16$) | 15 | Hamming (15, 11) |
| 26 | 5 ($2^5 = 32 \ge 26+5+1=32$) | 31 | Hamming (31, 26) |

---

## 4. Hamming (7, 4) Code Construction Rules
Richard Hamming ne 1950 me yeh method develop kiya tha:

### 4.1 Bit Positions:
Codeword positions ko 1 se 7 tak number kiya jata hai:
- **Parity Bits ($p_i$):** Hamesha $2$ ki powers wali positions par aati hain:
  - $p_1$ at Position $1$ ($2^0$)
  - $p_2$ at Position $2$ ($2^1$)
  - $p_4$ at Position $4$ ($2^2$)
- **Data Bits ($d_i$):** Remaining positions par arrange hoti hain:
  - $d_1$ at Position $3$
  - $d_2$ at Position $5$
  - $d_3$ at Position $6$
  - $d_4$ at Position $7$

```
Position:   1    2    3    4    5    6    7
Bit Type:  p1   p2   d1   p4   d2   d3   d4
Binary:   001  010  011  100  101  110  111
```

### 4.2 Parity Bit Equations (Even Parity / XOR):
Har parity bit un positions ko check karti hai jinke binary representation me corresponding bit `1` hoti hai:
- **$p_1$ (Checks positions with LSB = 1: $\{1, 3, 5, 7\}$):**
  $$p_1 \oplus d_1 \oplus d_2 \oplus d_4 = 0 \implies \mathbf{p_1 = d_1 \oplus d_2 \oplus d_4}$$
- **$p_2$ (Checks positions with 2nd bit = 1: $\{2, 3, 6, 7\}$):**
  $$p_2 \oplus d_1 \oplus d_3 \oplus d_4 = 0 \implies \mathbf{p_2 = d_1 \oplus d_3 \oplus d_4}$$
- **$p_4$ (Checks positions with MSB = 1: $\{4, 5, 6, 7\}$):**
  $$p_4 \oplus d_2 \oplus d_3 \oplus d_4 = 0 \implies \mathbf{p_4 = d_2 \oplus d_3 \oplus d_4}$$

---

## 5. Receiver Syndrome Decoding & Bit Correction
Jab receiver codeword $b_1 b_2 b_3 b_4 b_5 b_6 b_7$ receive karta hai, to wo 3-bit **Syndrome ($S_4 S_2 S_1$)** calculate karta hai:
$$S_1 = b_1 \oplus b_3 \oplus b_5 \oplus b_7$$
$$S_2 = b_2 \oplus b_3 \oplus b_6 \oplus b_7$$
$$S_4 = b_4 \oplus b_5 \oplus b_6 \oplus b_7$$

- **Syndrome Interpretation:**
  - If $S_4 S_2 S_1 = 000 \implies \text{No Error! Data is valid.}$
  - If $S_4 S_2 S_1 \ne 000 \implies$ The binary value of $(S_4 S_2 S_1)_2$ directly points to the **Exact Corrupted Bit Position**!
  - **Correction:** Corrupted bit ko invert kar do ($0 \to 1$ or $1 \to 0$)!

---

## 6. AKTU Core Solved Numerical: Encode, Corrupt & Correct

> **Problem Statement (AKTU Semester Exam 10 Marks):**  
> A 4-bit data word `1011` is to be transmitted using an even-parity 7-bit Hamming code.  
> 1. Calculate the values of parity bits $p_1, p_2, p_4$.  
> 2. Construct the transmitted 7-bit Hamming codeword.  
> 3. Suppose bit 6 is flipped during transmission. Show how the receiver calculates the syndrome, identifies the erroneous bit position, and corrects it.

### Step-by-Step Solution:

#### Step 1: Data Bit Allocation:
Data = `1011` $\implies d_1 = 1, d_2 = 0, d_3 = 1, d_4 = 1$.

#### Step 2: Parity Bit Calculation:
$$p_1 = d_1 \oplus d_2 \oplus d_4 = 1 \oplus 0 \oplus 1 = 0$$
$$p_2 = d_1 \oplus d_3 \oplus d_4 = 1 \oplus 1 \oplus 1 = 1$$
$$p_4 = d_2 \oplus d_3 \oplus d_4 = 0 \oplus 1 \oplus 1 = 0$$

#### Step 3: Transmitted Codeword:
Arranging bits in positions 1 to 7:
```
Position:  1   2   3   4   5   6   7
Bit:      p1  p2  d1  p4  d2  d3  d4
Value:     0   1   1   0   0   1   1
```
$$\mathbf{\text{Transmitted Codeword} = 0110011}$$

#### Step 4: Error Introduction during Transmission:
Bit 6 is flipped from $1 \to 0$:
Received word:
```
Position:  1   2   3   4   5   6   7
Received:  0   1   1   0   0   0   1   (Bit 6 changed from 1 to 0!)
```

#### Step 5: Syndrome Calculation at Receiver:
$$S_1 = b_1 \oplus b_3 \oplus b_5 \oplus b_7 = 0 \oplus 1 \oplus 0 \oplus 1 = 0$$
$$S_2 = b_2 \oplus b_3 \oplus b_6 \oplus b_7 = 1 \oplus 1 \oplus 0 \oplus 1 = 1$$
$$S_4 = b_4 \oplus b_5 \oplus b_6 \oplus b_7 = 0 \oplus 0 \oplus 0 \oplus 1 = 1$$

Syndrome Word:
$$\mathbf{S = S_4 S_2 S_1 = (110)_2 = 6_{10}}$$

#### Step 6: Error Detection and Correction:
- Syndrome value is `6`, which mathematically proves that **Bit Position 6 is in error**!
- Receiver corrects bit 6 by complementing it: $b_6 = 0 \to 1$.
- Corrected Codeword: `0110011`.
- Original Data recovered from positions 3, 5, 6, 7: `1011`!
