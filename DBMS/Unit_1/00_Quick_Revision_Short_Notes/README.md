# ⚡ Unit 1: Ultra High-Yield 3-Page Quick Revision Short Notes

> **Exam & Interview Rapid Recall Sheet:** Yeh short notes document Unit 1 ke sabhi 12 core subtopics aur theoretical concepts ko **sirf 3 pages** mein condense karta hai. Last-minute AKTU exam revision ya top product/service tech interview se pehle pooray unit ko blitz-speed me recall karne ke liye design kiya gaya hai.
>
> 📄 **Standalone 3-Page Verified PDF:** [Unit_1_Quick_Revision_3_Page_Notes.pdf](Unit_1_Quick_Revision_3_Page_Notes.pdf)

---

## 📑 Page 1: Introduction, 3-Schema Architecture, File System vs DBMS & Languages

### 1.1 3-Schema ANSI/SPARC Architecture & Data Independence
- **Objective:** Physical hard drive par stored binary data se application programs aur user queries ko completely decouple karna.
- **The 3 Abstraction Levels:**
  1. **External Level (View Schema):** Multiple tailored views for end users. Unrelated tables hide hote hain (e.g., Student portal hides teacher salary).
  2. **Conceptual Level (Logical Schema):** Pure database structure ka global blueprint (entities, attributes, relationships, integrity constraints). Hardware independent.
  3. **Internal Level (Physical Schema):** Data physically hard disk par kaise stored hai (B+ Trees, hashing, clustering, file pointers, block allocation).
- **Data Independence:**
  - **Logical Data Independence:** Conceptual schema modify karne par External schema & user queries untouched rehti hain. *(Very Difficult to achieve)*. Example: Adding column `DOB` to table does not break existing views.
  - **Physical Data Independence:** Internal schema (disk indexing, hashing, sorting) modify karne par Conceptual/External untouched rehti hain. *(Easily achieved)*. Example: Changing Heap file to B+ Tree.

### 1.2 Traditional File System vs Modern DBMS (10-Marker Comparison)
| Evaluation Parameter | Traditional File System (OS Files) | Database Management System (DBMS) |
| :--- | :--- | :--- |
| **Data Redundancy** | Har department duplicate files maintain karta hai; immense disk waste. | Centralized schema; normalization through minimum redundancy. |
| **Data Inconsistency** | Ek file update hui, doosri purani reh gayi $\rightarrow$ Phantom data mismatch. | Single point updates & cascade rules; 100% mutual consistency. |
| **Atomicity Guarantee** | No rollback. Mid-transfer system crash leaves money deducted & lost. | WAL (Write-Ahead Logging) & 2-Phase Commit ensure All-or-Nothing. |
| **Concurrent Access** | File-level OS lock; reader-writer stalls or race conditions (lost update). | 2PL & multi-version timestamping guarantee Serializability. |
| **Security & Abstraction** | Operating system coarse file permissions (rwx); no column masking. | Fine-grained column/row level SQL privileges (`GRANT SELECT`). |

### 1.3 Database Users & DBA Duties
- **Naive / Parametric:** Form GUI users (ATM, Railway booking, cashier).
- **Application Programmers:** DML embedded code likhne wale (Java/C++ devs).
- **Sophisticated Users:** Complex ad-hoc SQL / Analytical queries (Data Analysts).
- **Specialized Users:** Non-relational apps (GIS spatial data, AI models).
- **DBA (Database Administrator) Duties:** Schema definition, Storage structure & access path tuning, Granting authorization (DCL), Periodic backup & crash recovery.

### 1.4 DBMS Languages Taxonomy
- **DDL (Data Definition Language):** Schema structure create/alter karta hai. Auto-committed! Commands: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`.
- **DML (Data Manipulation Language):** Tuples modify/retrieve karta hai.
  - *Procedural (Low-level):* User specifies **WHAT** data and **HOW** to get it (Relational Algebra).
  - *Declarative (High-level):* User specifies only **WHAT** data is needed (SQL, Relational Calculus). Commands: `SELECT`, `INSERT`, `UPDATE`, `DELETE`.
- **DCL (Data Control Language):** Security & Permissions. Commands: `GRANT`, `REVOKE`.
- **TCL (Transaction Control Language):** Atomicity & Consistency. Commands: `COMMIT`, `ROLLBACK`, `SAVEPOINT`.

### 1.5 DBMS Tier Architectures
- **1-Tier:** User UI, Client logic, aur Database ek hi physical machine par resident (Local SQLite, MS Access).
- **2-Tier:** Client PC par UI + App logic run hoti hai; Database remote server par hota hai via ODBC/JDBC. Fat client bottleneck.
- **3-Tier:** Client (Web Browser) $\rightarrow$ Application Server (Business Logic) $\rightarrow$ Database Server (Data Storage). Scalable, secure & enterprise standard.

---

## 📑 Page 2: ER Modeling, Attributes, Cardinalities, Weak Entities, Keys & EER

### 2.1 Attributes Taxonomy & Symbols
- **Simple / Atomic:** Cannot be divided further (`Age`, `RollNo`).
- **Composite:** Hierarchy of sub-parts (`Name` $\rightarrow$ `First`, `Mid`, `Last`).
- **Single-Valued:** Single item per tuple (`Aadhar_No`, `DOB`).
- **Multivalued:** Multiple items per entity (`Phone_No`, `Skills`). Symbol: **Double Ellipse**.
- **Derived:** Computed dynamically (`Age = Current_Date - DOB`). Symbol: **Dashed Ellipse**.
- **Key Attribute:** Primary identifier. Symbol: **Underlined Text**.

### 2.2 Cardinality & Participation Constraints
- **Cardinality Ratios:**
  - **1:1 (One-to-One):** Citizen $\leftrightarrow$ Passport.
  - **1:N (One-to-Many):** Department $\rightarrow$ Employees.
  - **M:N (Many-to-Many):** Students $\leftrightarrow$ Courses.
- **Participation Constraints:**
  - **Total Participation (Double Line):** Har entity relationship me mandatory appear hoti hai (e.g., Har Employee ka Dept hona mandatory).
  - **Partial Participation (Single Line):** Kuch entities relation ke bina exist kar sakti hain (e.g., Har Professor Dean nahi hota).

### 2.3 Weak Entity Sets & Identifying Relationships
- **Definition:** Aisa entity set jiske paas apna Primary Key form karne ke liye sufficient attributes na hon. Yeh identifying **Owner Entity** par depend karta hai.
- **Symbols:**
  - Weak Entity Set: **Double Rectangle**.
  - Identifying Relationship: **Double Diamond** (Always 1:N from Owner to Weak, Total participation on Weak side).
  - Partial Key / Discriminator: **Dashed Underline**.
- **Weak Entity Primary Key:**
  $$\text{Weak Entity PK} = \text{Owner PK} + \text{Partial Key (Discriminator)}$$
- **Canonical Example:**
  - Owner: `EMPLOYEE(Emp_ID, Name, Salary)`
  - Weak: `DEPENDENT(Dep_Name, Relation, Age)` [Partial key: `Dep_Name`]
  - Resulting Composite PK: `{Emp_ID, Dep_Name}`.

### 2.4 Relational Keys Hierarchy & Mathematical Formulas
- **Super Key (SK):** Any set of attributes jo relation ke har tuple ko uniquely identify kare.
- **Candidate Key (CK):** **Minimal Super Key**. Koi bhi proper subset super key nahi hona chahiye!
- **Primary Key (PK):** Database designer dwara choose kiya gaya single candidate key. **CANNOT BE NULL!**
- **Alternate Key (AK):** Unselected candidate keys ($\text{AK} = \text{CK} - \text{PK}$).
- **Foreign Key (FK):** Attribute referencing the Primary Key of another parent relation.
- **Super Key Counting Formula:**
  - Relation $R(A_1, A_2, \dots, A_n)$ with single candidate key of size $k$:
    $$\text{Total Super Keys} = 2^{n - k}$$
  - For multiple candidate keys: Apply **Principle of Inclusion-Exclusion**:
    $$|SK(A \cup B)| = 2^{n - |A|} + 2^{n - |B|} - 2^{n - |A \cup B|}$$

### 2.5 Extended ER (EER) Modeling Features
- **Generalization:** Bottom-up approach. Multiple lower entities ki common properties extract karke superclass banana (e.g., Car & Truck $\rightarrow$ Vehicle).
- **Specialization:** Top-down approach. Superclass ko specific distinguishing attributes ke basis par subclasses me split karna (e.g., Employee $\rightarrow$ Developer, QA).
- **Aggregation:** Relationship-as-Entity abstract karna taaki ternary relationship ko binary me clean model kiya ja sake.
- **EER Constraints:**
  - **Disjointness:** Disjoint (`d`) = mutually exclusive; Overlapping (`o`) = simultaneous membership allowed.
  - **Completeness:** Total (Double line) = mandatory subclass membership; Partial (Single line) = optional subclass membership.

---

## 📑 Page 3: ER-to-Relational Mapping, Minimization, Constraints & Relational Algebra

### 3.1 The 7 ER-to-Relational Mapping Rules & Table Minimization
| ER Construct | Conversion / Mapping Rule | Min Tables | Resulting Relational Schema Structure |
| :--- | :--- | :--- | :--- |
| **Strong Entity** | Create dedicated table. Flatten composite attributes into atomic columns. | **1 Table** | `STUDENT(RollNo, FName, LName, City, Marks)` |
| **Weak Entity** | Table contains weak attributes + Owner PK as Foreign Key. Composite PK! | **1 Table** | `DEPENDENT(Emp_ID (FK), Dep_Name, Relation, Age)` |
| **1:1 (Both Total)** | Merge both entity sets and relationship into a SINGLE unified table! | **1 Table** | `CITIZEN_PASSPORT(Aadhar_No, Name, Pass_No, IssueDate)` |
| **1:1 (One Partial)** | Maintain 2 tables. Place PK of Partial entity as Foreign Key on Total side. | **2 Tables** | `EMP(Emp_ID, Name)` & `DEPT(Dept_ID, DName, Mgr_ID(FK))` |
| **1:N Relationship** | NO new table! Put Primary Key of '1' side as Foreign Key into 'N' side table. | **2 Tables** | `DEPT(Dept_ID)` & `EMP(Emp_ID, Name, Dept_ID(FK))` |
| **M:N Relationship** | Create separate Join Table! PK = Composite union of both participating PKs. | **3 Tables** | `STU(Roll)`, `CRS(CID)`, `ENROLL(Roll(FK), CID(FK), Grade)` |
| **Multivalued Attr** | Create separate table. PK = (Entity PK + Multivalued Attribute). | **+1 Table** | `STUDENT_PHONE(RollNo(FK), Phone_Number)` |

### 3.2 Relational Data Model & The 4 Integrity Constraints
1. **Domain Constraint:** Har attribute value uske defined valid atomic set me hona chahiye (`Age > 0`, `Marks` $\in [0, 100]$).
2. **Key Constraint:** Relation ke koi bhi do distinct tuples identical Primary/Candidate Key share nahi kar sakte.
3. **Entity Integrity:** Primary Key attribute value **KABHI BHI NULL NAHI** ho sakti!
4. **Referential Integrity:** Foreign Key value ya to parent relation ke existing valid Primary Key se match karegi, ya fir **NULL** hogi. Violated on Delete/Update $\rightarrow$ Actions: `CASCADE`, `SET NULL`, `RESTRICT`.

### 3.3 Relational Algebra Operations Master Summary
| Operation | Symbol | Type | Behavior & Key Property | Example Syntax |
| :--- | :--- | :--- | :--- | :--- |
| **Selection** | $\sigma_p(R)$ | Horizontal | Rows filter karta hai based on predicate condition $p$. Degree same, Cardinality $\le |R|$. | $\sigma_{\text{Salary} > 50000}(\text{EMPLOYEE})$ |
| **Projection** | $\pi_A(R)$ | Vertical | Columns filter karta hai. **Automatically removes duplicate rows!** Degree = $|A|$. | $\pi_{\text{Name, Salary}}(\text{EMPLOYEE})$ |
| **Cartesian Product** | $R \times S$ | Cross | Combines all tuples. Degree = $\text{deg}(R)+\text{deg}(S)$; Cardinality = $|R| \times |S|$. | $\text{STUDENT} \times \text{COURSE}$ |
| **Natural Join** | $R \bowtie S$ | Join | Common attribute names par Cartesian product followed by equality selection and projection. | $\text{EMP} \bowtie \text{DEPT}$ |
| **Outer Joins** | Left ($\ltimes$), Right ($\rtimes$), Full ($\bowtie$) | Preserve | Unmatched dangling tuples ko retain karte hain padded with NULLs. | $\text{EMP} \LeftThreetimes \text{DEPT}$ |
| **Division Operator** | $R \div S$ | Universal | Solves "**FOR ALL / EVERY**" queries. (Find students who took ALL math courses). | $\pi_{\text{Roll, CID}}(\text{ENROLL}) \div \pi_{\text{CID}}(\text{MATH\_CRS})$ |

### 3.4 Relational Calculus & Codd's Theorem
- **Tuple Relational Calculus (TRC):** Non-procedural. Focuses on filtering tuples: $\{ t \mid P(t) \}$.
- **Domain Relational Calculus (DRC):** Focuses on filtering individual attribute domain variables: $\{ \langle x_1, x_2, \dots, x_n \rangle \mid P(x_1, x_2, \dots, x_n) \}$.
- **Codd's Theorem (Relational Completeness):**
  $$\text{Relational Algebra} \equiv \text{Safe TRC} \equiv \text{Safe DRC}$$
  A query language is **Relationally Complete** if it can express any query expressible in basic Relational Algebra. SQL is built upon this exact formal foundation!
