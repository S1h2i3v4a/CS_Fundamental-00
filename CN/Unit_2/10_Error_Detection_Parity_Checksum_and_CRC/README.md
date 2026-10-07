# Module 10: Error Detection: Parity, Checksum & Cyclic Redundancy Check (CRC)

## 1. Types of Transmission Errors
Noise aur attenuation transmission lines par bits ko distort kar dete hain ($0 \to 1$ or $1 \to 0$):
1. **Single-Bit Error:** Pura data unit me sirf ek bit invert hoti hai. (Rare in modern high-speed transmission).
2. **Burst Error:** Data unit me do ya do se adhik bits corrupt hoti hain.
   - **Burst Length:** Pehli corrupted bit se lekar aakhiri corrupted bit tak ki total length (chahe beech ki kuch bits sahi bhi hon!). E.g., agar bit 3 aur bit 9 flip hui hain, to burst length $9 - 3 + 1 = 7$ bits hai.

---

## 2. Parity Check Methods

### 2.1 Simple (1D) Parity
- **Even Parity:** Total number of 1s ko even banane ke liye ek extra parity bit add ki jati hai.
- **Odd Parity:** Total number of 1s ko odd banane ke liye parity bit add hoti hai.
- **Weakness:** Agar **even number of bits flip ho jayein** (e.g., 2 bits ya 4 bits), to parity same rehti hai aur error undetected reh jata hai! (50% failure rate on burst errors).

### 2.2 Two-Dimensional (2D) Parity (LRC + VRC)
Data bits ko ek 2D rectangular table (matrix) me arrange kiya jata hai:
- Har row ke end me **Row Parity bit** add hoti hai.
- Pure table ke bottom par ek extra row add hoti hai jisme har column ki **Column Parity bit** hoti hai.
- **Detection Power:** Saare 1-bit, 2-bit, aur 3-bit errors pakad leti hai.
- **Correction Power:** Single-bit error ka intersection (Row $i$, Column $j$) milne par use automatically invert karke **correct** bhi kiya ja sakta hai!

---

## 3. Internet Checksum (1's Complement Arithmetic)
IP, TCP, aur UDP protocols internet checksum use karte hain:
1. Message ko 16-bit blocks me divide kiya jata hai.
2. Saare blocks ko 1's complement addition ke through add kiya jata hai.
   - **Wrap-around Carry Rule:** Agar MSB se carry out nikalta hai, to use discard karne ki bajay result ke LSB me add kiya jata hai!
3. Sum aane ke baad uska 1's complement (NOT operation) liya jata hai. Yeh result **Checksum** hota hai.
4. **Receiver Verification:** Receiver data blocks aur checksum ko add karta hai. Agar answer sabhi `1`s (`0xFFFF`) aaye, to data error-free hai!

---

## 4. Cyclic Redundancy Check (CRC) Polynomial Division

CRC Data Link Layer ka sabse powerful aur standardized error detection method hai (used in Ethernet 802.3 FCS). Yeh **Modulo-2 Arithmetic** (Binary division without carry/borrow, equivalent to XOR) par based hota hai.

### 4.1 Modulo-2 Arithmetic Rules
$$\mathbf{0 \oplus 0 = 0 \quad | \quad 0 \oplus 1 = 1 \quad | \quad 1 \oplus 0 = 1 \quad | \quad 1 \oplus 1 = 0}$$
- Same bits produce `0`, different bits produce `1`.
- Addition and subtraction are identical!

### 4.2 Algorithm Steps:
1. **Generator Polynomial $G(x)$:** Divisor of degree $r$.
2. **Append Zeros:** Data bitstream $D$ ke peeche $r$ zeros append kiye jate hain ($D \cdot 2^r$).
3. **Modulo-2 Division:** Appended bitstream ko $G(x)$ se modulo-2 divide kiya jata hai.
4. **Remainder ($R$):** Division ke baad bacha hua $r$-bit remainder hi **CRC (FCS)** hota hai.
5. **Transmitted Codeword:** $C = \text{Data} + \text{Remainder } R$.
6. **Receiver Verification:** Receiver received codeword ko exact same $G(x)$ se divide karta hai.
   - If $\text{Remainder} == 0 \implies \mathbf{ACCEPTED}$ (No error detected).
   - If $\text{Remainder} \ne 0 \implies \mathbf{REJECTED}$ (Error corrupted the frame!).

---

## 5. AKTU Core Solved Numericals

### Numerical 1: CRC Calculation & Verification (AKTU 10 Marks Exam Question)
> **Problem Statement:**  
> A bit stream `100100` is transmitted using the standard generator polynomial $G(x) = x^3 + x^2 + 1$.  
> 1. Find the binary representation of $G(x)$ and degree $r$.  
> 2. Determine the CRC code bits to be appended.  
> 3. Write the actual transmitted codeword.  
> 4. Verify the codeword at the receiver by showing that the remainder is 0.

#### Solution:
**Step 1: Generator Polynomial to Binary:**
$$G(x) = 1 \cdot x^3 + 1 \cdot x^2 + 0 \cdot x^1 + 1 \cdot x^0 \implies \mathbf{1101}$$
Degree of polynomial $r = 3$. Divisor has $r + 1 = 4$ bits.

**Step 2: Append $r = 3$ Zeros to Data:**
Data = `100100`  
Appended stream = `100100 000` (9 bits).

**Step 3: Modulo-2 Division:**
```
            111101  (Quotient)
     -------------
1101 ) 100100000
       1101
       -----
       01000      (Bring down 0)
        1101
        ----
        01010     (Bring down 0)
         1101
         ----
         01110    (Bring down 0)
          1101
          ----
          00110   (Bring down 0)
           0000
           ----
           01100  (Bring down 0)
            1101
            ----
            0001  --> Remainder R = 001 (3 bits)
```

**Step 4: Transmitted Codeword:**
$$\text{Codeword} = \text{Data} + \text{Remainder} = 100100\ 001$$

**Step 5: Receiver Verification:**
Receiver divides `100100001` by `1101`:
```
1101 ) 100100001
       1101
       -----
       01000
        1101
        ----
        01010
         1101
         ----
         01110
          1101
          ----
          00110
           0000
           ----
           01101
            1101
            ----
            0000  --> Remainder = 000! Verified Error-Free!
```

---

## 6. Error Detecting Capabilities of Polynomials
Ek polynomial $G(x)$ mathematically kya-kya detect kar sakta hai:
1. **Single-Bit Errors:** Detectable if $G(x)$ has more than one term and $x^0$ coefficient is 1.
2. **Two Isolated Single-Bit Errors:** Detectable if $G(x)$ does not divide $x^k + 1$ for any $k \le \text{frame length}$.
3. **Odd Number of Bit Errors:** Detectable if $G(x)$ contains $(x + 1)$ as a factor.
4. **Burst Errors of Length $L \le r$:** 100% detectable!
5. **Burst Errors of Length $L = r + 1$:** Detectable with probability $1 - \left(\frac{1}{2}\right)^{r-1}$. (For CRC-32, $99.9999999\%$ detection rate!).
