# Module 12: Unit 2 AKTU PYQs and Solved Query Bank

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** Past 5-Year AKTU Exam Questions, Dual Relational Algebra & SQL Query Solutions, Suppliers-Parts System, Library Management System & Viva Q&A

---

## 1. Past 5-Year Question Trend Analysis

AKTU examination mein Unit 2 se har saal 2 se 3 questions puche jaate hain (Total 17 to 24 marks):
1. **Numerical on Relational Algebra (AKTU 2020-21, 2021-22, 2022-23, 2023-24):** 10 Marks.
2. **Explain Relational Algebra Operations in Detail (AKTU 2015-16, 2017-18, 2018-19):** 10 Marks.
3. **Difference between WHERE and HAVING / TRUNCATE vs DROP vs DELETE:** 2 to 7 Marks.
4. **Triggers / Views / Cursors with Syntax and Example:** 7 to 10 Marks.

---

## 2. Master Problem 1: Suppliers-Parts Database (AKTU 10-Marker)

Given Schema:
- `Suppliers(sid, sname, address)` — PK: `sid`
- `Parts(pid, pname, color)` — PK: `pid`
- `Catalog(sid, pid, cost)` — PK: `(sid, pid)`

---

### Query 1: Find the names of suppliers who supply some RED part.
- **Relational Algebra:**
  $$\pi_{\text{sname}}\Big( \text{Suppliers} \bowtie \pi_{\text{sid}}\big(\text{Catalog} \bowtie \sigma_{\text{color} = \text{'RED'}}(\text{Parts})\big) \Big)$$
- **SQL:**
  ```sql
  SELECT DISTINCT S.sname
  FROM Suppliers S
  JOIN Catalog C ON S.sid = C.sid
  JOIN Parts P ON C.pid = P.pid
  WHERE P.color = 'RED';
  ```

---

### Query 2: Find the sids of suppliers who supply EVERY part.
- **Relational Algebra (Division Operator):**
  $$\pi_{\text{sid}, \text{pid}}(\text{Catalog}) \div \pi_{\text{pid}}(\text{Parts})$$
- **SQL (GROUP BY & HAVING COUNT):**
  ```sql
  SELECT sid
  FROM Catalog
  GROUP BY sid
  HAVING COUNT(DISTINCT pid) = (SELECT COUNT(*) FROM Parts);
  ```

---

### Query 3: Find suppliers who supply NO RED parts.
- **Relational Algebra (Set Difference):**
  $$\pi_{\text{sid}}(\text{Suppliers}) - \pi_{\text{sid}}\big(\text{Catalog} \bowtie \sigma_{\text{color} = \text{'RED'}}(\text{Parts})\big)$$
- **SQL (NOT IN Subquery):**
  ```sql
  SELECT sname
  FROM Suppliers
  WHERE sid NOT IN (
      SELECT C.sid
      FROM Catalog C
      JOIN Parts P ON C.pid = P.pid
      WHERE P.color = 'RED'
  );
  ```

---

## 3. Master Problem 2: Library Management System

Given Schema:
- `Student(RollNo, Name, Branch)`
- `Book(ISBN, Title, Author, Publisher)`
- `Issue(RollNo, ISBN, IssueDate)`

### Query 1: Find names of students who have borrowed books authored by 'Korth'.
- **SQL:**
  ```sql
  SELECT DISTINCT S.Name
  FROM Student S
  JOIN Issue I ON S.RollNo = I.RollNo
  JOIN Book B ON I.ISBN = B.ISBN
  WHERE B.Author = 'Korth';
  ```

### Query 2: Find books that have NEVER been issued to any student.
- **SQL:**
  ```sql
  SELECT Title, ISBN
  FROM Book
  WHERE ISBN NOT IN (SELECT DISTINCT ISBN FROM Issue);
  ```

---

## 4. Top Viva & Technical Interview Questions

1. **Q: Why does Relational Algebra's Projection ($\pi$) drop duplicates automatically while SQL's SELECT does not?**  
   *Ans:* Relational algebra mathematically sets par operate karti hai (sets by definition contain unique elements). SQL real-world performance ke liye multisets (bags) par operate karti hai taaki har query execution par heavy sorting/hashing overhead na ho. User ko explicit `DISTINCT` keyword dena padta hai.

2. **Q: Can a Correlated Subquery be converted into a JOIN?**  
   *Ans:* Yes! Almost all correlated subqueries (especially with `EXISTS` or equality joins) can be rewritten as `INNER JOIN` with distinct projection, which allows the DBMS query optimizer to choose hash joins or merge joins for $O(N)$ efficiency.
