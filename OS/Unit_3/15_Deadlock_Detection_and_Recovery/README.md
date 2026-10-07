# Module 15: Deadlock Detection & Recovery Strategies

> **Unit 3: CPU Scheduling & Deadlock** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Deadlock Detection Principles

Agar system me Deadlock Prevention ya Avoidance implement na kiya jaye, to system Deadlock me ja sakta hai. Aise systems me OS periodic intervals par **Deadlock Detection Algorithm** run karta hai:

### 1.1 Single-Instance Resources: Wait-For Graph (WFG)
- RAG me se resource nodes ko collapse karke sirf process nodes rakhe jaate hain.
- Directed edge $P_i \to P_j$ ka matlab hai ki $P_i$ us resource ke liye wait kar raha hai jo $P_j$ ke paas allocated hai.
- **Detection Algorithm:** Standard Cycle Detection via Depth First Search (DFS) in $O(V^2)$ time.
- Agar WFG me cycle mil jaye &rarr; **Deadlock Detected!**

### 1.2 Multiple-Instance Resources: Detection Algorithm
Banker's algorithm ke similar matrix algorithm use hota hai jisme:
- `Available[m]`, `Allocation[n][m]`, aur process ki actual request matrix `Request[n][m]` compare hoti hai.

---

## 2. Deadlock Recovery Strategies (Gateway Slide 260)

Deadlock detect hone ke baad system ko normal state me laane ke 2 primary approaches hote hain:

### 2.1 Process Termination
1. **Abort All Deadlocked Processes:** Saare deadlocked processes ko kill kar do.
   - *Advantage:* Deadlock 100% resolve hone ki guarantee.
   - *Disadvantage:* Bahut expensive (ghanton ki computation barbad ho jati hai).
2. **Abort One Process at a Time:** Ek process ko kill karo, fir detection run karo. Agar cycle abhi bhi hai to agla process kill karo.
   - *Victim Selection Criteria:*
     - Process ki priority kitni hai.
     - Process ne kitna CPU time use kiya hai aur kitna bacha hai.
     - Process ne kitne resources lock kiye huye hain.
     - Process interactive hai ya batch.

### 2.2 Resource Preemption
Deadlocked process se resources forcibly chheen kar kisi dusre process ko allocate karna:
1. **Selecting a Victim:** Aisa process choose karna jisse preemption cost minimum ho.
2. **Rollback:**
   - *Total Rollback:* Process ko completely abort karke shuru se restart karna.
   - *Partial Rollback:* Process ko pichhle saved **Checkpoint** state par restore karna taaki progress bachi rahe.
3. **Preventing Starvation:**
   - Agar har baar usi same process ko victim chun liya jaye to wo kabhi complete nahi ho payega (**Starvation**).
   - **Solution:** Victim selection formula me process ke **Number of Rollbacks** ka factor add kar diya jata hai. Jis process ko ek baar preempt kiya gaya, agli baar uski preemption cost badh jati hai.

---

## 3. Architectural Diagram

<div class="diagram">
  <img src="diagrams/deadlock_detection_recovery.svg" alt="Deadlock Detection Recovery Diagram" style="max-width: 100%;">
</div>

---

## 4. AKTU Exam & Interview Highlights

> **AKTU PYQ (10 Marks):**
> *"How is a deadlock detected in a system? Explain Wait-For graph. Discuss recovery from deadlock through process termination and resource preemption with starvation prevention."*
>
> **Top Tech Interview Insight:**
> *"How does the Ostrich Algorithm compare with Deadlock Detection?"*
> **Answer:** The Ostrich Algorithm deadlocks ko simply ignore kar deta hai (like an ostrich sticking its head in the sand). UNIX, Linux aur Windows general purpose OS me yahi use karte hain kyunki actual deadlocks rare hote hain aur detection/avoidance ka runtime overhead unki recovery cost se zyada hota hai!
