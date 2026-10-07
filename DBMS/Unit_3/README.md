# Unit 3: Relational Database Design & Normalization

> **Course:** Database Management Systems (AKTU Code: **BCS501**)  
> **Source Material:** Gateway Classes B.Tech 3rd Year Lecture Series & AKTU Previous 5-Year Examinations  
> **Core Focus:** Functional Dependencies, Armstrong's Axioms, Attribute Closure, Minimal Canonical Cover, Database Anomalies, Normal Forms (1NF, 2NF, 3NF, BCNF, 4NF, 5NF), Decomposition Properties (Lossless Join, Dependency Preservation), and Step-by-Step Solved Numericals.

---

## 📚 Central Master Documents & Downloads

- ⚡ **[Unit 3 Ultra Quick Revision Short Notes (Exact 3-Page Cheat Sheet)](Unit_3_Quick_Revision_3_Page_Notes.pdf)**
- 📖 **[Unit 3 Complete Master Consolidated Notes (All 13 Modules Merged with Bookmarks)](Unit_3_Master_Notes.pdf)**

---

## 🗂️ Sequential Module Directory

| Module # | Module Title & Focus Topic | Vector Architecture Diagram | Formats |
| :---: | :--- | :---: | :---: |
| **00** | **[Quick Revision Short Notes](00_Quick_Revision_Short_Notes/)**<br>Strict 3-page high-yield formula &amp; decision tree summary | N/A | [HTML](00_Quick_Revision_Short_Notes/00_Quick_Revision_Short_Notes.html) \| [PDF](00_Quick_Revision_Short_Notes/00_Quick_Revision_Short_Notes.pdf) |
| **01** | **[Functional Dependencies &amp; Types](01_Functional_Dependencies_and_Types/)**<br>Formal definition, Determinant vs Dependent, Trivial, Non-Trivial, Full vs Partial FDs | [SVG](01_Functional_Dependencies_and_Types/diagrams/functional_dependencies_taxonomy.svg) | [HTML](01_Functional_Dependencies_and_Types/01_Functional_Dependencies_and_Types.html) \| [PDF](01_Functional_Dependencies_and_Types/01_Functional_Dependencies_and_Types.pdf) |
| **02** | **[Armstrong's Axioms &amp; Inference Rules](02_Armstrongs_Axioms_and_Inference_Rules/)**<br>Primary Axioms (Reflexivity, Augmentation, Transitivity), Derived rules, Soundness &amp; Completeness | [SVG](02_Armstrongs_Axioms_and_Inference_Rules/diagrams/armstrong_axioms_inference_tree.svg) | [HTML](02_Armstrongs_Axioms_and_Inference_Rules/02_Armstrongs_Axioms_and_Inference_Rules.html) \| [PDF](02_Armstrongs_Axioms_and_Inference_Rules/02_Armstrongs_Axioms_and_Inference_Rules.pdf) |
| **03** | **[Attribute Closure &amp; Candidate Keys](03_Attribute_Closure_and_Candidate_Key_Algorithms/)**<br>Polynomial closure algorithm X⁺, 3-category partition method, Prime vs Non-Prime attributes | [SVG](03_Attribute_Closure_and_Candidate_Key_Algorithms/diagrams/attribute_closure_and_candidate_key_pipeline.svg) | [HTML](03_Attribute_Closure_and_Candidate_Key_Algorithms/03_Attribute_Closure_and_Candidate_Key_Algorithms.html) \| [PDF](03_Attribute_Closure_and_Candidate_Key_Algorithms/03_Attribute_Closure_and_Candidate_Key_Algorithms.pdf) |
| **04** | **[Equivalence &amp; Canonical Minimal Cover](04_Equivalence_and_Canonical_Minimal_Cover/)**<br>Testing F ≡ G, 3-phase canonical cover (Fc), Extraneous LHS removal, Redundant FD elimination | [SVG](04_Equivalence_and_Canonical_Minimal_Cover/diagrams/canonical_minimal_cover_pipeline.svg) | [HTML](04_Equivalence_and_Canonical_Minimal_Cover/04_Equivalence_and_Canonical_Minimal_Cover.html) \| [PDF](04_Equivalence_and_Canonical_Minimal_Cover/04_Equivalence_and_Canonical_Minimal_Cover.pdf) |
| **05** | **[Database Anomalies &amp; 1NF](05_Database_Anomalies_and_1NF/)**<br>Data redundancy, Insertion Anomaly, Deletion Anomaly, Update Anomaly, Atomic domain rules | [SVG](05_Database_Anomalies_and_1NF/diagrams/database_anomalies_and_1nf_pipeline.svg) | [HTML](05_Database_Anomalies_and_1NF/05_Database_Anomalies_and_1NF.html) \| [PDF](05_Database_Anomalies_and_1NF/05_Database_Anomalies_and_1NF.pdf) |
| **06** | **[Second Normal Form (2NF)](06_Second_Normal_Form_2NF/)**<br>No Partial Dependency, Full FD requirement, Simple Candidate Key Theorem, 2NF decomposition | [SVG](06_Second_Normal_Form_2NF/diagrams/second_normal_form_2nf_architecture.svg) | [HTML](06_Second_Normal_Form_2NF/06_Second_Normal_Form_2NF.html) \| [PDF](06_Second_Normal_Form_2NF/06_Second_Normal_Form_2NF.pdf) |
| **07** | **[Third Normal Form (3NF)](07_Third_Normal_Form_3NF/)**<br>Removal of Transitive Dependency, Universal 3NF Test (X is Super Key OR Y is Prime), Bernstein 3NF Synthesis | [SVG](07_Third_Normal_Form_3NF/diagrams/third_normal_form_3nf_architecture.svg) | [HTML](07_Third_Normal_Form_3NF/07_Third_Normal_Form_3NF.html) \| [PDF](07_Third_Normal_Form_3NF/07_Third_Normal_Form_3NF.pdf) |
| **08** | **[Boyce-Codd Normal Form (BCNF)](08_Boyce_Codd_Normal_Form_BCNF/)**<br>Strict Super Key requirement, Overlapping Candidate Keys anomaly, 3NF vs BCNF Trade-Off | [SVG](08_Boyce_Codd_Normal_Form_BCNF/diagrams/bcnf_vs_3nf_comparison.svg) | [HTML](08_Boyce_Codd_Normal_Form_BCNF/08_Boyce_Codd_Normal_Form_BCNF.html) \| [PDF](08_Boyce_Codd_Normal_Form_BCNF/08_Boyce_Codd_Normal_Form_BCNF.pdf) |
| **09** | **[Decomposition Properties](09_Decomposition_Properties_Lossless_and_Dependency_Preservation/)**<br>Lossless (Non-Additive) Join Theorem, Spurious Tuples Hazard, Dependency Preservation verification | [SVG](09_Decomposition_Properties_Lossless_and_Dependency_Preservation/diagrams/lossless_join_and_dependency_preservation.svg) | [HTML](09_Decomposition_Properties_Lossless_and_Dependency_Preservation/09_Decomposition_Properties_Lossless_and_Dependency_Preservation.html) \| [PDF](09_Decomposition_Properties_Lossless_and_Dependency_Preservation/09_Decomposition_Properties_Lossless_and_Dependency_Preservation.pdf) |
| **10** | **[Multivalued Dependencies &amp; 4NF](10_Multivalued_Dependencies_and_Fourth_Normal_Form_4NF/)**<br>Independent multi-valued facts X ↠ Y, Cartesian product explosion, Fagin's Theorem &amp; 4NF split | [SVG](10_Multivalued_Dependencies_and_Fourth_Normal_Form_4NF/diagrams/multivalued_dependencies_and_4nf_pipeline.svg) | [HTML](10_Multivalued_Dependencies_and_Fourth_Normal_Form_4NF/10_Multivalued_Dependencies_and_Fourth_Normal_Form_4NF.html) \| [PDF](10_Multivalued_Dependencies_and_Fourth_Normal_Form_4NF/10_Multivalued_Dependencies_and_Fourth_Normal_Form_4NF.pdf) |
| **11** | **[Join Dependencies (5NF) &amp; IND](11_Join_Dependencies_5NF_and_Inclusion_Dependencies/)**<br>Project-Join Normal Form (PJNF), N-way lossless join ⋈[R1..Rn], Inclusion Dependencies &amp; Foreign Keys | [SVG](11_Join_Dependencies_5NF_and_Inclusion_Dependencies/diagrams/join_dependencies_5nf_and_inclusion_rules.svg) | [HTML](11_Join_Dependencies_5NF_and_Inclusion_Dependencies/11_Join_Dependencies_5NF_and_Inclusion_Dependencies.html) \| [PDF](11_Join_Dependencies_5NF_and_Inclusion_Dependencies/11_Join_Dependencies_5NF_and_Inclusion_Dependencies.pdf) |
| **12** | **[AKTU PYQs &amp; Solved Decompositions](12_Unit_3_AKTU_PYQs_and_Solved_Decompositions/)**<br>Past 5-year AKTU 10-markers, Full numerical decompositions, Highest Normal Form identification | [SVG](12_Unit_3_AKTU_PYQs_and_Solved_Decompositions/diagrams/aktu_exam_decomposition_decision_tree.svg) | [HTML](12_Unit_3_AKTU_PYQs_and_Solved_Decompositions/12_Unit_3_AKTU_PYQs_and_Solved_Decompositions.html) \| [PDF](12_Unit_3_AKTU_PYQs_and_Solved_Decompositions/12_Unit_3_AKTU_PYQs_and_Solved_Decompositions.pdf) |

---

## 🎯 Master Normal Form Hierarchy &amp; Quick Comparison

```
1NF (Atomic Domains)
 └── 2NF (No Partial Dependencies)
      └── 3NF (No Transitive Dependencies: X is Super Key OR Y is Prime)
           └── BCNF (Strict Super Key: Every determinant X MUST be Super Key)
                └── 4NF (No Multivalued Dependencies X ↠ Y)
                     └── 5NF / PJNF (No Join Dependencies ⋈[R1...Rn])
```
