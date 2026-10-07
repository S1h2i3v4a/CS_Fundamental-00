# Module 00: Unit 5 Ultra Quick Revision (3-Page Recall Notes)

> **Unit 5: I/O Systems, Disk Scheduling, RAID & File Management** | *B.Tech CS/IT/Allied (AKTU BCS401)*

---

## 1. Quick Revision PDF Overview
Yeh document Unit 5 ka **exact 3-page ultra high-yield revision sheet** hai. Isme exam se pehle 15 minute me poori unit recall karne ke liye saare key formulas, scheduling traces, RAID architectures, UNIX inode derivations aur free space management schemes concisely pack kiye gaye hain.

- **Standalone Verified PDF:** [`Unit_5_Quick_Revision_3_Page_Notes.pdf`](./Unit_5_Quick_Revision_3_Page_Notes.pdf) *(Verified: Strictly 3 Pages)*
- **Root Unit PDF:** [`../Unit_5_Quick_Revision_3_Page_Notes.pdf`](../Unit_5_Quick_Revision_3_Page_Notes.pdf)
- **Interactive HTML:** [`Unit_5_Quick_Revision_3_Page_Notes.html`](./Unit_5_Quick_Revision_3_Page_Notes.html)

---

## 2. 3-Page Structure Summary

### Page 1: I/O Hardware, Kernel Subsystems & Disk Storage
- **I/O Hardware Architecture:** Device Controller registers (Data-in, Data-out, Status, Control), PMIO vs MMIO.
- **Polling vs Interrupts:** Busy-waiting trade-offs, Interrupt Vector Table (IVT), Maskable vs Non-Maskable (NMI).
- **Direct Memory Access (DMA):** DMAC architecture, Cycle Stealing, 1 interrupt per block.
- **Kernel I/O Subsystem:** I/O Scheduling, Buffering (Single, Double Ping-Pong, Circular), Caching vs Spooling.
- **Physical Disk Geometry:** Platters, Tracks, Sectors, Cylinders, Spindle, Moving R/W Heads.
- **Access Time Formulas:** $T_{\text{access}} = T_{\text{seek}} + T_{\text{rotational}} + T_{\text{transfer}} + T_{\text{controller}}$. Average rotational latency formula ($30000 / \text{RPM}$ ms) with solved numerical.

### Page 2: Disk Scheduling & RAID Architecture
- **Disk Scheduling Master Benchmark:** 8 requests (`98, 183, 37, 122, 14, 124, 65, 67`), Head `53`, Range `0-199`.
  - FCFS: 640 cylinders (Wild mechanical oscillations).
  - SSTF: 236 cylinders (Greedy, starvation risk).
  - SCAN (Elevator): 236 cylinders (Travels to boundary 199).
  - C-SCAN: 382 cylinders (Uniform wait, circular return sweep).
  - **LOOK: 208 cylinders (Most optimal, reverses at max request).**
  - C-LOOK: 322 cylinders (Uniform wait without touching boundaries).
- **RAID Levels 0 to 6 & 10:**
  - Core Techniques: Striping (Speed), Mirroring (Fault tolerance), Parity (XOR recovery).
  - Comprehensive comparison: Usable capacity, minimum disks, fault tolerance, write penalty.
  - RAID 5 Distributed Parity 4-I/O write penalty derivation ($2\text{ reads} + 2\text{ writes}$).
  - RAID 10 (1+0) vs RAID 01 (0+1) reliability.

### Page 3: File Systems, Inodes, Allocation & Protection
- **File & Directory Concepts:** FCB / Inode metadata, Single/Two/Tree/Acyclic Graph structures, Hard links vs Soft/Symbolic links.
- **Virtual File System (VFS):** Superblock, Inode, Dentry (dcache), and File objects.
- **File Allocation Methods:** Contiguous, Linked, FAT, Indexed allocation comparison table.
- **UNIX Inode Architecture:** 12 Direct, 1 Single, 1 Double, 1 Triple Indirect derivation; Max file size $\approx 4\text{ TB}$ calculation.
- **Free Space Management:** Bit Vector / Bitmap calculation ($O(1)$ hardware instructions, RAM overhead formula), Linked Free List, Grouping, Counting.
- **Protection & Security:** Access Matrix model, ACL vs Capability Lists, UNIX 9-bit octal permissions (`chmod 754`), SUID, SGID, Sticky bit.
