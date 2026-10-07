# Module 01: Relational Algebra Complete Operators and Solved Numericals

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** Procedural Query Foundations, Fundamental & Derived Operators, Union Compatibility, Joins, Division Operator & AKTU Solved Numericals

---

## 1. Relational Algebra Overview & Core Philosophy

Relational Algebra ek **procedural query language** hai jisme user system ko yeh batata hai ki **WHAT data is required** AND **HOW to retrieve that data step-by-step**.
- Yeh relations (tables) ko as an input leti hai aur output mein bhi ek **new relation (table)** return karti hai (**Closure Property**).
- Relational database management systems (RDBMS) ke query execution engines (query optimizers) high-level SQL queries ko internal relational algebra expression tree mein compile aur optimize karte hain.

```
       [ SQL Declarative Query ]
                  │
                  ▼
         [ Query Parser ]
                  │
                  ▼
     [ Relational Algebra Tree ]  <-- (Heuristic Rule-Based Optimization)
                  │
                  ▼
       [ Physical Execution Plan ]
```

---

## 2. Fundamental Operations of Relational Algebra

Fundamental operations wo atomic operations hain jinhe kisi doosre relational operator ke combination se express **nahi** kiya ja sakta. Yeh 5 core operations hain:

### 2.1 Selection ($\sigma$) — Horizontal Filtering
- **Working:** Relation ke un tuples (rows) ko select karta hai jo specified predicate condition $p$ ko satisfy karte hain.
- **Formal Notation:**
  $$\sigma_p(R)$$
- **Key Characteristics:**
  - Works on **Rows** (horizontal slice).
  - Degree (column count) unaltered rehti hai: $\text{deg}(\sigma_p(R)) = \text{deg}(R)$.
  - Cardinality (row count) decrease ya equal ho sakti hai: $|\sigma_p(R)| \le |R|$.
- **Example Queries:**
  - *Find all CSE students:* $\sigma_{\text{Dept} = \text{'CSE'}}(\text{STUDENT})$
  - *Find CSE students with CPI > 8.5:* $\sigma_{\text{Dept} = \text{'CSE'} \land \text{CPI} > 8.5}(\text{STUDENT})$

### 2.2 Projection ($\pi$) — Vertical Filtering
- **Working:** Relation ke specific specified attributes (columns) ko extract karta hai aur baaki sabhi columns ko discard kar deta hai.
- **Formal Notation:**
  $$\pi_{A_1, A_2, \dots, A_k}(R)$$
- **Key Characteristics:**
  - Works on **Columns** (vertical slice).
  - **Duplicate Elimination:** Formal relational algebra sets par work karti hai (not multisets/bags). Isliye projection operation duplicate rows ko **automatically remove** kar deta hai!
  - Output degree: $\text{deg}(\pi_A(R)) = k$ (where $k$ is number of projected attributes).
- **Example Queries:**
  - *Get only names of students:* $\pi_{\text{Name}}(\text{STUDENT})$
  - *Get distinct department names:* $\pi_{\text{Dept}}(\text{STUDENT})$

### 2.3 Union ($\cup$)
- **Working:** Do relations ke sabhi tuples ko combine karta hai aur duplicates ko eliminate karta hai.
- **Formal Notation:** $R \cup S$
- **Union Compatibility Condition (Crucial AKTU Exam Question):**
  Do relations $R$ aur $S$ tabhi union-compatible hote hain jab:
  1. Dono relations ki **degree (number of columns) exactly same** ho: $\text{deg}(R) = \text{deg}(S)$.
  2. Corresponding attributes ke **domains (data types) compatible** hon: $\text{dom}(R.A_i) = \text{dom}(S.B_i)$.
- **Commutative Property:** $R \cup S = S \cup R$.

### 2.4 Set Difference ($-$)
- **Working:** Un tuples ko return karta hai jo first relation $R$ mein present hain lekin second relation $S$ mein present **nahi** hain.
- **Formal Notation:** $R - S$
- **Conditions:** $R$ aur $S$ ka **Union Compatible** hona mandatory hai.
- **Non-Commutative Property:** $R - S \ne S - R$.

### 2.5 Cartesian Product ($\times$)
- **Working:** Relation $R$ ke har single tuple ko relation $S$ ke har single tuple ke saath pair karta hai.
- **Formal Notation:** $R \times S$
- **Metrics Calculation:**
  $$\text{Degree}(R \times S) = \text{Degree}(R) + \text{Degree}(S)$$
  $$\text{Cardinality}(R \times S) = |R| \times |S|$$
- **Example:** Agar $R$ mein 10 rows and 3 columns hain, aur $S$ mein 5 rows and 4 columns hain, toh $R \times S$ mein $3 + 4 = 7$ columns aur $10 \times 5 = 50$ rows hongi.

### 2.6 Rename ($\rho$)
- **Working:** Output relation ya uske attributes ke names ko change karta hai taaki self-joins ya sub-expressions mein ambiguity na rahe.
- **Notation:** $\rho_{S(B_1, B_2, \dots, B_n)}(R)$ (renames relation $R$ to $S$ and attributes to $B_1 \dots B_n$).

---

## 3. Derived Operators & Advanced Joins

Derived operators fundamental operators ke combinations se express kiye ja sakte hain.

### 3.1 Theta Join ($\bowtie_\theta$) & Equi Join
- **Theta Join:** Cartesian product followed by condition-based selection.
  $$R \bowtie_\theta S = \sigma_\theta(R \times S)$$
- **Equi Join:** Theta join jisme condition operator strictly equality ($=$) hota hai.

### 3.2 Natural Join ($\bowtie$)
- **Definition:** Equi-join on all attributes that have the same name in both relations, followed by the automatic projection that removes redundant duplicate columns.
- **Syntax:** $R \bowtie S$

### 3.3 Outer Joins (Handling Dangling / Non-Matching Tuples)
1. **Left Outer Join ($R \LeftThreetimes S$):** Keeps all matching tuples PLUS all non-matching tuples from the left relation $R$ (padded with NULL for $S$ attributes).
2. **Right Outer Join ($R \RightThreetimes S$):** Keeps all matching tuples PLUS all non-matching tuples from the right relation $S$ (padded with NULL for $R$ attributes).
3. **Full Outer Join ($R \fullouterjoin S$):** Keeps all matching tuples PLUS all unmatched tuples from BOTH $R$ and $S$.

### 3.4 Division Operator ($\div$) — Solving "FOR ALL" Queries
- **Purpose:** Relational algebra mein universal quantification ("find entities associated with **ALL** items of a target set") ko solve karne ke liye division operator use hota hai.
- **Formal Expansion:**
  $$R(A, B) \div S(B) = \pi_A(R) - \pi_A((\pi_A(R) \times S) - R)$$

---

## 4. Solved AKTU Numerical: Suppliers & Parts Database (10-Marker)

Given Schema:
- `SUPPLIERS(sid, sname, address)`
- `PARTS(pid, pname, color)`
- `CATALOG(sid, pid, cost)`

### Query 1: Find names of suppliers who supply some RED part.
$$\pi_{\text{sname}}\Big( \text{SUPPLIERS} \bowtie \pi_{\text{sid}}\big(\text{CATALOG} \bowtie \sigma_{\text{color} = \text{'RED'}}(\text{PARTS})\big) \Big)$$

### Query 2: Find sids of suppliers who supply every part.
$$\pi_{\text{sid}, \text{pid}}(\text{CATALOG}) \div \pi_{\text{pid}}(\text{PARTS})$$

### Query 3: Find sids of suppliers who supply every RED part.
$$\pi_{\text{sid}, \text{pid}}(\text{CATALOG}) \div \pi_{\text{pid}}(\sigma_{\text{color} = \text{'RED'}}(\text{PARTS}))$$
