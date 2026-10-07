# Module 08: SQL Views and Security Abstraction

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** Virtual Tables Architecture, Security Column Masking, Updatability Rules, `WITH CHECK OPTION`, and Materialized Views

---

## 1. What is a View in SQL?

View ek **Virtual Table** hoti hai jo underlying base tables par ek SELECT query ke through dynamically construct hoti hai:
- **No Physical Disk Storage:** View ka apna koi physical data disk par store nahi hota (except the SQL query definition stored in the DBMS data dictionary).
- Jab bhi user view ko query karta hai (`SELECT * FROM ViewName`), DBMS query engine underlying SELECT query ko dynamically execute karke fresh data stream render karta hai.

```sql
CREATE VIEW Student_Public AS
SELECT RollNo, Name, Branch
FROM Student; -- Hides sensitive columns like FeePending, Mobile, Marks
```

---

## 2. Core Advantages of Views

1. **Security & Column Masking:** Sensitive columns (Salary, Password hashes) ko end users aur analysts se hide karna.
2. **Query Complexity Abstraction:** 4-5 tables ke complicated joins ko abstract karke simple single-table interface provide karna.
3. **Logical Data Independence:** Agar base table structure modify hota hai, toh view definition update karke client applications ko bina code rewrite ke smooth chalaya ja sakta hai.

---

## 3. Updatable Views vs Read-Only Views

Kya hum kisi View par `INSERT`, `UPDATE`, ya `DELETE` perform kar sakte hain?
- **Answer:** Sirf tab jab view **Updatable View** ho!

### Criteria for Updatable Views:
Ek view par modifications allow hoti hain agar aur sirf agar:
1. View exactly **ek single base table** par constructed ho (No multiple table joins).
2. Base table ki **Primary Key** view ke projected columns mein included ho.
3. Query mein koi **Aggregate function** (`SUM`, `AVG`, `COUNT`) na ho.
4. Query mein koi **`GROUP BY`**, **`HAVING`**, ya **`DISTINCT`** clause na ho.
5. Base table ke sabhi `NOT NULL` columns (jinme default value nahi hai) view mein maujood hon.

---

## 4. `WITH CHECK OPTION` (Integrity Enforcer)

Agar view updatable hai, toh user aisi row insert ya update kar sakta hai jo view ke `WHERE` clause ko violate kar de!
- `WITH CHECK OPTION` clause ensure karta hai ki koi bhi DML operation view ke filtering condition ko satisfy kare, warna operation reject ho jata hai.

```sql
CREATE VIEW IT_Employees AS
SELECT EmpID, Name, Dept, Salary
FROM Employee
WHERE Dept = 'IT'
WITH CHECK OPTION;

-- Allowed:
INSERT INTO IT_Employees VALUES (105, 'Rohan', 'IT', 70000);

-- Rejected (Error thrown!):
INSERT INTO IT_Employees VALUES (106, 'Pooja', 'HR', 65000);
```

---

## 5. Materialized Views vs Dynamic Virtual Views

| Feature | Standard Virtual View | Materialized View (MView) |
| :--- | :--- | :--- |
| **Data Storage** | No physical data on disk (only query definition). | **Physically stored** on disk as a snapshot. |
| **Execution Cost** | Evaluated on every run (Costly for complex joins). | Instant read from disk cache (Very Fast). |
| **Freshness** | 100% Real-time current data. | May be stale until explicitly refreshed. |
| **Use Case** | OLTP transaction security & masking. | OLAP Data Warehousing, Dashboards, BI Analytics. |
