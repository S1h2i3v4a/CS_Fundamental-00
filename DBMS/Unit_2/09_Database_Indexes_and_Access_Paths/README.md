# Module 09: Database Indexes and Access Paths

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** B-Tree Index Architecture, Clustered vs Non-Clustered Indexes, Dense vs Sparse Indexing, and Query Optimization Trade-offs

---

## 1. What is a Database Index?

Database Index ek auxiliary data structure (usually a B+ Tree) hai jo disk blocks par stored data rows ko rapid access provide karta hai:
- **Without Index (Full Table Scan):** DBMS ko table ke har single disk block ko sequentially read karna padta hai ($O(N)$ Disk I/O).
- **With Index:** Binary search / tree traversal ke through desired row kuch hi block accesses mein mil jati hai ($O(\log N)$ Disk I/O).

---

## 2. Clustered vs Non-Clustered Index (10-Marker)

| Feature | Clustered Index | Non-Clustered (Secondary) Index |
| :--- | :--- | :--- |
| **Physical Data Order** | Data rows are **physically sorted** on disk in the order of the indexed key. | Physical data file untouched; index maintains a separate sorted B-Tree. |
| **Leaf Node Content** | Contains the **actual data rows** (pages). | Contains the **Search Key + Row Locator (RID/Pointer)** to data block. |
| **Allowed Count per Table** | **Only ONE** per table (data can only have one physical sort order). | **Multiple** allowed per table (e.g. up to 999 in SQL Server). |
| **Creation Mechanism** | Automatically created when `PRIMARY KEY` is defined. | Created explicitly using `CREATE INDEX` statement. |
| **Lookup Speed** | Fastest for range scans (`BETWEEN 10 AND 50`). | Incurs extra pointer indirection hop to read actual row. |

---

## 3. Dense Index vs Sparse Index

```
[ Dense Index ]:              [ Sparse Index ]:
(Every record has an index entry)  (Only first record of each block has entry)
 Index       Data File           Index       Data File
 [ 10 ] ----> [ 10 | Aman  ]     [ 10 ] ----> Block 1: [ 10 | Aman  ]
 [ 20 ] ----> [ 20 | Rohit ]                           [ 20 | Rohit ]
 [ 30 ] ----> [ 30 | Neha  ]     [ 30 ] ----> Block 2: [ 30 | Neha  ]
 [ 40 ] ----> [ 40 | Priya ]                           [ 40 | Priya ]
```

### Key Distinctions:
1. **Dense Index:**
   - Har single record ka index entry hota hai.
   - Faster point lookup.
   - Consumes high memory. Can be used on unsorted files.
2. **Sparse Index:**
   - Har disk block ke pehle record (Block Anchor) ka index entry hota hai.
   - Extremely small memory footprint (fits entirely in RAM).
   - **Strict Requirement:** Underlying data file **must be physically sorted** on the search key!

---

## 4. Composite & Unique Index Syntax
```sql
-- Composite index on multiple columns
CREATE INDEX idx_student_branch_cpi ON Student (Branch, CPI DESC);

-- Unique index to prevent duplicate entries
CREATE UNIQUE INDEX idx_emp_email ON Employee (Email);
```
