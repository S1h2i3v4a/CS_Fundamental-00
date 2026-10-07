# Module 12: Resource Allocation Graph (RAG) & Cycle Detection Rules

> **Unit 3: CPU Scheduling & Deadlock** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Resource Allocation Graph (RAG) Basics

### 1.1 Formal Graph Representation
RAG ek directed graph $G = (V, E)$ hai:
- **Vertices ($V$):**
  1. Process Nodes: $P = \{P_1, P_2, \dots, P_n\}$ (Circles)
  2. Resource Nodes: $R = \{R_1, R_2, \dots, R_m\}$ (Rectangles). Har rectangle ke andar dots resource ke individual instances represent karte hain.
- **Edges ($E$):**
  1. **Request Edge ($P_i \to R_j$):** Process $P_i$ resource $R_j$ ki ek instance request kar raha hai (Wait state).
  2. **Assignment Edge ($R_j \to P_i$):** Resource $R_j$ ki ek specific instance process $P_i$ ko allocated hai.

---

## 2. Cycle Detection Rules: Golden Theorem

### 2.1 Rule 1: No Cycle in RAG
$$\text{If Graph has NO Cycle } \implies \text{System is 100\% DEADLOCK FREE.}$$

### 2.2 Rule 2: Single-Instance Resources With Cycle
$$\text{If each resource has EXACTLY 1 instance AND Graph has a Cycle } \implies \text{DEADLOCK IS GUARANTEED!}$$
Is case me cycle ka hona deadlock ke liye **Necessary and Sufficient Condition** hai.

### 2.3 Rule 3: Multiple-Instance Resources With Cycle
$$\text{If resources have Multiple instances AND Graph has a Cycle } \implies \text{DEADLOCK MAY OR MAY NOT EXIST!}$$
Is case me cycle sirf **Necessary Condition** hai, par Sufficient nahi hai!

---

## 3. Classic Counterexample: Cycle with NO Deadlock (Gateway Slide 212)

Consider a system:
- $R_1$ has 2 instances.
- $R_2$ has 2 instances.
- Process $P_1$ holds 1 instance of $R_1$ and requests $R_2$.
- Process $P_2$ holds 1 instance of $R_2$ and requests $R_1$.
- Process $P_3$ holds 1 instance of $R_1$ and needs nothing.
- Process $P_4$ holds 1 instance of $R_2$ and needs nothing.

### Analysis:
Graph me cycle exist karti hai: $P_1 \to R_2 \to P_2 \to R_1 \to P_1$.
Lekin:
1. $P_3$ kisi resource ka wait nahi kar raha. Wo execute hokar $R_1$ ka instance release kar dega.
2. $P_2$ ko $R_1$ mil jayega, wo complete hokar $R_2$ release kar dega.
3. Fir $P_1$ ko $R_2$ mil jayega aur sabhi processes safely terminate ho jayenge.
- **Conclusion:** Cycle hone ke bawajood system me **Deadlock nahi hai!**

---

## 4. Architectural Diagram

<div class="diagram">
  <img src="diagrams/resource_allocation_graph.svg" alt="Resource Allocation Graph Diagram" style="max-width: 100%;">
</div>

---

## 5. AKTU Exam & Interview Highlights

> **AKTU PYQ (10 Marks):**
> *"What is Resource Allocation Graph (RAG)? Prove that a cycle in RAG is a necessary but not a sufficient condition for deadlock."*
>
> **Top Tech Interview Insight:**
> *"How do modern distributed systems detect cycles in resource graphs?"*
> **Answer:** Distributed systems wait-for graphs build karte hain aur Chandy-Misra-Haas probe messaging algorithm ($O(|E|)$ messages) use karke edge-chasing ke zariye distributed cycles detect karte hain.
