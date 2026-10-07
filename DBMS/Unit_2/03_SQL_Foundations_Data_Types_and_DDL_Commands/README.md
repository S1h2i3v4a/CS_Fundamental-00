# Module 03: SQL Foundations, Data Types, and DDL Commands

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** SQL Characteristics, Data Types & Literals, DDL Lifecycle (`CREATE`, `ALTER`, `DROP`, `TRUNCATE`), and the classic DROP vs TRUNCATE vs DELETE comparison

---

## 1. SQL Overview & Characteristics

**SQL (Structured Query Language)** relational databases ke saath interact karne ke liye ANSI/ISO standard language hai.
- **Declarative Nature:** User specifies *what* data is needed, query optimizer plans *how* to access it.
- **Relational Completeness:** Relational Algebra aur Tuple Relational Calculus dono ko natively implement karti hai.
- **Unified Language:** Ek hi language ke through data definition, data manipulation, access control, aur transaction control handle hota hai.

---

## 2. SQL Data Types & Storage

| Data Type Category | Type Name | Working & Characteristics | Real-World Use Case |
| :--- | :--- | :--- | :--- |
| **Fixed String** | `CHAR(n)` | Fixed length $n$ characters. Shorter strings pad with trailing spaces. | Country codes (`IN`, `US`), Gender (`M`, `F`). |
| **Variable String** | `VARCHAR(n)` / `VARCHAR2(n)` | Variable length up to $n$ characters. No trailing space waste. | Customer Name, Email, Address. |
| **Integers** | `INT`, `BIGINT`, `SMALLINT` | Exact numeric whole values without fractions. | Roll Numbers, Quantity, Counts. |
| **Exact Decimals** | `DECIMAL(p, s)` / `NUMERIC` | Precision $p$ (total digits) with scale $s$ (decimal digits). | Currency, Bank balances (`DECIMAL(12, 2)`). |
| **Temporal** | `DATE`, `TIME`, `TIMESTAMP` | Calendar date (YYYY-MM-DD), Time, and Fractional seconds. | Birth dates, Order timestamps. |
| **Large Objects** | `BLOB`, `CLOB` | Binary Large Object & Character Large Object (Gigabytes). | Profile photos, PDF resumes, JSON text. |

---

## 3. SQL Commands Taxonomy

```
                                [ SQL Commands ]
       ┌──────────────────┬──────────────┴──────────────┬──────────────────┐
       ▼                  ▼                             ▼                  ▼
     [ DDL ]           [ DML ]                       [ DCL ]            [ TCL ]
 Data Definition   Data Manipulation               Data Control       Transaction
  CREATE, ALTER,    SELECT, INSERT,                GRANT, REVOKE        COMMIT,
  DROP, TRUNCATE    UPDATE, DELETE                                     ROLLBACK
  (Auto-Commit)     (Requires Commit)
```

---

## 4. DDL Commands (Data Definition Language)

DDL commands database schema objects (tables, views, indexes) ke structure ko define aur modify karte hain. **Yeh operations auto-committed hote hain (cannot be rolled back)!**

### 4.1 CREATE TABLE
```sql
CREATE TABLE Student (
    RollNo INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Branch VARCHAR(10) DEFAULT 'CSE',
    CPI DECIMAL(3, 2),
    EnrollDate DATE
);
```

### 4.2 ALTER TABLE (4 Sub-Variants)
1. **ADD a new column:**
   ```sql
   ALTER TABLE Student ADD Email VARCHAR(100);
   ```
2. **DROP an existing column:**
   ```sql
   ALTER TABLE Student DROP COLUMN Email;
   ```
3. **MODIFY column data type or constraint:**
   ```sql
   ALTER TABLE Student MODIFY Name VARCHAR(100);
   ```
4. **RENAME a column:**
   ```sql
   ALTER TABLE Student RENAME COLUMN CPI TO CGPA;
   ```

### 4.3 DROP TABLE vs TRUNCATE TABLE vs DELETE (AKTU 10-Marker Classic)

| Parameter | `DROP TABLE` | `TRUNCATE TABLE` | `DELETE FROM` |
| :--- | :--- | :--- | :--- |
| **Command Category** | **DDL** (Data Definition) | **DDL** (Data Definition) | **DML** (Data Manipulation) |
| **Effect on Schema** | Table **Schema + Data dono delete** ho jate hain. | Table **Data delete** hota hai; **Schema preserved** rehti hai. | Table **Data delete** hota hai; **Schema preserved** rehti hai. |
| **WHERE Clause** | Not Applicable. | **Not supported** (all rows purged). | **Supported** (`WHERE id = 5`). |
| **Rollback Capability** | **Cannot be rolled back** (Auto-commit). | **Cannot be rolled back** (Auto-commit). | **Can be rolled back** (Undo log maintained). |
| **Execution Speed** | Very Fast. | **Lightning Fast** (Deallocates pages, resets HWM). | Slower (Row-by-row deletion & logging). |
| **Triggers Fired** | DROP trigger only. | No DELETE triggers fire! | Fires `ON DELETE` triggers for each row. |
