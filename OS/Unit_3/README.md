# Operating Systems - Unit 3: CPU Scheduling & Deadlock

> **University Curriculum:** AKTU B.Tech II-Year (Semester-IV) CS / IT & Allied Branches (`BCS401`)  
> **Source Syllabus:** Complete 263-Page Unit 3 Lecture Series (Gateway Classes BCS401)

---

## 📑 Complete Unit 3 Module Navigation

| Priority / Folder | Module Title | Key Topics Covered | Direct Links |
| :---: | :--- | :--- | :---: |
| **00** | **[00_Quick_Revision_Short_Notes](00_Quick_Revision_Short_Notes/)** | ⭐ **Exact 3-Page Ultra Revision Notes** (Formulae, Comparison Tables, Traces) | [PDF](Unit_3_Quick_Revision_3_Page_Notes.pdf) &bull; [Notes](00_Quick_Revision_Short_Notes/README.md) |
| **01** | **[01_Process_Concepts_States_and_PCB](01_Process_Concepts_States_and_PCB/)** | Program vs Process, Address Space, 5 & 7 States Model, PCB Fields (`task_struct`) | [PDF](01_Process_Concepts_States_and_PCB/01_Process_Concepts_States_and_PCB.pdf) &bull; [Notes](01_Process_Concepts_States_and_PCB/README.md) |
| **02** | **[02_Schedulers_and_Context_Switching](02_Schedulers_and_Context_Switching/)** | Schedulers (LTS, STS, MTS), Dispatcher, Latency, CPU Efficiency Formula & Overhead | [PDF](02_Schedulers_and_Context_Switching/02_Schedulers_and_Context_Switching.pdf) &bull; [Notes](02_Schedulers_and_Context_Switching/README.md) |
| **03** | **[03_Threads_and_Multithreading_Models](03_Threads_and_Multithreading_Models/)** | Process vs Thread, Shared vs Private data, ULT vs KLT, Models ($M:1$, $1:1$, $M:N$) | [PDF](03_Threads_and_Multithreading_Models/03_Threads_and_Multithreading_Models.pdf) &bull; [Notes](03_Threads_and_Multithreading_Models/README.md) |
| **04** | **[04_CPU_Scheduling_Concepts_and_Criteria](04_CPU_Scheduling_Concepts_and_Criteria/)** | CPU-I/O Burst Cycle, Preemptive vs Non-Preemptive, 5 Performance Criteria (TAT, WT, RT) | [PDF](04_CPU_Scheduling_Concepts_and_Criteria/04_CPU_Scheduling_Concepts_and_Criteria.pdf) &bull; [Notes](04_CPU_Scheduling_Concepts_and_Criteria/README.md) |
| **05** | **[05_FCFS_and_Convoy_Effect](05_FCFS_and_Convoy_Effect/)** | FCFS Scheduling, Detailed Convoy Effect Proof ($17.0\text{ ms} \to 3.0\text{ ms}$), Solved Numericals | [PDF](05_FCFS_and_Convoy_Effect/05_FCFS_and_Convoy_Effect.pdf) &bull; [Notes](05_FCFS_and_Convoy_Effect/README.md) |
| **06** | **[06_SJF_and_SRTF_Scheduling](06_SJF_and_SRTF_Scheduling/)** | Non-preemptive SJF, Exponential Smoothing Burst Prediction, SRTF Preemptive Trace | [PDF](06_SJF_and_SRTF_Scheduling/06_SJF_and_SRTF_Scheduling.pdf) &bull; [Notes](06_SJF_and_SRTF_Scheduling/README.md) |
| **07** | **[07_Priority_Scheduling_and_Aging](07_Priority_Scheduling_and_Aging/)** | Priority Scheduling (Preemptive & Non-preemptive), GATE-2017 Trace, Starvation & Aging | [PDF](07_Priority_Scheduling_and_Aging/07_Priority_Scheduling_and_Aging.pdf) &bull; [Notes](07_Priority_Scheduling_and_Aging/README.md) |
| **08** | **[08_Round_Robin_Scheduling](08_Round_Robin_Scheduling/)** | Circular FIFO Queue, Time Quantum $q$ Dynamics, 80% Rule of Thumb, Solved Numericals | [PDF](08_Round_Robin_Scheduling/08_Round_Robin_Scheduling.pdf) &bull; [Notes](08_Round_Robin_Scheduling/README.md) |
| **09** | **[09_Multilevel_Queue_and_MLFQ](09_Multilevel_Queue_and_MLFQ/)** | Multilevel Queue (MLQ Static) vs Multilevel Feedback Queue (MLFQ Dynamic Feedback) | [PDF](09_Multilevel_Queue_and_MLFQ/09_Multilevel_Queue_and_MLFQ.pdf) &bull; [Notes](09_Multilevel_Queue_and_MLFQ/README.md) |
| **10** | **[10_Multiprocessor_Scheduling](10_Multiprocessor_Scheduling/)** | Asymmetric (AMP) vs Symmetric (SMP), Processor Affinity (Cache Warmth), NUMA, Migration | [PDF](10_Multiprocessor_Scheduling/10_Multiprocessor_Scheduling.pdf) &bull; [Notes](10_Multiprocessor_Scheduling/README.md) |
| **11** | **[11_Deadlock_System_Model_and_Coffman_Conditions](11_Deadlock_System_Model_and_Coffman_Conditions/)** | System Resource Model, 4 Coffman Necessary Conditions, Deadlock vs Starvation | [PDF](11_Deadlock_System_Model_and_Coffman_Conditions/11_Deadlock_System_Model_and_Coffman_Conditions.pdf) &bull; [Notes](11_Deadlock_System_Model_and_Coffman_Conditions/README.md) |
| **12** | **[12_Resource_Allocation_Graph_RAG](12_Resource_Allocation_Graph_RAG/)** | RAG Edges, Cycle Theorems (Single-instance vs Multi-instance), Counterexample Traces | [PDF](12_Resource_Allocation_Graph_RAG/12_Resource_Allocation_Graph_RAG.pdf) &bull; [Notes](12_Resource_Allocation_Graph_RAG/README.md) |
| **13** | **[13_Deadlock_Prevention_and_Havender_Algorithm](13_Deadlock_Prevention_and_Havender_Algorithm/)** | Denying Coffman Conditions, Havender's Resource Ordering $F(R_i) < F(R_j)$ & Proof | [PDF](13_Deadlock_Prevention_and_Havender_Algorithm/13_Deadlock_Prevention_and_Havender_Algorithm.pdf) &bull; [Notes](13_Deadlock_Prevention_and_Havender_Algorithm/README.md) |
| **14** | **[14_Deadlock_Avoidance_and_Bankers_Algorithm](14_Deadlock_Avoidance_and_Bankers_Algorithm/)** | Safe State, Banker's Algorithm Data Structures, Safety Algorithm & Resource Request Trace | [PDF](14_Deadlock_Avoidance_and_Bankers_Algorithm/14_Deadlock_Avoidance_and_Bankers_Algorithm.pdf) &bull; [Notes](14_Deadlock_Avoidance_and_Bankers_Algorithm/README.md) |
| **15** | **[15_Deadlock_Detection_and_Recovery](15_Deadlock_Detection_and_Recovery/)** | Wait-For Graph (WFG), Detection Matrix, Process Abort, Preemption & Checkpoint Rollback | [PDF](15_Deadlock_Detection_and_Recovery/15_Deadlock_Detection_and_Recovery.pdf) &bull; [Notes](15_Deadlock_Detection_and_Recovery/README.md) |
| **16** | **[16_Unit_3_AKTU_PYQs_and_Interview_Cheatsheet](16_Unit_3_AKTU_PYQs_and_Interview_Cheatsheet/)** | AKTU PYQs (2 & 10 Marks), Master Formula Cheatsheet, Unit 3 Mindmap, FAANG FAQs | [PDF](16_Unit_3_AKTU_PYQs_and_Interview_Cheatsheet/16_Unit_3_AKTU_PYQs_and_Interview_Cheatsheet.pdf) &bull; [Notes](16_Unit_3_AKTU_PYQs_and_Interview_Cheatsheet/README.md) |

---

## 📚 Consolidated Master Deliverable
- 📕 **[Unit_3_Master_Notes.pdf](Unit_3_Master_Notes.pdf)**: Complete 20+ page compilation of all 16 chapter PDFs with high-resolution SVG architecture diagrams.
- ⚡ **[Unit_3_Quick_Revision_3_Page_Notes.pdf](Unit_3_Quick_Revision_3_Page_Notes.pdf)**: Exact 3-page ultra high-yield revision PDF for quick recall.
