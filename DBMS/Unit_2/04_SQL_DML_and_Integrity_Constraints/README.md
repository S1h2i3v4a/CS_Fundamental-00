# Module 04: SQL DML and Integrity Constraints

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** Data Manipulation Language (`INSERT`, `UPDATE`, `DELETE`, `SELECT`), Table Constraints & Referential Integrity Cascade Actions

---

## 1. DML Commands Overview

DML (Data Manipulation Language) commands tables ke andar ke **data tuples** ko manipulate aur query karne ke liye use hote hain.
- DML statements transaction control ke under aate hain (`COMMIT` / `ROLLBACK` required to persist).

### 1.1 INSERT
```sql
-- Single row insert
INSERT INTO Employee (EmpID, Name, Dept, Salary)
VALUES (101, 'Aman Sharma', 'IT', 65000);

-- Bulk insert from another table
INSERT INTO High_Earners (EmpID, Name, Salary)
SELECT EmpID, Name, Salary FROM Employee WHERE Salary > 100000;
```

### 1.2 UPDATE
```sql
-- Increase IT department salary by 10%
UPDATE Employee
SET Salary = Salary * 1.10
WHERE Dept = 'IT';
```
> [!WARNING]
> Agar `UPDATE` query mein `WHERE` clause omit kar diya jaye, toh table ke **sabhi rows** modify ho jayenge!

### 1.3 DELETE
```sql
-- Delete inactive employees
DELETE FROM Employee
WHERE Status = 'Resigned';
```

---

## 2. SQL Integrity Constraints Hierarchy

Integrity constraints database mein invalid, corrupt ya inconsistent data ko enter hone se rokne ke liye rules enforce karte hain:

| Constraint | Enforcement Rule | NULL Behavior | Real-World Example |
| :--- | :--- | :--- | :--- |
| `NOT NULL` | Column cannot contain empty/missing values. | Disallows NULL | `Name VARCHAR(50) NOT NULL` |
| `UNIQUE` | Har row mein attribute value distinct honi chahiye. | Allows multiple NULLs (in SQL standard) | `Email VARCHAR(100) UNIQUE` |
| `PRIMARY KEY` | Uniquely identifies each record. (`NOT NULL + UNIQUE`). | **Strictly Disallows NULL** | `RollNo INT PRIMARY KEY` |
| `FOREIGN KEY` | Child table column must match parent table's Primary Key. | Allows NULL (unless marked NOT NULL) | `DeptID INT REFERENCES Dept(DeptID)` |
| `CHECK` | Enforces custom boolean validation condition. | Ignores NULL | `CHECK (Age >= 18 AND Salary > 0)` |
| `DEFAULT` | Auto-assigns fallback value agar insert statement value na de. | N/A | `Country VARCHAR(30) DEFAULT 'India'` |

---

## 3. Referential Integrity & Cascade Actions

Jab parent table mein se koi row DELETE ya UPDATE hoti hai jisko child table ki Foreign Key refer kar rahi hai, toh 4 actions define kiye ja sakte hain:

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    Amount DECIMAL(10, 2),
    CONSTRAINT fk_customer
        FOREIGN KEY (CustomerID)
        REFERENCES Customers(CustomerID)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

### The 4 Referential Actions:
1. **`ON DELETE CASCADE`:** Parent customer delete hone par uske **saare orders child table se automatically delete** ho jate hain.
2. **`ON DELETE SET NULL`:** Parent customer delete hone par child table mein `CustomerID` column **`NULL`** set ho jata hai.
3. **`ON DELETE SET DEFAULT`:** Parent delete hone par child key default fallback value par set ho jati hai.
4. **`ON DELETE RESTRICT` / `NO ACTION`:** Agar child table mein related orders exist karte hain, toh database system parent customer ko **delete karne se mana kar deta hai (Error thrown)!** (Default behavior).
