# DBMS Unit 5: Concurrency Control Techniques

> **Subject:** Database Management System (DBMS)  
> **AKTU Course Code:** BCS501  
> **Source Material:** Gateway Classes AKTU One-Shot Lecture Slides (72 Pages)  
> **Author:** Antigravity High-Yield Engineering Architecture  
> **Repository:** [CS_Fundamental-00/DBMS/Unit_5](https://github.com/S1h2i3v4a/CS_Fundamental-00/tree/main/DBMS/Unit_5)

---

## ⚡ Direct Download Access

| Deliverable | Description | Pages | Direct Link |
| :--- | :--- | :--- | :--- |
| **🚀 3-Page Ultra Revision Sheet** | Formulae, 2PL Variants, Thomas' Write Rule, 5x5 MGL Matrix, MGL Rules, and Oracle MVCC | **Exact 3 Pages** | [Unit_5_Quick_Revision_3_Page_Notes.pdf](Unit_5_Quick_Revision_3_Page_Notes.pdf) |
| **📘 Complete Master Notes PDF** | Consolidated textbook merging all 15 module chapters with Table of Contents bookmarks | **Full Coverage** | [Unit_5_Master_Notes.pdf](Unit_5_Master_Notes.pdf) |

---

## 📑 Complete Curriculum Modules Directory

| # | Module Folder | Key Topics Covered | SVG Diagram | Chapter PDF |
| :-: | :--- | :--- | :---: | :---: |
| **00** | [00_Quick_Revision_Short_Notes](00_Quick_Revision_Short_Notes/) | 3-Page Ultra High-Yield Master Exam Sheet, 5x5 Matrix, Mindmap | [SVG](00_Quick_Revision_Short_Notes/diagrams/unit5_quick_revision_mindmap.svg) | [PDF](00_Quick_Revision_Short_Notes/00_Quick_Revision_Short_Notes.pdf) |
| **01** | [01_Concurrency_Control_Foundations_and_Locking_Basics](01_Concurrency_Control_Foundations_and_Locking_Basics/) | Concurrency Control Need, Binary vs Shared/Exclusive Locks, Compatibility | [SVG](01_Concurrency_Control_Foundations_and_Locking_Basics/diagrams/concurrency_control_foundations_and_locking_basics.svg) | [PDF](01_Concurrency_Control_Foundations_and_Locking_Basics/01_Concurrency_Control_Foundations_and_Locking_Basics.pdf) |
| **02** | [02_Two_Phase_Locking_Protocol_and_Lock_Conversion](02_Two_Phase_Locking_Protocol_and_Lock_Conversion/) | Growing/Shrinking Phases, Lock Point, Upgrade/Downgrade Algorithms | [SVG](02_Two_Phase_Locking_Protocol_and_Lock_Conversion/diagrams/two_phase_locking_and_lock_conversion.svg) | [PDF](02_Two_Phase_Locking_Protocol_and_Lock_Conversion/02_Two_Phase_Locking_Protocol_and_Lock_Conversion.pdf) |
| **03** | [03_Two_Phase_Locking_Variants_Strict_Rigorous_Conservative](03_Two_Phase_Locking_Variants_Strict_Rigorous_Conservative/) | Basic, Conservative (Deadlock-Free), Strict (Cascadeless), Rigorous 2PL | [SVG](03_Two_Phase_Locking_Variants_Strict_Rigorous_Conservative/diagrams/two_phase_locking_protocol_variants.svg) | [PDF](03_Two_Phase_Locking_Variants_Strict_Rigorous_Conservative/03_Two_Phase_Locking_Variants_Strict_Rigorous_Conservative.pdf) |
| **04** | [04_Timestamp_Ordering_Protocols](04_Timestamp_Ordering_Protocols/) | TS Allocation, read_TS, write_TS, Basic TO Read/Write Rules, Deadlock-Free | [SVG](04_Timestamp_Ordering_Protocols/diagrams/basic_timestamp_ordering_protocol.svg) | [PDF](04_Timestamp_Ordering_Protocols/04_Timestamp_Ordering_Protocols.pdf) |
| **05** | [05_Thomas_Write_Rule_and_View_Serializability](05_Thomas_Write_Rule_and_View_Serializability/) | Obsolete Write Suppression, View Serializability (VSR), Solved Trace | [SVG](05_Thomas_Write_Rule_and_View_Serializability/diagrams/thomas_write_rule_and_view_serializability.svg) | [PDF](05_Thomas_Write_Rule_and_View_Serializability/05_Thomas_Write_Rule_and_View_Serializability.pdf) |
| **06** | [06_Multiversion_Concurrency_Control_MVCC_and_MVTO](06_Multiversion_Concurrency_Control_MVCC_and_MVTO/) | Version Chains, Non-Blocking Readers, MVTO Read/Write Rules, Vacuuming | [SVG](06_Multiversion_Concurrency_Control_MVCC_and_MVTO/diagrams/mvcc_architecture_and_mvto_protocol.svg) | [PDF](06_Multiversion_Concurrency_Control_MVCC_and_MVTO/06_Multiversion_Concurrency_Control_MVCC_and_MVTO.pdf) |
| **07** | [07_Multiversion_Two_Phase_Locking_MV2PL_and_Certify_Locks](07_Multiversion_Two_Phase_Locking_MV2PL_and_Certify_Locks/) | Read Lock (RL), Write Lock (WL), Certify Lock (CL), 3x3 Matrix, Commit Phase | [SVG](07_Multiversion_Two_Phase_Locking_MV2PL_and_Certify_Locks/diagrams/mv2pl_locks_and_certify_protocol.svg) | [PDF](07_Multiversion_Two_Phase_Locking_MV2PL_and_Certify_Locks/07_Multiversion_Two_Phase_Locking_MV2PL_and_Certify_Locks.pdf) |
| **08** | [08_Validation_Based_Protocol_Optimistic_Concurrency_Control](08_Validation_Based_Protocol_Optimistic_Concurrency_Control/) | OCC 3 Phases (Read, Validate, Write), 3 Validation Conditions, Phantoms | [SVG](08_Validation_Based_Protocol_Optimistic_Concurrency_Control/diagrams/validation_based_protocol_and_occ_phases.svg) | [PDF](08_Validation_Based_Protocol_Optimistic_Concurrency_Control/08_Validation_Based_Protocol_Optimistic_Concurrency_Control.pdf) |
| **09** | [09_Granularity_of_Data_Items_and_Hierarchy](09_Granularity_of_Data_Items_and_Hierarchy/) | Fine vs Coarse Granularity, Hierarchy Tree (db -> f -> p -> r) | [SVG](09_Granularity_of_Data_Items_and_Hierarchy/diagrams/granularity_hierarchy_and_tradeoffs.svg) | [PDF](09_Granularity_of_Data_Items_and_Hierarchy/09_Granularity_of_Data_Items_and_Hierarchy.pdf) |
| **10** | [10_Multiple_Granularity_Locking_and_Intention_Locks](10_Multiple_Granularity_Locking_and_Intention_Locks/) | IS, IX, SIX Modes, Master 5x5 Lock Compatibility Matrix (Slide 69) | [SVG](10_Multiple_Granularity_Locking_and_Intention_Locks/diagrams/intention_locks_and_compatibility_matrix.svg) | [PDF](10_Multiple_Granularity_Locking_and_Intention_Locks/10_Multiple_Granularity_Locking_and_Intention_Locks.pdf) |
| **11** | [11_Multiple_Granularity_Locking_Protocol_Rules](11_Multiple_Granularity_Locking_Protocol_Rules/) | The 6 MGL Rules (Slide 70), Top-Down Locking, Bottom-Up Unlocking | [SVG](11_Multiple_Granularity_Locking_Protocol_Rules/diagrams/mgl_protocol_rules_and_tree_walkthrough.svg) | [PDF](11_Multiple_Granularity_Locking_Protocol_Rules/11_Multiple_Granularity_Locking_Protocol_Rules.pdf) |
| **12** | [12_Recovery_with_Concurrent_Transactions_and_2PC](12_Recovery_with_Concurrent_Transactions_and_2PC/) | Concurrent Recovery, Undo/Redo Checkpoints, Two-Phase Commit (2PC) | [SVG](12_Recovery_with_Concurrent_Transactions_and_2PC/diagrams/concurrent_recovery_and_2pc_protocol.svg) | [PDF](12_Recovery_with_Concurrent_Transactions_and_2PC/12_Recovery_with_Concurrent_Transactions_and_2PC.pdf) |
| **13** | [13_Case_Study_of_Oracle_Concurrency_Control](13_Case_Study_of_Oracle_Concurrency_Control/) | SCN, Undo Segments, Multi-Version Read Consistency, ORA-01555, Row Locks | [SVG](13_Case_Study_of_Oracle_Concurrency_Control/diagrams/oracle_concurrency_control_and_undo_architecture.svg) | [PDF](13_Case_Study_of_Oracle_Concurrency_Control/13_Case_Study_of_Oracle_Concurrency_Control.pdf) |
| **14** | [14_Unit_5_AKTU_PYQs_and_Solved_Problems](14_Unit_5_AKTU_PYQs_and_Solved_Problems/) | AKTU 10-Mark University Solutions: 2PL vs TO, MGL Matrix, Thomas Rule, Oracle | [SVG](14_Unit_5_AKTU_PYQs_and_Solved_Problems/diagrams/aktu_unit5_master_decision_flowchart.svg) | [PDF](14_Unit_5_AKTU_PYQs_and_Solved_Problems/14_Unit_5_AKTU_PYQs_and_Solved_Problems.pdf) |

---

## 🎯 Master Exam Formulae & Rules (AKTU BCS501)

1. **Multiple Granularity Locking (MGL) Rules:**
   - Locking is strictly **TOP-DOWN** starting at root ($db$).
   - Unlocking is strictly **BOTTOM-UP** starting at leaves (records).
   - Node locked in $S$ or $IS \implies$ Parent must have $IS$ or $IX$.
   - Node locked in $X, IX, SIX \implies$ Parent must have $IX$ or $SIX$.
2. **Master 5x5 Compatibility Matrix:**
   - $IS$ is compatible with everything EXCEPT $X$.
   - $X$ is incompatible with EVERY lock mode.
   - $IX$ is compatible only with $IS$ and $IX$.
   - $SIX$ is compatible only with $IS$.
3. **Thomas' Write Rule:**
   - If $TS(T) < write\_TS(X) \implies$ **IGNORE (Discard) write and CONTINUE**! Guarantees View Serializability without aborting.
4. **Conservative 2PL vs Strict 2PL:**
   - Conservative 2PL = Pre-declares all locks $\implies$ **100% Deadlock-Free**.
   - Strict 2PL = Holds exclusive locks till commit $\implies$ **Strict & Cascadeless Recovery**.
