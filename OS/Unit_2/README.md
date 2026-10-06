# Operating System - Unit 2: Concurrent Processes & Synchronization

Yeh folder **Operating System (Unit 2 Complete Syllabus - BCS401)** ke sabhi topics ko priority-wise, sequential do-digit format (`01_` to `12_`) mein organize karta hai taaki GitHub par exact hierarchical order mein display ho.

---

## ⚡ Quick Revision Short Notes (Last-Minute Recall)

> 🚀 **[00_Quick_Revision_Short_Notes](./00_Quick_Revision_Short_Notes/README.md)**  
> Poore Unit 2 ke sabhi 12 core subtopics ko **sirf 3 pages** mein condense kiya gaya hai taaki exam ya technical interview se 15 minute pehle sabhi concepts, code traces aur formulas rapidly recall ho sakein!  
> 📄 **[Download 3-Page Short Notes PDF (Instant Recall)](./Unit_2_Quick_Revision_3_Page_Notes.pdf)**

---

## 🗺️ Complete Unit 2 Roadmap (Priority 00 to 12)

| Priority | Module Subfolder | Key Concepts Covered | Visual Architectural Diagram | Chapter PDF |
| :---: | :--- | :--- | :---: | :---: |
| **00** | [00_Quick_Revision_Short_Notes](./00_Quick_Revision_Short_Notes/README.md) | **Unit 2 Ultra High-Yield 3-Page Cheat Sheet (All Concurrency Topics)** | Rapid Mind Map | [3-Page PDF](./Unit_2_Quick_Revision_3_Page_Notes.pdf) |
| **01** | [01_Process_Concept_and_Concurrency_Principles](./01_Process_Concept_and_Concurrency_Principles/README.md) | Process Concept, Independent vs Cooperating Processes, Concurrency Principles, Race Conditions & Lost Updates | [Process Concurrency & Race Condition](./01_Process_Concept_and_Concurrency_Principles/diagrams/process_concurrency_race_condition.svg) | [Download PDF](./01_Process_Concept_and_Concurrency_Principles/01_Process_Concept_and_Concurrency_Principles.pdf) |
| **02** | [02_Critical_Section_Problem_and_Criteria](./02_Critical_Section_Problem_and_Criteria/README.md) | 4 Code Sections (Entry, CS, Exit, Remainder), Primary (Mutual Exclusion, Progress) & Secondary Criteria (Bounded Wait, Speed Neutrality) | [Critical Section Structure & Criteria](./02_Critical_Section_Problem_and_Criteria/diagrams/critical_section_structure_criteria.svg) | [Download PDF](./02_Critical_Section_Problem_and_Criteria/02_Critical_Section_Problem_and_Criteria.pdf) |
| **03** | [03_Software_Solutions_Peterson_Algorithm](./03_Software_Solutions_Peterson_Algorithm/README.md) | Gary Peterson's 2-Process Algorithm, `flag[2]` & `turn` Variables, Step-by-Step State Trace, Mathematical Proofs | [Peterson's Algorithm State Trace](./03_Software_Solutions_Peterson_Algorithm/diagrams/peterson_algorithm_trace.svg) | [Download PDF](./03_Software_Solutions_Peterson_Algorithm/03_Software_Solutions_Peterson_Algorithm.pdf) |
| **04** | [04_Software_Solutions_Dekker_Algorithm](./04_Software_Solutions_Dekker_Algorithm/README.md) | First Software Solution (1965), Contention Back-off Loop, Polite Yielding, Comparison with Peterson | [Dekker's Algorithm Flowchart](./04_Software_Solutions_Dekker_Algorithm/diagrams/dekkers_algorithm_flowchart.svg) | [Download PDF](./04_Software_Solutions_Dekker_Algorithm/04_Software_Solutions_Dekker_Algorithm.pdf) |
| **05** | [05_Hardware_Synchronization_Test_and_Set](./05_Hardware_Synchronization_Test_and_Set/README.md) | Software Lock Flaw, Hardware Atomic Primitives (`Test_and_Set` / TSL, `Swap`), Spinlocks & Busy Waiting Analysis | [Hardware Sync & Spinlock Architecture](./05_Hardware_Synchronization_Test_and_Set/diagrams/hardware_sync_test_and_set.svg) | [Download PDF](./05_Hardware_Synchronization_Test_and_Set/05_Hardware_Synchronization_Test_and_Set.pdf) |
| **06** | [06_Semaphores_and_Mutexes](./06_Semaphores_and_Mutexes/README.md) | Dijkstra's Semaphores, Counting vs Binary Semaphores, Block & Wakeup Implementation (No Busy Wait), Mutex vs Semaphore | [Semaphore Block-Wakeup Queue Architecture](./06_Semaphores_and_Mutexes/diagrams/semaphore_block_wakeup_architecture.svg) | [Download PDF](./06_Semaphores_and_Mutexes/06_Semaphores_and_Mutexes.pdf) |
| **07** | [07_Producer_Consumer_Problem](./07_Producer_Consumer_Problem/README.md) | Bounded Buffer Problem, Assembly Race Condition on `count`, 3 Semaphores (`empty`, `full`, `mutex`), Deadlock Order Trap | [Circular Ring Buffer & Semaphore Coordination](./07_Producer_Consumer_Problem/diagrams/producer_consumer_bounded_buffer.svg) | [Download PDF](./07_Producer_Consumer_Problem/07_Producer_Consumer_Problem.pdf) |
| **08** | [08_Readers_Writers_Problem](./08_Readers_Writers_Problem/README.md) | Concurrent Readers, Exclusive Writers, Reader Counter `rc`, First-In Last-Out Lock, Writer Starvation Dilemma | [Readers-Writers Synchronization Architecture](./08_Readers_Writers_Problem/diagrams/readers_writers_synchronization.svg) | [Download PDF](./08_Readers_Writers_Problem/08_Readers_Writers_Problem.pdf) |
| **09** | [09_Dining_Philosophers_and_Sleeping_Barber](./09_Dining_Philosophers_and_Sleeping_Barber/README.md) | Classical Problems: 5 Philosophers Circular Wait Deadlock & Asymmetric Solution; Sleeping Barber Customer Queue & Dropout | [Dining Philosophers & Sleeping Barber](./09_Dining_Philosophers_and_Sleeping_Barber/diagrams/dining_philosophers_and_sleeping_barber.svg) | [Download PDF](./09_Dining_Philosophers_and_Sleeping_Barber/09_Dining_Philosophers_and_Sleeping_Barber.pdf) |
| **10** | [10_Process_Generation_and_Lifecycle](./10_Process_Generation_and_Lifecycle/README.md) | Forking vs Spawning, `fork()` Return Values, $2^n$ Mathematical Process Tree Formula, Zombie (`<defunct>`) vs Orphan Processes | [Process Generation, fork() & Lifecycle](./10_Process_Generation_and_Lifecycle/diagrams/fork_process_tree_lifecycle.svg) | [Download PDF](./10_Process_Generation_and_Lifecycle/10_Process_Generation_and_Lifecycle.pdf) |
| **11** | [11_Inter_Process_Communication_IPC](./11_Inter_Process_Communication_IPC/README.md) | Shared Memory (Fastest, Local) vs Message Passing (Distributed, Syscall), Direct vs Indirect, Blocking Semantics, Buffering | [Shared Memory vs Message Passing IPC](./11_Inter_Process_Communication_IPC/diagrams/ipc_shared_memory_vs_message_passing.svg) | [Download PDF](./11_Inter_Process_Communication_IPC/11_Inter_Process_Communication_IPC.pdf) |
| **12** | [12_Unit_2_AKTU_PYQs_and_Interview_Cheatsheet](./12_Unit_2_AKTU_PYQs_and_Interview_Cheatsheet/README.md) | Solved AKTU Question Bank (2014-2023), Priority Inversion & Mars Pathfinder Incident, Deadlock vs Livelock vs Starvation | [Unit 2 Complete Concurrency Mindmap](./12_Unit_2_AKTU_PYQs_and_Interview_Cheatsheet/diagrams/unit2_concurrency_mindmap.svg) | [Download PDF](./12_Unit_2_AKTU_PYQs_and_Interview_Cheatsheet/12_Unit_2_AKTU_PYQs_and_Interview_Cheatsheet.pdf) |

---

## 📚 Master Consolidated PDF Documents
- 📄 **[Unit_2_Quick_Revision_3_Page_Notes.pdf](./Unit_2_Quick_Revision_3_Page_Notes.pdf)** (Exact 3-Page Ultra Condensed Sheet for Rapid Recall)
- 📄 **[Unit_2_Master_Notes.pdf](./Unit_2_Master_Notes.pdf)** (Complete 17-Page Master Document, All 12 Modules Consolidated)

---
*Created for CS Fundamentals Repository by Shivam Keshari*
