# Computer Science Fundamentals Repository

Welcome to the **CS Fundamentals** repository! Yeh repository Computer Science ke core subjects (Operating Systems, Computer Architecture, Memory Hierarchy, Scheduling, Kernels, Concurrent Processes, Synchronization, IPC, System Calls, and Exam PYQs) ke high-yield, interview-focused, aur structured notes provide karta hai.

---

## ⚡ Quick Revision Short Notes (Rapid Recall)
- 📄 **[Unit 1: 3-Page Quick Revision Short Notes (PDF)](./OS/Unit_1/Unit_1_Quick_Revision_3_Page_Notes.pdf)**: Complete Unit 1 condensed into **EXACT 3 PAGES**!
- 📄 **[Unit 2: 3-Page Quick Revision Short Notes (PDF)](./OS/Unit_2/Unit_2_Quick_Revision_3_Page_Notes.pdf)**: Complete Unit 2 (Concurrency & Synchronization) condensed into **EXACT 3 PAGES**!
- 📄 **[Unit 3: 3-Page Quick Revision Short Notes (PDF)](./OS/Unit_3/Unit_3_Quick_Revision_3_Page_Notes.pdf)**: Complete Unit 3 (CPU Scheduling & Deadlock) condensed into **EXACT 3 PAGES**!
- 📄 **[Unit 4: 3-Page Quick Revision Short Notes (PDF)](./OS/Unit_4/Unit_4_Quick_Revision_3_Page_Notes.pdf)**: Complete Unit 4 (Memory Management & Virtual Memory) condensed into **EXACT 3 PAGES**!
- 📄 **[Unit 5: 3-Page Quick Revision Short Notes (PDF)](./OS/Unit_5/Unit_5_Quick_Revision_3_Page_Notes.pdf)**: Complete Unit 5 (I/O Systems, Disk Scheduling, RAID & File Management) condensed into **EXACT 3 PAGES**!
- 📘 **[Unit 1 Guide](./OS/Unit_1/00_Quick_Revision_Short_Notes/README.md)** | **[Unit 2 Guide](./OS/Unit_2/00_Quick_Revision_Short_Notes/README.md)** | **[Unit 3 Guide](./OS/Unit_3/00_Quick_Revision_Short_Notes/README.md)** | **[Unit 4 Guide](./OS/Unit_4/00_Quick_Revision_Short_Notes/README.md)** | **[Unit 5 Guide](./OS/Unit_5/00_Quick_Revision_Short_Notes/README.md)**

---

## 📂 Repository Structure & Units

```
CS_Fundamental-00/
├── README.md                                    <-- Main Repository Guide
└── OS/                                          <-- Operating System Core Module
    ├── README.md                                <-- OS Subjects Index
    ├── Unit_1/                                  <-- Unit 1 Folder (Priorities 00 to 19)
    │   ├── README.md                            <-- Unit 1 Complete Roadmap
    │   ├── Unit_1_Quick_Revision_3_Page_Notes.pdf <-- 3-Page Rapid Recall PDF
    │   ├── Unit_1_Master_Notes.pdf              <-- 58-Page Consolidated Master PDF
    │   ├── 00_Quick_Revision_Short_Notes/       <-- Priority 00: 3-Page Ultra High-Yield Notes
    │   ├── 01_Introduction_to_OS/               <-- Priority 01: Definition, 3 Entities, 4 Components
    │   ├── 02_Components_and_Abstract_View/     <-- Priority 02: Abstract Layered View, Translators
    │   ├── 03_User_vs_System_View/              <-- Priority 03: User View vs System View (a = b + c)
    │   ├── 04_Kernel_and_Operations/            <-- Priority 04: Kernel Definition & 5 Core Functions
    │   ├── 05_Computer_System_Organization/     <-- Priority 05: Common Bus, Device/Memory Controllers
    │   ├── 06_Bootstrap_Program_and_Booting/    <-- Priority 06: Bootstrap Loader, POST, MBR/GPT
    │   ├── 07_Dual_Mode_Operation/              <-- Priority 07: User Mode vs Kernel Mode, Mode Bit
    │   ├── 08_Memory_Management_Functions/      <-- Priority 08: Primary Memory Byte Array, Base/Limit
    │   ├── 09_Memory_Hierarchy_and_Caching/     <-- Priority 09: Hierarchy Pyramid, L1/L2/L3, AMAT
    │   ├── 10_Processor_Management_and_Scheduling/ <-- Priority 10: Process PCB, Context Switch Latency
    │   ├── 11_Device_and_File_Management/      <-- Priority 11: Device Drivers, File CRUD, Inodes
    │   ├── 12_User_Interface_and_Specialized_OS_Functions/ <-- Priority 12: CLI vs GUI, Booting Modes
    │   ├── 13_Types_of_Operating_Systems_Batch_and_Multiprogrammed/ <-- Priority 13: Batch OS, Spooling
    │   ├── 14_Time_Sharing_and_Real_Time_Systems/ <-- Priority 14: Time Quantum, Hard vs Soft RTOS
    │   ├── 15_Multiprocessor_and_Distributed_Systems/ <-- Priority 15: SMP vs ASMP, Threads
    │   ├── 16_Operating_System_Structures_and_Architectures/ <-- Priority 16: Monolithic, Microkernel, LKM
    │   ├── 17_Advanced_Kernel_and_System_Calls/ <-- Priority 17: Reentrant Kernel, 6-Stage Syscall Trace
    │   ├── 18_OS_Services_and_System_Components/ <-- Priority 18: OS Services Stack, 8 Core Subsystems
    │   └── 19_AKTU_PYQs_and_Interview_Cheatsheet/ <-- Priority 19: 10 Years AKTU PYQs & Solved Answers
    ├── Unit_2/                                  <-- Unit 2 Folder (Priorities 00 to 12)
    │   ├── README.md                            <-- Unit 2 Complete Roadmap
    │   ├── Unit_2_Quick_Revision_3_Page_Notes.pdf <-- 3-Page Rapid Recall PDF
    │   ├── Unit_2_Master_Notes.pdf              <-- 17-Page Consolidated Master PDF
    │   ├── 00_Quick_Revision_Short_Notes/       <-- Priority 00: 3-Page Ultra High-Yield Notes
    │   ├── 01_Process_Concept_and_Concurrency_Principles/ <-- Priority 01: Race Conditions, Cooperating Processes
    │   ├── 02_Critical_Section_Problem_and_Criteria/      <-- Priority 02: 4 Sections, 4 Criteria (Mutual Exclusion, Progress)
    │   ├── 03_Software_Solutions_Peterson_Algorithm/      <-- Priority 03: Peterson's 2-Process Algorithm & Trace
    │   ├── 04_Software_Solutions_Dekker_Algorithm/        <-- Priority 04: Dekker's Algorithm & Back-off Loop
    │   ├── 05_Hardware_Synchronization_Test_and_Set/      <-- Priority 05: Atomic TSL, Swap, Spinlocks & Busy Wait
    │   ├── 06_Semaphores_and_Mutexes/                     <-- Priority 06: Counting vs Binary, Block-Wakeup Queue
    │   ├── 07_Producer_Consumer_Problem/                  <-- Priority 07: Bounded Buffer, Assembly Race, Deadlock Trap
    │   ├── 08_Readers_Writers_Problem/                    <-- Priority 08: Reader Priority, First-In Last-Out Lock, Starvation
    │   ├── 09_Dining_Philosophers_and_Sleeping_Barber/    <-- Priority 09: Circular Wait Deadlock, Barber Queue & Dropout
    │   ├── 10_Process_Generation_and_Lifecycle/           <-- Priority 10: fork(), 2^n Process Tree, Zombie vs Orphan
    │   ├── 11_Inter_Process_Communication_IPC/            <-- Priority 11: Shared Memory vs Message Passing, Sync Semantics
    │   └── 12_Unit_2_AKTU_PYQs_and_Interview_Cheatsheet/  <-- Priority 12: Concurrency PYQs & Solved Answers
    └── Unit_3/                                  <-- Unit 3 Folder (Priorities 00 to 16)
        ├── README.md                            <-- Unit 3 Complete Roadmap
        ├── Unit_3_Quick_Revision_3_Page_Notes.pdf <-- 3-Page Rapid Recall PDF
        ├── Unit_3_Master_Notes.pdf              <-- 17-Page Consolidated Master PDF
        ├── 00_Quick_Revision_Short_Notes/       <-- Priority 00: 3-Page Ultra High-Yield Notes
        ├── 01_Process_Concepts_States_and_PCB/  <-- Priority 01: Program vs Process, Address Space, 5 & 7 States, PCB
        ├── 02_Schedulers_and_Context_Switching/ <-- Priority 02: LTS, STS, MTS, Dispatcher Latency, CPU Efficiency
        ├── 03_Threads_and_Multithreading_Models/ <-- Priority 03: Process vs Thread, ULT vs KLT, Multithreading Models
        ├── 04_CPU_Scheduling_Concepts_and_Criteria/ <-- Priority 04: CPU-I/O Burst, Preemption, 5 Criteria (TAT, WT, RT)
        ├── 05_FCFS_and_Convoy_Effect/           <-- Priority 05: FCFS FIFO, Convoy Effect Proof & Solved Numericals
        ├── 06_SJF_and_SRTF_Scheduling/          <-- Priority 06: SJF Optimality, Exponential Smoothing, SRTF Preemption
        ├── 07_Priority_Scheduling_and_Aging/    <-- Priority 07: Preemptive Priority, GATE-2017 Trace, Starvation & Aging
        ├── 08_Round_Robin_Scheduling/           <-- Priority 08: Circular FIFO, Time Quantum Dynamics, 80% Rule
        ├── 09_Multilevel_Queue_and_MLFQ/        <-- Priority 09: MLQ Static Queues vs MLFQ Dynamic Feedback & Aging
        ├── 10_Multiprocessor_Scheduling/        <-- Priority 10: AMP vs SMP, Processor Affinity, NUMA, Load Balancing
        ├── 11_Deadlock_System_Model_and_Coffman_Conditions/ <-- Priority 11: 4 Coffman Conditions, Deadlock vs Starvation
        ├── 12_Resource_Allocation_Graph_RAG/    <-- Priority 12: RAG Request/Assignment Edges, Single vs Multi Cycle Rules
        ├── 13_Deadlock_Prevention_and_Havender_Algorithm/ <-- Priority 13: Denying Conditions, Havender's Resource Ordering
        ├── 14_Deadlock_Avoidance_and_Bankers_Algorithm/ <-- Priority 14: Safe State, Banker's Safety & Resource Request
        ├── 15_Deadlock_Detection_and_Recovery/  <-- Priority 15: Wait-For Graph (WFG), Detection Matrix, Process Abort
        └── 16_Unit_3_AKTU_PYQs_and_Interview_Cheatsheet/ <-- Priority 16: AKTU PYQs, Formula Sheet, Unit 3 Mindmap
    └── Unit_4/                                  <-- Unit 4 Folder (Priorities 00 to 15)
        ├── README.md                            <-- Unit 4 Complete Roadmap
        ├── Unit_4_Quick_Revision_3_Page_Notes.pdf <-- 3-Page Rapid Recall PDF
        ├── Unit_4_Master_Notes.pdf              <-- 19-Page Consolidated Master PDF
        ├── 00_Quick_Revision_Short_Notes/       <-- Priority 00: 3-Page Ultra High-Yield Notes
        ├── 01_Memory_Hierarchy_and_Address_Binding/ <-- Priority 01: Hierarchy, Resident Monitor, Binding Phases
        ├── 02_Contiguous_Allocation_and_Fragmentation/ <-- Priority 02: MFT, MVT, Internal/External Frag, Base/Limit
        ├── 03_Dynamic_Storage_Allocation_Strategies/ <-- Priority 03: First/Best/Worst/Next Fit, Compaction
        ├── 04_Paging_Architecture_and_Address_Translation/ <-- Priority 04: Frames, Pages, (p,d) to (f,d) Translation
        ├── 05_Translation_Lookaside_Buffer_TLB_and_EMAT/ <-- Priority 05: TLB Hardware, Hit/Miss, EMAT Formulas
        ├── 06_Multilevel_and_Inverted_Page_Tables/ <-- Priority 06: Two-Level Paging, Inverted Table, ASID
        ├── 07_Segmentation_and_Paged_Segmentation/ <-- Priority 07: User View, Base/Limit Trap, Hybrid Paging
        ├── 08_Virtual_Memory_and_Demand_Paging/ <-- Priority 08: Lazy Swapper, Valid-Invalid Bit, Page Fault
        ├── 09_Page_Fault_Handling_and_EAT_Performance/ <-- Priority 09: 6-Step Interrupt Trace, EAT Performance
        ├── 10_FIFO_Page_Replacement_and_Beladys_Anomaly/ <-- Priority 10: FIFO Queue, Belady Anomaly Proof
        ├── 11_Optimal_and_LRU_Page_Replacement/  <-- Priority 11: OPT Future Benchmark, LRU Stack Property
        ├── 12_Counting_Algorithms_and_Clock_Replacement/ <-- Priority 12: Clock Second Chance, LFU/MFU
        ├── 13_Thrashing_and_Working_Set_Model/   <-- Priority 13: CPU Thrashing, Working Set (Delta), PFF
        ├── 14_Locality_of_Reference_and_Cache_Organization/ <-- Priority 14: Temporal/Spatial Locality, Cache Mappings
        └── 15_Unit_4_AKTU_PYQs_and_Interview_Cheatsheet/ <-- Priority 15: AKTU PYQs, Formula Sheet, Interview Q&As
    └── Unit_5/                                  <-- Unit 5 Folder (Priorities 00 to 14)
        ├── README.md                            <-- Unit 5 Complete Roadmap
        ├── Unit_5_Quick_Revision_3_Page_Notes.pdf <-- 3-Page Rapid Recall PDF
        ├── Unit_5_Master_Notes.pdf              <-- 21-Page Consolidated Master PDF
        ├── 00_Quick_Revision_Short_Notes/       <-- Priority 00: 3-Page Ultra High-Yield Notes
        ├── 01_IO_Hardware_and_Kernel_Subsystems/ <-- Priority 01: Polling, Interrupts, DMA, Buffering, Spooling
        ├── 02_Disk_Storage_and_Physical_Architecture/ <-- Priority 02: Platters, Tracks, Sectors, Latency Math
        ├── 03_Disk_Scheduling_FCFS_and_SSTF/    <-- Priority 03: FCFS (640 cyl) vs SSTF (236 cyl), Starvation
        ├── 04_Disk_Scheduling_SCAN_and_CSCAN/   <-- Priority 04: SCAN Elevator (236 cyl) vs C-SCAN (382 cyl)
        ├── 05_Disk_Scheduling_LOOK_and_CLOOK/   <-- Priority 05: LOOK (208 cyl - Best) vs C-LOOK (322 cyl)
        ├── 06_RAID_Architecture_Levels_0_to_6/  <-- Priority 06: Striping, Mirroring, Parity, RAID 0-6 & 10
        ├── 07_File_Concept_and_Access_Methods/  <-- Priority 07: File Attributes, FCB, Sequential & Direct
        ├── 08_Directory_Structures_and_File_Sharing/ <-- Priority 08: Single/Two/Tree/Acyclic, Hard & Soft Links
        ├── 09_File_System_Implementation_and_VFS/ <-- Priority 09: Superblock, Inodes, Dentry, Linux VFS
        ├── 10_UNIX_Inode_Architecture_and_Calculations/ <-- Priority 10: Direct/Indirect Pointers, 4TB File Sizing
        ├── 11_File_Allocation_Methods/          <-- Priority 11: Contiguous, Linked, FAT, Indexed Allocations
        ├── 12_Free_Space_Management_Techniques/ <-- Priority 12: Bit Vector (Bitmap), Free List, Grouping, Counting
        ├── 13_File_System_Protection_and_Access_Matrix/ <-- Priority 13: Access Matrix, ACL, Capability, chmod 754
        └── 14_Unit_5_AKTU_PYQs_and_Interview_Cheatsheet/ <-- Priority 14: Solved 10-Markers, SSDs vs HDDs, FAANG Q&A
```

---

## 🛠️ Key Highlights
- **Priority-Driven Sequential Sorting:** Har unit ke folders sequential zero-padded prefixes (`00_` to `19_`, `00_` to `12_`, `00_` to `16_`, `00_` to `15_`) se organized hain jisse GitHub par automatically exact teaching order me top-to-bottom display hote hain.
- **Bilingual Hinglish Explanations:** Deep machine-level assembly traces, real-world intuitive analogies, edge cases aur semester exam answers.
- **Architectural Dark-Mode Diagrams:** Har module me custom vector SVG flowcharts aur diagrams shamil hain.
- **Single-Click Printable PDFs:** Har chapter ka standalone PDF aur poor unit ka all-in-one consolidated **Master PDF** available hai.
- **Strict 3-Page Recall Notes:** Revision ke liye exact 3 pages me condense kiye gaye rapid recall documents.

---
*Created for Computer Science Engineering Students & Aspiring Software Engineers by Shivam Keshari*