# ⚡ Unit 2: Ultra High-Yield 3-Page Quick Revision Short Notes

> **Exam & Interview Rapid Recall Sheet:** Yeh short notes document Unit 2 ke sabhi Relational Algebra operators, Relational Calculus, SQL DDL/DML, Constraints, Execution Pipeline, Joins, Views, Indexes, Cursors, aur Triggers ko **sirf 3 pages** mein condense karta hai.
>
> 📄 **Standalone 3-Page Verified PDF:** [Unit_2_Quick_Revision_3_Page_Notes.pdf](Unit_2_Quick_Revision_3_Page_Notes.pdf)

---

## 📑 Page 1: Relational Algebra, Relational Calculus, SQL Foundations & DDL

### 1.1 Relational Algebra (5 Fundamental Operators)
- **Selection ($\sigma_p(R)$):** Rows filter karta hai condition $p$ ke basis par. Degree unaltered, Cardinality $\le |R|$.
- **Projection ($\pi_A(R)$):** Columns filter karta hai. **Automatically eliminates duplicate rows!** Degree = $|A|$.
- **Union ($R \cup S$):** Combines rows. Requires **Union Compatibility** (same degree & compatible attribute domains).
- **Set Difference ($R - S$):** Rows in $R$ but absent in $S$. Non-commutative ($R - S \ne S - R$).
- **Cartesian Product ($R \times S$):** Pairs every tuple. Degree = $m + n$, Cardinality = $m \times n$.
- **Rename ($\rho$):** Renames relation or attributes to avoid ambiguity in self-joins.

### 1.2 Derived Joins & Division Operator
- **Theta Join ($R \bowtie_\theta S$):** $\sigma_\theta(R \times S)$. Equi-join strictly uses equality ($=$).
- **Natural Join ($R \bowtie S$):** Equi-join on common attribute names + duplicate columns removed automatically.
- **Outer Joins:** Preserves dangling unmatched rows with NULL padding:
  - Left Outer ($R \LeftThreetimes S$), Right Outer ($R \RightThreetimes S$), Full Outer ($R \fullouterjoin S$).
- **Division Operator ($R \div S$):** Solves "**FOR ALL / EVERY**" queries:
  $$R(A, B) \div S(B) = \pi_A(R) - \pi_A((\pi_A(R) \times S) - R)$$

### 1.3 Relational Calculus (TRC vs DRC) & Codd's Theorem
- **Tuple Relational Calculus (TRC):** $\{ t \mid P(t) \}$. Tuple variable $t$ represents an entire row. Uses $\exists$ and $\forall$.
- **Domain Relational Calculus (DRC):** $\{ \langle x_1..x_n \rangle \mid P \}$. Variables represent column attribute domains.
- **Safe Queries:** Unsafe expressions like $\{ t \mid \neg(t \in R) \}$ return infinite universes. A calculus expression is Safe if all resulting values are bounded within the active domain.
- **Codd's Theorem:** $\text{Relational Algebra} \equiv \text{Safe TRC} \equiv \text{Safe DRC}$.

### 1.4 SQL Foundations, Data Types & Command Families
- **Data Types:** `CHAR(n)` (fixed-length), `VARCHAR(n)` (variable-length), `INT`, `DECIMAL(p, s)` (exact numeric), `DATE`, `TIMESTAMP`, `BLOB`, `CLOB`.
- **4 Command Families:**
  - **DDL:** `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME` (Auto-committed!).
  - **DML:** `SELECT`, `INSERT`, `UPDATE`, `DELETE` (Requires commit).
  - **DCL:** `GRANT`, `REVOKE`.
  - **TCL:** `COMMIT`, `ROLLBACK`, `SAVEPOINT`.

### 1.5 DROP vs TRUNCATE vs DELETE Comparison Matrix
| Parameter | `DROP TABLE` | `TRUNCATE TABLE` | `DELETE FROM` |
| :--- | :--- | :--- | :--- |
| **Category** | DDL | DDL | DML |
| **Schema State** | Destroyed completely | Preserved | Preserved |
| **WHERE Clause** | No | No (all rows purged) | Yes (`WHERE id = 5`) |
| **Rollback** | No (Auto-commit) | No (Auto-commit) | Yes (Logged in undo) |
| **Speed** | Instant | Lightning Fast (Resets HWM) | Slower (Row logging) |
| **Triggers** | DROP trigger | No DELETE triggers fired | Fires row DELETE triggers |

---

## 📑 Page 2: DML, Integrity Constraints, Aggregate Functions & Execution Pipeline

### 2.1 DML Operations
- `INSERT INTO`: Single or bulk tuple insertion.
- `UPDATE`: Modifies candidate rows. Precaution: Missing `WHERE` clause updates all rows in table!
- `DELETE FROM`: Purges candidate rows with undo logging.
- `SELECT`: Declarative data extraction expression.

### 2.2 SQL Integrity Constraints & Cascade Actions
- **Constraints:** `NOT NULL`, `UNIQUE`, `PRIMARY KEY` (NOT NULL + UNIQUE), `FOREIGN KEY`, `CHECK`, `DEFAULT`.
- **Referential Integrity Actions (`ON DELETE` / `ON UPDATE`):**
  1. `CASCADE`: Changes automatically propagate to child rows.
  2. `SET NULL`: Sets child foreign key to `NULL`.
  3. `SET DEFAULT`: Sets child foreign key to its default fallback value.
  4. `RESTRICT / NO ACTION`: Rejects parent deletion with an error if child rows exist (Default).

### 2.3 Physical Engine Execution Pipeline
$$\text{FROM / JOIN} \rightarrow \text{WHERE} \rightarrow \text{GROUP BY} \rightarrow \text{HAVING} \rightarrow \text{SELECT} \rightarrow \text{DISTINCT} \rightarrow \text{ORDER BY} \rightarrow \text{LIMIT}$$
- **Key Takeaway:** `WHERE` executes before `SELECT` (no column aliases allowed in `WHERE`). `ORDER BY` executes after `SELECT` (aliases allowed).

### 2.4 Aggregate Functions & GROUP BY
- Functions: `COUNT(*)`, `COUNT(col)`, `SUM`, `AVG`, `MIN`, `MAX`.
- All aggregates ignore `NULL` values (except `COUNT(*)`).
- **GROUP BY Rule:** All non-aggregated columns in the `SELECT` list must appear in the `GROUP BY` clause!

### 2.5 WHERE vs HAVING Comparison
| Parameter | `WHERE` Clause | `HAVING` Clause |
| :--- | :--- | :--- |
| **Scope** | Operates on individual rows. | Operates on grouped summary buckets. |
| **Timing** | Executes BEFORE `GROUP BY`. | Executes AFTER `GROUP BY` aggregation. |
| **Aggregates** | Strictly Forbidden (`WHERE AVG(s) > 50k` is ERROR). | Designed for aggregates (`HAVING AVG(s) > 50k`). |

---

## 📑 Page 3: Joins, Subqueries, Views, Indexes, Cursors & Triggers

### 3.1 SQL Joins & Set Operations
- `INNER JOIN`: Only matching records.
- `SELF JOIN`: Joins table with itself (Employee-Manager hierarchy).
- `OUTER JOINS`: Retains unmatched dangling rows with `NULL` (LEFT, RIGHT, FULL).
- `UNION` (deduplicates, slow sort) vs `UNION ALL` (fast concatenation).
- `INTERSECT` (common rows) and `MINUS` (subtraction).

### 3.2 Nested & Correlated Subqueries
- **Multi-Row:** `IN`, `> ANY` (`> MIN`), `> ALL` (`> MAX`).
- **Correlated Subquery:** Inner query references outer row attributes; executes row-by-row ($O(N \times M)$ nested loop).
- **`EXISTS` vs `NOT EXISTS`:** Boolean short-circuit evaluation! Stops immediately upon finding first match. Faster than `IN` on large indexed tables.

### 3.3 SQL Views & Security Abstraction
- **View:** Virtual table defined by a SQL query; no physical data rows stored on disk.
- **Updatable View Criteria:** Derived from single base table, contains Primary Key, NO aggregate functions, NO `GROUP BY`, `HAVING`, or `DISTINCT`.
- **`WITH CHECK OPTION`:** Prevents inserts/updates that violate the view's `WHERE` filter.
- **Materialized View:** Physically stored snapshot on disk for high-speed OLAP aggregations.

### 3.4 Database Indexes (B-Tree)
- **Clustered Index:** Data physically sorted on disk in index order. Leaf nodes contain actual rows. **Only 1 per table** (Auto on PK).
- **Non-Clustered:** Separate B-Tree. Leaf nodes contain Key + Row Pointer. Multiple allowed.
- **Dense Index:** Index entry for EVERY row.
- **Sparse Index:** 1 entry per disk block (Strictly requires sorted data file!).

### 3.5 PL/SQL Cursors
- **Implicit Cursors:** Auto-managed by DBMS for all DML. Attributes: `SQL%FOUND`, `SQL%NOTFOUND`, `SQL%ROWCOUNT`, `SQL%ISOPEN`.
- **Explicit Cursors (4 Lifecycle Steps):** `DECLARE` $\rightarrow$ `OPEN` $\rightarrow$ `FETCH` $\rightarrow$ `CLOSE`.
- **Cursor FOR Loop:** Automatically handles open, fetch, and close cycles.

### 3.6 Database Triggers (ECA Model)
- **Event:** `INSERT`, `UPDATE`, `DELETE` on table.
- **Timing:** `BEFORE` (data validation/security) vs `AFTER` (auditing/logging).
- **Granularity:** `FOR EACH ROW` (row-level with `:NEW` and `:OLD`) vs Statement-level.
- **Salary Reduction Prevention Trigger:**
  ```sql
  CREATE OR REPLACE TRIGGER prevent_salary_decrease
  BEFORE UPDATE OF Salary ON Employee FOR EACH ROW
  BEGIN
      IF :NEW.Salary < :OLD.Salary THEN
          RAISE_APPLICATION_ERROR(-20001, 'Salary reduction forbidden!');
      END IF;
  END;
  ```
