# Module 06: SQL Joins and Set Operations

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** Inner Join, Natural Join, Self Join, Outer Joins (Left, Right, Full), and Set Operations (`UNION`, `UNION ALL`, `INTERSECT`, `MINUS`)

---

## 1. SQL Join Architecture

Joins multiple tables ke columns ko unke beech common attributes (Primary Key - Foreign Key relationship) ke basis par combine karte hain:

### 1.1 INNER JOIN / EQUI JOIN
Sirf wahi rows return karta hai jahan dono tables ke join predicate match karte hon:
```sql
SELECT E.EmpID, E.Name, D.DeptName
FROM Employee E
INNER JOIN Department D ON E.DeptID = D.DeptID;
```

### 1.2 SELF JOIN (Same Table Join)
Ek table ko khud ke saath join karna. Canonical Example: Employee-Manager hierarchy:
```sql
SELECT E.Name AS Employee, M.Name AS Manager
FROM Employee E
LEFT JOIN Employee M ON E.ManagerID = M.EmpID;
```

### 1.3 OUTER JOINS (Handling Dangling / Unmatched Records)
1. **LEFT OUTER JOIN:** Left table ke saare rows aayenge. Right table se sirf matching rows aayenge; non-matching right columns mein `NULL` appear hoga.
2. **RIGHT OUTER JOIN:** Right table ke saare rows aayenge. Left non-matching columns mein `NULL` fill hoga.
3. **FULL OUTER JOIN:** Dono tables ke sabhi matching aur non-matching rows combine hokar aayenge.

---

## 2. SQL Set Operations

Set operations do queries ke **result sets (rows)** ko horizontally combine karti hain.
- **Prerequisite:** Dono queries ka **Union Compatible** hona zaroori hai (Same number of columns and compatible data types).

### 2.1 UNION vs UNION ALL (Top Interview Question)
- **`UNION`:** Do queries ke rows ko combine karta hai aur **duplicate rows ko eliminate** karta hai. Internal memory sort apply karta hai (performance overhead).
- **`UNION ALL`:** Do queries ke rows ko direct append karta hai without checking for duplicates. **Extremely fast execution**!

```sql
-- Fast concatenation when duplicate removal is not needed:
SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers;
```

### 2.2 INTERSECT
Un rows ko return karta hai jo dono queries mein common hain:
```sql
-- Students who are enrolled in BOTH CSE and Robotics Club:
SELECT RollNo FROM CSE_Students
INTERSECT
SELECT RollNo FROM Robotics_Club;
```

### 2.3 MINUS (Oracle) / EXCEPT (PostgreSQL/SQL Server)
First query ke un rows ko return karta hai jo second query mein exist nahi karte:
```sql
-- Students who submitted Assignment 1 but NOT Assignment 2:
SELECT RollNo FROM Assign1_Submissions
MINUS
SELECT RollNo FROM Assign2_Submissions;
```
