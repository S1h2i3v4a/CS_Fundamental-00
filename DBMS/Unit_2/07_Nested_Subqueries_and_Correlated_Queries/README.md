# Module 07: Nested Subqueries and Correlated Queries

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** Subquery Types, Scalar vs Multi-Row Operators (`IN`, `ANY`, `ALL`), Correlated Subqueries Execution, and `EXISTS` vs `NOT EXISTS`

---

## 1. What is a Subquery?

Subquery (Nested Query) ek aisi SQL query hoti hai jo kisi doosri main SQL query ke andar enclosed (parenthesized) hoti hai.
- Outer query ko **Main Query** kaha jata hai.
- Inner query ko **Subquery** kaha jata hai.

---

## 2. Independent Nested Subqueries

Independent subquery outer query par depend **nahi** karti. Yeh pehle ek baar execute hoti hai, output generate karti hai, aur wo output outer query ko pass kar diya jata hai.

### 2.1 Scalar Subquery (Single Value)
```sql
-- Find employees who earn more than the company average salary:
SELECT Name, Salary
FROM Employee
WHERE Salary > (SELECT AVG(Salary) FROM Employee);
```

### 2.2 Multi-Row Subqueries (`IN`, `ANY`, `ALL`)
1. **`IN` Operator:**
   ```sql
   -- Find employees working in departments located in 'Noida':
   SELECT Name FROM Employee
   WHERE DeptID IN (SELECT DeptID FROM Department WHERE City = 'Noida');
   ```
2. **`> ANY` (Equivalent to `> MIN`):**
   ```sql
   -- Earning more than AT LEAST ONE person in Sales:
   SELECT Name FROM Employee
   WHERE Salary > ANY (SELECT Salary FROM Employee WHERE Dept = 'Sales');
   ```
3. **`> ALL` (Equivalent to `> MAX`):**
   ```sql
   -- Earning more than EVERY SINGLE person in Sales:
   SELECT Name FROM Employee
   WHERE Salary > ALL (SELECT Salary FROM Employee WHERE Dept = 'Sales');
   ```

---

## 3. Correlated Subqueries (Nested Loops)

Correlated subquery mein inner query **outer table ke attributes ko refer** karti hai.
- Iska execution independent nahi hota: Outer query ke **har ek individual row ke liye inner subquery baar-baar re-evaluate** hoti hai!
- **Time Complexity:** $O(N \times M)$ (Nested Loop).

```sql
-- Find employees earning more than the average salary of THEIR OWN department:
SELECT E1.Name, E1.DeptID, E1.Salary
FROM Employee E1
WHERE E1.Salary > (
    SELECT AVG(E2.Salary)
    FROM Employee E2
    WHERE E2.DeptID = E1.DeptID -- Correlation link!
);
```

---

## 4. `EXISTS` vs `NOT EXISTS`

`EXISTS` operator verify karta hai ki subquery kam se kam ek row return karti hai ya nahi:
- **Boolean Short-Circuit:** Jaise hi subquery ko pehla matching record milta hai, evaluation turant TRUE mark karke stop ho jata hai (data disk se read nahi karta).

```sql
-- Find customers who have placed at least one order:
SELECT CustName
FROM Customers C
WHERE EXISTS (
    SELECT 1
    FROM Orders O
    WHERE O.CustomerID = C.CustomerID
);
```

### `IN` vs `EXISTS` Performance Rule:
- Agar inner table chhota hai: `IN` faster hota hai.
- Agar inner table bohot bada hai (millions of rows): `EXISTS` significantly faster hota hai kyunki wo indexed search aur early termination use karta hai.
