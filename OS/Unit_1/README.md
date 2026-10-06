# Operating System - Unit 1: Introduction, Architectures & System Structures

Yeh folder **Operating System (Unit 1 Complete Syllabus)** ke sabhi topics ko priority-wise, sequential do-digit format (`01_` to `19_`) mein organize karta hai taaki GitHub par exact hierarchical order mein display ho.

---

## ⚡ Quick Revision Short Notes (Last-Minute Recall)

> 🚀 **[00_Quick_Revision_Short_Notes](./00_Quick_Revision_Short_Notes/README.md)**  
> Poore Unit 1 ke sabhi 19 subtopics ko **sirf 3 pages** mein condense kiya gaya hai taaki exam ya interview se 10 minute pehle pure concepts rapidly recall ho sakein!  
> 📄 **[Download 3-Page Short Notes PDF (Instant Recall)](./Unit_1_Quick_Revision_3_Page_Notes.pdf)**

---

## 🗺️ Complete Unit 1 Roadmap (Priority 01 to 19)

| Priority | Module Subfolder | Key Concepts Covered | Visual Architectural Diagram | Chapter PDF |
| :---: | :--- | :--- | :---: | :---: |
| **00** | [00_Quick_Revision_Short_Notes](./00_Quick_Revision_Short_Notes/README.md) | **Unit 1 Ultra High-Yield 3-Page Cheat Sheet (All 19 Topics)** | Rapid Mind Map | [3-Page PDF](./Unit_1_Quick_Revision_3_Page_Notes.pdf) |
| **01** | [01_Introduction_to_OS](./01_Introduction_to_OS/README.md) | OS Definition, 3 Entities (H/W, App S/W, System S/W), 4 Components | [Concentric OS Architecture](./01_Introduction_to_OS/diagrams/os_position_diagram.svg) | [Download PDF](./01_Introduction_to_OS/01_Introduction_to_OS.pdf) |
| **02** | [02_Components_and_Abstract_View](./02_Components_and_Abstract_View/README.md) | Abstract Layered View, Translators, Hardware Resources | [Layered System Stack](./02_Components_and_Abstract_View/diagrams/computer_abstract_view.svg) | [Download PDF](./02_Components_and_Abstract_View/02_Components_and_Abstract_View.pdf) |
| **03** | [03_User_vs_System_View](./03_User_vs_System_View/README.md) | User View (Convenience) vs System View (Resource Manager), `a = b + c` trace | [Dual Perspective Layout](./03_User_vs_System_View/diagrams/user_vs_system_diagram.svg) | [Download PDF](./03_User_vs_System_View/03_User_vs_System_View.pdf) |
| **04** | [04_Kernel_and_Operations](./04_Kernel_and_Operations/README.md) | Kernel Bridge & 5 Core OS Functions, Monolithic vs Microkernel vs Hybrid | [Kernel Architecture & Types](./04_Kernel_and_Operations/diagrams/kernel_architecture_diagram.svg) | [Download PDF](./04_Kernel_and_Operations/04_Kernel_and_Operations.pdf) |
| **05** | [05_Computer_System_Organization](./05_Computer_System_Organization/README.md) | Common Bus, Device & Memory Controllers, Internal CPU (ALU, CU, Regs) | [System Bus & Multicore CPU](./05_Computer_System_Organization/diagrams/system_organization.svg) | [Download PDF](./05_Computer_System_Organization/05_Computer_System_Organization.pdf) |
| **06** | [06_Bootstrap_Program_and_Booting](./06_Bootstrap_Program_and_Booting/README.md) | Firmware (ROM/EPROM/EEPROM), POST, MBR/GPT, Kernel Handoff | [Bootstrapping Flowchart](./06_Bootstrap_Program_and_Booting/diagrams/bootstrapping_flow.svg) | [Download PDF](./06_Bootstrap_Program_and_Booting/06_Bootstrap_Program_and_Booting.pdf) |
| **07** | [07_Dual_Mode_Operation](./07_Dual_Mode_Operation/README.md) | User vs Kernel Mode, Mode Bit (1 ↔ 0), `printf()` Trap Execution Trace | [Dual-Mode Transition](./07_Dual_Mode_Operation/diagrams/dual_mode_operation.svg) | [Download PDF](./07_Dual_Mode_Operation/07_Dual_Mode_Operation.pdf) |
| **08** | [08_Memory_Management_Functions](./08_Memory_Management_Functions/README.md) | Primary Memory Byte Array, Base/Limit Memory Allocation & Protection | [Memory Partition Layout](./08_Memory_Management_Functions/diagrams/memory_management_layout.svg) | [Download PDF](./08_Memory_Management_Functions/08_Memory_Management_Functions.pdf) |
| **09** | [09_Memory_Hierarchy_and_Caching](./09_Memory_Hierarchy_and_Caching/README.md) | Memory Hierarchy Pyramid, Caching, AMAT Formula, Cache Coherency | [Cache Architecture & Hierarchy](./09_Memory_Hierarchy_and_Caching/diagrams/memory_hierarchy_cache.svg) | [Download PDF](./09_Memory_Hierarchy_and_Caching/09_Memory_Hierarchy_and_Caching.pdf) |
| **10** | [10_Processor_Management_and_Scheduling](./10_Processor_Management_and_Scheduling/README.md) | Process Lifecycle, PCB, Multiprogramming, Context Switch Latency Trace | [Processor Dispatching & PCB](./10_Processor_Management_and_Scheduling/diagrams/processor_management.svg) | [Download PDF](./10_Processor_Management_and_Scheduling/10_Processor_Management_and_Scheduling.pdf) |
| **11** | [11_Device_and_File_Management](./11_Device_and_File_Management/README.md) | Device Drivers & Uniform Interface, File CRUD, Inodes, File Read Journey | [Hierarchical Directory & Driver](./11_Device_and_File_Management/diagrams/device_and_file_management.svg) | [Download PDF](./11_Device_and_File_Management/11_Device_and_File_Management.pdf) |
| **12** | [12_User_Interface_and_Specialized_OS_Functions](./12_User_Interface_and_Specialized_OS_Functions/README.md) | CLI vs GUI vs Touch, Cold vs Warm Booting, Protection, Accounting, Debugging | [UI Types & Boot Diagnostic Flow](./12_User_Interface_and_Specialized_OS_Functions/diagrams/ui_and_booting_diagram.svg) | [Download PDF](./12_User_Interface_and_Specialized_OS_Functions/12_User_Interface_and_Specialized_OS_Functions.pdf) |
| **13** | [13_Types_of_Operating_Systems_Batch_and_Multiprogrammed](./13_Types_of_Operating_Systems_Batch_and_Multiprogrammed/README.md) | Batch OS (Punch Cards, Operator), Spooling FIFO, Multiprogramming ($1 - p^n$) | [Batch Execution & Spooler FIFO](./13_Types_of_Operating_Systems_Batch_and_Multiprogrammed/diagrams/batch_and_multiprogramming.svg) | [Download PDF](./13_Types_of_Operating_Systems_Batch_and_Multiprogrammed/13_Types_of_Operating_Systems_Batch_and_Multiprogrammed.pdf) |
| **14** | [14_Time_Sharing_and_Real_Time_Systems](./14_Time_Sharing_and_Real_Time_Systems/README.md) | Time Slice $q$, Round Robin Preemption, Hard vs Soft RTOS Deadlines | [Gantt Chart & RTOS Deadline Curves](./14_Time_Sharing_and_Real_Time_Systems/diagrams/timesharing_and_rtos.svg) | [Download PDF](./14_Time_Sharing_and_Real_Time_Systems/14_Time_Sharing_and_Real_Time_Systems.pdf) |
| **15** | [15_Multiprocessor_and_Distributed_Systems](./15_Multiprocessor_and_Distributed_Systems/README.md) | Flynn's Taxonomy, SMP vs ASMP, Multiuser Quotas, Heavyweight Process vs Threads | [SMP Architecture & Thread Models](./15_Multiprocessor_and_Distributed_Systems/diagrams/multiprocessor_multithreaded.svg) | [Download PDF](./15_Multiprocessor_and_Distributed_Systems/15_Multiprocessor_and_Distributed_Systems.pdf) |
| **16** | [16_Operating_System_Structures_and_Architectures](./16_Operating_System_Structures_and_Architectures/README.md) | MS-DOS, Monolithic, Layered ($N \to N-1$), Microkernel, Modular LKMs (Linux) | [4-in-1 OS Structures Comparison](./16_Operating_System_Structures_and_Architectures/diagrams/os_structures.svg) | [Download PDF](./16_Operating_System_Structures_and_Architectures/16_Operating_System_Structures_and_Architectures.pdf) |
| **17** | [17_Advanced_Kernel_and_System_Calls](./17_Advanced_Kernel_and_System_Calls/README.md) | Reentrant Kernel Concurrency, 6-Stage Syscall Lifecycle, Parameter Passing | [Reentrant Kernel & Syscall Trap Trace](./17_Advanced_Kernel_and_System_Calls/diagrams/reentrant_and_syscall.svg) | [Download PDF](./17_Advanced_Kernel_and_System_Calls/17_Advanced_Kernel_and_System_Calls.pdf) |
| **18** | [18_OS_Services_and_System_Components](./18_OS_Services_and_System_Components/README.md) | Layered Services Stack (Slide 130), 8 Core Subsystems (Slide 135) | [Services Architecture & 8 Subsystems](./18_OS_Services_and_System_Components/diagrams/os_services_components.svg) | [Download PDF](./18_OS_Services_and_System_Components/18_OS_Services_and_System_Components.pdf) |
| **19** | [19_AKTU_PYQs_and_Interview_Cheatsheet](./19_AKTU_PYQs_and_Interview_Cheatsheet/README.md) | 10 Years AKTU Solved Questions (2014-2023), Interview Q&A, Formula Cheatsheet | [Unit 1 Complete Knowledge Graph](./19_AKTU_PYQs_and_Interview_Cheatsheet/diagrams/unit1_mindmap.svg) | [Download PDF](./19_AKTU_PYQs_and_Interview_Cheatsheet/19_AKTU_PYQs_and_Interview_Cheatsheet.pdf) |

---

## 📚 Master Consolidated PDF Documents
- 📄 **[Unit_1_Quick_Revision_3_Page_Notes.pdf](./Unit_1_Quick_Revision_3_Page_Notes.pdf)** (Exact 3-Page Ultra Condensed Sheet for Rapid Recall)
- 📄 **[Unit_1_Master_Notes.pdf](./Unit_1_Master_Notes.pdf)** (Complete 58-Page Master Document, All 19 Modules Consolidated)

---
*Created for CS Fundamentals Repository by Shivam Keshari*
