# Module 02: Relational Calculus (TRC and DRC)

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** Declarative Non-Procedural Foundations, Tuple Relational Calculus (TRC), Domain Relational Calculus (DRC), Quantifiers ($\exists, \forall$), Safe Queries & Codd's Equivalence Theorem

---

## 1. What is Relational Calculus?

Relational Algebra ke contrast mein, Relational Calculus ek **non-procedural (declarative)** query language hai:
- User sirf specify karta hai **WHAT information is desired**, bina yeh bataye ki data disk se kaise evaluate aur join hoga.
- Yeh mathematical logic (First-Order Predicate Calculus) par based hai.

```
Relational Algebra  --> Procedural    (WHAT + HOW step-by-step)
Relational Calculus --> Non-Procedural (WHAT only, Declarative)
```

---

## 2. Tuple Relational Calculus (TRC)

TRC mein queries relations ke individual **tuples (rows)** ko filter karti hain.

### 2.1 General Syntax
$$\{ t \mid P(t) \}$$
- $t$: Resulting tuple variable.
- $P(t)$: Predicate formula jo specify karta hai ki tuple $t$ result mein aane ke liye kya condition satisfy karega.

### 2.2 First-Order Logic Quantifiers
1. **Existential Quantifier ($\exists$ — "There exists"):**
   $$\exists s \in R \, (P(s))$$
   Yeh condition tab TRUE evaluate hoti hai jab relation $R$ mein kam se kam ek aisa tuple $s$ exist kare jiske liye predicate $P(s)$ TRUE ho.
2. **Universal Quantifier ($\forall$ — "For all"):**
   $$\forall s \in R \, (P(s))$$
   Yeh condition tab TRUE evaluate hoti hai jab relation $R$ ke **har ek single tuple** $s$ ke liye predicate $P(s)$ TRUE ho.
3. **De Morgan's Duality:**
   $$\forall s \, (P(s)) \equiv \neg \big( \exists s \, (\neg P(s)) \big)$$

### 2.3 Solved TRC Examples
Given Schema: `EMPLOYEE(emp_id, name, dept, salary)`
- **Query 1:** Find all employees with salary > 50,000:
  $$\{ t \mid t \in \text{EMPLOYEE} \land t.\text{salary} > 50000 \}$$
- **Query 2:** Find names of all employees working in 'Research' department:
  $$\{ t.\text{name} \mid t \in \text{EMPLOYEE} \land t.\text{dept} = \text{'Research'} \}$$

### 2.4 Safe TRC Queries (Important Exam Concept)
Ek TRC query tab **Safe** kehlati hai jab wo hamesha ek **finite set of tuples** produce kare jo database ke defined domain se belong karte hon.
- **Unsafe Query Example:**
  $$\{ t \mid \neg(t \in \text{EMPLOYEE}) \}$$
  Yeh query database ke bahar ke infinite universe ke har possible tuple ko return karne ki koshish karegi, jo computational disaster hai. Isliye query languages sirf *Safe* calculus ko allow karte hain.

---

## 3. Domain Relational Calculus (DRC)

DRC mein query variables individual **attribute domain values** ko represent karte hain, na ki pooray tuple ko.

### 3.1 General Syntax
$$\{ \langle x_1, x_2, \dots, x_n \rangle \mid P(x_1, x_2, \dots, x_n) \}$$
- $\langle x_1, \dots, x_n \rangle$: Resulting domain attributes.
- $P(x_1, \dots, x_n)$: Predicate condition on domain variables.

### 3.2 Solved DRC Example
- **Query:** Get `emp_id` and `name` of employees working in 'Sales' department:
  $$\{ \langle e, n \rangle \mid \exists d, s \, (\langle e, n, d, s \rangle \in \text{EMPLOYEE} \land d = \text{'Sales'}) \}$$

---

## 4. Codd's Theorem & Relational Completeness

E.F. Codd ne prove kiya tha ki:
$$\text{Relational Algebra} \equiv \text{Safe TRC} \equiv \text{Safe DRC}$$
- Koi bhi query language jo basic Relational Algebra ki expressive power ko match kar sakti hai, use **Relationally Complete** kaha jata hai.
- Modern SQL relational algebra aur relational calculus dono ke theoretical concepts par build ki gayi hai.
