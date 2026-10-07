# Module 05: SQL Clauses, Aggregate Functions, and Groupings

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** SQL Clauses Execution Pipeline, Aggregate Functions (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`), `GROUP BY`, `HAVING`, and the classic WHERE vs HAVING comparison

---

## 1. SQL Execution Pipeline (Written vs Physical Order)

SQL query likhne ka sequence aur database query engine ke execute karne ka internal sequence fundamentally different hota hai:

```
[ Written SQL Query Sequence ]:
SELECT -> FROM -> WHERE -> GROUP BY -> HAVING -> ORDER BY -> LIMIT

[ Physical Engine Execution Pipeline ]:
1. FROM & JOIN     (Tables identify karna aur Cartesian/Join form karna)
2. WHERE           (Individual rows filter karna BEFORE grouping)
3. GROUP BY        (Remaining rows ko summary buckets me partition karna)
4. HAVING          (Summary groups ko filter karna AFTER aggregation)
5. SELECT          (Output columns, expressions, aur aliases compute karna)
6. DISTINCT        (Duplicate output rows remove karna)
7. ORDER BY        (Final result set ko sort karna)
8. LIMIT / OFFSET  (Top-N rows extract karna)
```

> [!NOTE]
> Kyunki `WHERE` clause `SELECT` se pehle execute hota hai, isliye aap `WHERE` clause mein `SELECT` mein define kiye gaye **column alias** ko use **nahi** kar sakte! Par `ORDER BY` clause `SELECT` ke baad execute hota hai, isliye wahan alias bilkul valid hai.

---

## 2. SQL Aggregate Functions

Aggregate functions multiple row values ko input leti hain aur **single summary value** calculate karke return karti hain:

1. **`COUNT(*)` vs `COUNT(column)`:**
   - `COUNT(*)`: Table ke total rows count karta hai (including NULL rows).
   - `COUNT(column)`: Sirf us column ke **non-NULL** values ko count karta hai.
2. **`SUM(column)`:** Sabhi non-NULL numeric values ka total return karta hai.
3. **`AVG(column)`:** Arithmetic mean calculate karta hai: $\frac{\sum \text{values}}{\text{non-NULL count}}$. (NULL values denominator mein include nahi hotin!).
4. **`MIN(column)` & `MAX(column)`:** Smallest aur largest value return karta hai (numeric, string ya date types par applicable).

---

## 3. `GROUP BY` Clause Rules

`GROUP BY` identical values wale rows ko summary rows mein collapse karta hai:
- **Golden Projection Rule:** Agar query mein `GROUP BY` use ho raha hai, toh `SELECT` clause mein sirf wahi columns direct appear ho sakte hain jo `GROUP BY` list mein hain, ya fir un par koi aggregate function (`SUM`, `AVG`, `COUNT`) laga hona chahiye!

```sql
-- Valid Query:
SELECT Dept, JobTitle, AVG(Salary), COUNT(*)
FROM Employee
GROUP BY Dept, JobTitle;
```

---

## 4. `WHERE` vs `HAVING` (AKTU 10-Marker Comparison)

| Parameter | `WHERE` Clause | `HAVING` Clause |
| :--- | :--- | :--- |
| **Operation Level** | Operates on **individual rows (tuples)**. | Operates on **grouped summary buckets**. |
| **Execution Timing** | Executes **BEFORE** `GROUP BY` clustering. | Executes **AFTER** `GROUP BY` aggregation. |
| **Aggregate Functions** | **Cannot contain aggregate functions** (`WHERE SUM(sal) > 5000` is SYNTAX ERROR). | **Designed for aggregate functions** (`HAVING AVG(sal) > 60000`). |
| **Usage Without GROUP BY** | Natively supported on any table query. | Can be used without `GROUP BY`, applies aggregate to entire table. |
| **Performance Impact** | Reduces number of rows before grouping (Faster). | Filters groups after memory-heavy aggregation. |

### Complete Real-World Example:
```sql
SELECT Dept, AVG(Salary) AS AvgSalary, COUNT(*) AS HeadCount
FROM Employee
WHERE Status = 'Active'               -- 1. Row filter
GROUP BY Dept                         -- 2. Grouping
HAVING COUNT(*) >= 5 AND AVG(Salary) > 50000 -- 3. Group filter
ORDER BY AvgSalary DESC;              -- 4. Sorting
```
