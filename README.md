# Computer Science Fundamentals Repository

Welcome to the **CS Fundamentals** repository! Yeh repository Computer Science ke core subjects (Operating Systems, Computer Architecture, Memory Hierarchy, Scheduling, Kernels, Concurrent Processes, Synchronization, IPC, System Calls, and Exam PYQs) ke high-yield, interview-focused, aur structured notes provide karta hai.

---

## ⚡ Quick Revision Short Notes (Rapid Recall)
- 📄 **[Unit 1: 3-Page Quick Revision Short Notes (PDF)](./OS/Unit_1/Unit_1_Quick_Revision_3_Page_Notes.pdf)**: Complete Unit 1 condensed into **EXACT 3 PAGES**!
- 📄 **[Unit 2: 3-Page Quick Revision Short Notes (PDF)](./OS/Unit_2/Unit_2_Quick_Revision_3_Page_Notes.pdf)**: Complete Unit 2 (Concurrency & Synchronization) condensed into **EXACT 3 PAGES**!
- 📘 **[Unit 1 Short Notes Guide](./OS/Unit_1/00_Quick_Revision_Short_Notes/README.md)** | **[Unit 2 Short Notes Guide](./OS/Unit_2/00_Quick_Revision_Short_Notes/README.md)**

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
    └── Unit_2/                                  <-- Unit 2 Folder (Priorities 00 to 12)
        ├── README.md                            <-- Unit 2 Complete Roadmap
        ├── Unit_2_Quick_Revision_3_Page_Notes.pdf <-- 3-Page Rapid Recall PDF
        ├── Unit_2_Master_Notes.pdf              <-- 17-Page Consolidated Master PDF
        ├── 00_Quick_Revision_Short_Notes/       <-- Priority 00: 3-Page Ultra High-Yield Notes
        ├── 01_Process_Concept_and_Concurrency_Principles/ <-- Priority 01: Race Conditions, Cooperating Processes
        ├── 02_Critical_Section_Problem_and_Criteria/      <-- Priority 02: 4 Sections, 4 Criteria (Mutual Exclusion, Progress)
        ├── 03_Software_Solutions_Peterson_Algorithm/      <-- Priority 03: Peterson's 2-Process Algorithm & Trace
        ├── 04_Software_Solutions_Dekker_Algorithm/        <-- Priority 04: Dekker's Algorithm & Back-off Loop
        ├── 05_Hardware_Synchronization_Test_and_Set/      <-- Priority 05: Atomic TSL, Swap, Spinlocks & Busy Wait
        ├── 06_Semaphores_and_Mutexes/                     <-- Priority 06: Counting vs Binary, Block-Wakeup Queue
        ├── 07_Producer_Consumer_Problem/                  <-- Priority 07: Bounded Buffer, Assembly Race, Deadlock Trap
        ├── 08_Readers_Writers_Problem/                    <-- Priority 08: Reader Priority, First-In Last-Out Lock, Starvation
        ├── 09_Dining_Philosophers_and_Sleeping_Barber/    <-- Priority 09: Circular Wait Deadlock, Barber Queue & Dropout
        ├── 10_Process_Generation_and_Lifecycle/           <-- Priority 10: fork(), 2^n Process Tree, Zombie vs Orphan
        ├── 11_Inter_Process_Communication_IPC/            <-- Priority 11: Shared Memory vs Message Passing, Sync Semantics
        └── 12_Unit_2_AKTU_PYQs_and_Interview_Cheatsheet/  <-- Priority 12: AKTU PYQs (2014-2023) Solved, Concurrency Mindmap
```

---

## 🚀 Key Highlights of this Repository
1. **Ultra High-Yield 3-Page Short Notes:** Har Unit exact 3 pages mein available hai quick recall ke liye ([Unit 1](./OS/Unit_1/Unit_1_Quick_Revision_3_Page_Notes.pdf) & [Unit 2](./OS/Unit_2/Unit_2_Quick_Revision_3_Page_Notes.pdf)).
2. **Perfect GitHub Sorting:** Sabhi subfolders ko zero-padded prefixes (`00_`, `01_`...) diye gaye hain taaki GitHub file browser mein 100% sequential priority order dikhe.
3. **Hinglish Intuition:** Relatable, clear Hinglish bhasha mein technical concepts explain kiye gaye hain.
4. **Step-by-Step Code & Execution Traces:** Peterson's turn trace, Dekker's collision resolution, Assembly race conditions on shared `count`, `fork()` process trees ($2^n$).
5. **Architectural SVG Diagrams:** Dark/Tech-themed high-resolution vector diagrams jo print aur digital reading dono ke liye optimized hain.

---
*Maintained by Shivam Keshari*
