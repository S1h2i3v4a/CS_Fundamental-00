# Module 10: Advanced SQL — PL/SQL Cursors

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Topic Focus:** PL/SQL Memory Context Area, Implicit Cursors (`SQL%` Attributes), Explicit Cursor 4-Step Lifecycle (`DECLARE`, `OPEN`, `FETCH`, `CLOSE`), and Cursor FOR Loops

---

## 1. What is a Cursor in DBMS?

Jab SQL query execute hoti hai, toh database engine uske result set ko memory mein hold karne ke liye ek private work area allocate karta hai jise **Context Area** kaha jata hai.
- **Cursor** us context area par ek pointer hota hai jiske through application program result set ke rows ko row-by-row sequentially process kar sakta hai.

```
                  [ Private Memory Context Area ]
                     ┌────────────────────────┐
   Cursor Pointer ──>│ Row 1: 101 | Aman     │
                     ├────────────────────────┤
                     │ Row 2: 102 | Rohan    │
                     ├────────────────────────┤
                     │ Row 3: 103 | Neha     │
                     └────────────────────────┘
```

---

## 2. Implicit Cursors

Implicit cursors Oracle/DBMS engine dwara **automatically** open aur manage kiye jaate hain jab bhi koi SQL statement (`SELECT INTO`, `INSERT`, `UPDATE`, `DELETE`) execute hota hai.

### The 4 Implicit Cursor Attributes:
| Attribute | Return Type | Meaning |
| :--- | :--- | :--- |
| `SQL%FOUND` | Boolean | `TRUE` agar recently executed DML ne kam se kam 1 row affect kiya ho. |
| `SQL%NOTFOUND` | Boolean | `TRUE` agar recently executed DML ne zero rows affect kiye hon. |
| `SQL%ROWCOUNT` | Integer | Total number of rows affected by the statement. |
| `SQL%ISOPEN` | Boolean | Always evaluates to `FALSE` (DBMS auto-closes cursor after completion). |

```sql
BEGIN
    UPDATE Employee SET Salary = Salary + 5000 WHERE Dept = 'HR';
    IF SQL%FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Updated ' || SQL%ROWCOUNT || ' employees.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('No HR employees found.');
    END IF;
END;
```

---

## 3. Explicit Cursors (The 4 Lifecycle Steps)

Jab query **multiple rows return** karti hai aur programmer ko row-by-row processing par complete control chahiye hota hai, tab **Explicit Cursor** use kiya jata hai:

```
  [ 1. DECLARE ] ──> [ 2. OPEN ] ──> [ 3. FETCH ] ──> [ 4. CLOSE ]
   Define Query      Execute &        Load Row into     Free Memory
                     Active Set       Variables
```

### 3.1 Step-by-Step PL/SQL Implementation:
```sql
DECLARE
    -- Step 1: Declare the cursor
    CURSOR c_emp IS
        SELECT EmpID, Name, Salary FROM Employee WHERE Dept = 'IT';
    
    v_id   Employee.EmpID%TYPE;
    v_name Employee.Name%TYPE;
    v_sal  Employee.Salary%TYPE;
BEGIN
    -- Step 2: Open cursor (Query executes, active set populated)
    OPEN c_emp;
    
    LOOP
        -- Step 3: Fetch current row into variables
        FETCH c_emp INTO v_id, v_name, v_sal;
        EXIT WHEN c_emp%NOTFOUND; -- Terminate when all rows processed
        
        DBMS_OUTPUT.PUT_LINE('ID: ' || v_id || ', Name: ' || v_name || ', Salary: ' || v_sal);
    END LOOP;
    
    -- Step 4: Close cursor (Free memory)
    CLOSE c_emp;
END;
```

### 3.2 Simplified Cursor FOR Loop:
Cursor FOR loop automatically cursor ko OPEN karta hai, rows FETCH karta hai, aur loop end hone par CLOSE kar deta hai (zero memory leak risk):
```sql
BEGIN
    FOR emp_rec IN (SELECT EmpID, Name, Salary FROM Employee WHERE Dept = 'IT') LOOP
        DBMS_OUTPUT.PUT_LINE(emp_rec.Name || ' earns ' || emp_rec.Salary);
    END LOOP;
END;
```
