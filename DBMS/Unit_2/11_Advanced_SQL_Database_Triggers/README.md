# Module 11: Advanced SQL — Database Triggers

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** Event-Condition-Action (ECA) Model, Trigger Timing (`BEFORE` vs `AFTER`), Trigger Granularity (`FOR EACH ROW`), Pseudo-Records (`:NEW` & `:OLD`), and Solved Audit Triggers

---

## 1. What is a Database Trigger?

Trigger ek special **stored PL/SQL block** hota hai jo kisi specified database event ke occur hone par **automatically execute (fire)** ho jata hai:
- User ya application ko trigger call karne ki zaroorat nahi hoti (unlike Stored Procedures).
- **ECA Model:**
  - **Event:** DML Operation (`INSERT`, `UPDATE`, `DELETE`) on target table.
  - **Condition:** Optional `WHEN` boolean filter.
  - **Action:** PL/SQL execution block.

---

## 2. Trigger Classifications

### 2.1 Timing: BEFORE vs AFTER
- **`BEFORE` Trigger:** Database table update hone se **pehle** fire hota hai. Input data ko validate, sanitize ya unauthorized operations ko `RAISE_APPLICATION_ERROR` ke through abort karne ke liye use hota hai.
- **`AFTER` Trigger:** Table successfully update hone ke **baad** fire hota hai. Auditing, historical change logs maintain karne, aur external systems ko synchronize karne ke liye ideal hai.

### 2.2 Granularity: Row-Level vs Statement-Level
- **Row-Level (`FOR EACH ROW`):** DML statement se affect hone wale **har single row** ke liye alag se fire hota hai. Isme `:NEW` aur `:OLD` variables ka access hota hai.
- **Statement-Level (Default):** Pooray SQL command ke liye **sirf 1 baar** fire hota hai (chahe statement ne 1 row update kiya ho ya 10,000 rows).

---

## 3. Pseudo-Records: `:NEW` and `:OLD`

| Event Type | `:OLD` Value | `:NEW` Value |
| :--- | :--- | :--- |
| **`INSERT`** | `NULL` (No prior record exists) | Contains incoming values being inserted. |
| **`UPDATE`** | Contains values **before** update. | Contains new values **after** update. |
| **`DELETE`** | Contains values of record being deleted. | `NULL` (Row is purged). |

---

## 4. Solved AKTU Case Studies (10-Marker)

### Case Study 1: Prevent Salary Reduction Trigger
```sql
CREATE OR REPLACE TRIGGER trg_prevent_salary_decrease
BEFORE UPDATE OF Salary ON Employee
FOR EACH ROW
BEGIN
    IF :NEW.Salary < :OLD.Salary THEN
        RAISE_APPLICATION_ERROR(-20001, 'Violation: Salary cannot be decreased from current value ' || :OLD.Salary);
    END IF;
END;
/
```

### Case Study 2: Employee Audit Logging Trigger
```sql
CREATE OR REPLACE TRIGGER trg_emp_audit
AFTER INSERT OR DELETE ON Employee
FOR EACH ROW
BEGIN
    IF INSERTING THEN
        INSERT INTO Emp_Audit_Log (EmpID, Action, ChangeDate, ChangedBy)
        VALUES (:NEW.EmpID, 'INSERT', SYSDATE, USER);
    ELSIF DELETING THEN
        INSERT INTO Emp_Audit_Log (EmpID, Action, ChangeDate, ChangedBy)
        VALUES (:OLD.EmpID, 'DELETE', SYSDATE, USER);
    END IF;
END;
/
```
