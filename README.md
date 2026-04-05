![C Language](https://img.shields.io/badge/Language-C-00599C?style=for-the-badge&logo=c)
![Compiler](https://img.shields.io/badge/Compiler-GCC-FFD133?style=for-the-badge&logo=gnu)
![OS](https://img.shields.io/badge/OS-Ubuntu-E95420?style=for-the-badge&logo=ubuntu)

# **Algorithmic Evolution of Sequence Alignment: A Comparative Study**

---

## **1. Project Executive Summary**
This project provides a comprehensive computational analysis of the two pillars of sequence bioinformatics: **Global Alignment (Needleman-Wunsch)** and **Local Alignment (Smith-Waterman)**. 

Beyond simple alignment, this repository demonstrates the **computational evolution** of these algorithms—moving from computationally expensive naive recursion to high-performance Dynamic Programming (DP) techniques. All implementations were cross-validated against the **Freiburg RNA Bioinformatics** suite to ensure mathematical and biological accuracy.

---

## **2. Core Bioinformatics Algorithms**

### **A. Needleman-Wunsch (Global Alignment)**
* **Sequence A:** `GATCGGGAC` (9 bp)
* **Sequence B:** `CGTACACACTAG` (12 bp)
* **Purpose:** Optimizes the alignment across the entire length of both sequences.
* **Scoring Parameters:** * **Match:** +1 
    * **Mismatch:** -1 
    * **Gap (Indel):** -2

### **B. Smith-Waterman (Local Alignment)**
* **Purpose:** Identifies the most conserved sub-regions (motifs) between divergent sequences.
* **Scoring Constraint:** Includes a **Zero-Floor** ($\max(0, \text{score})$), preventing negative scores from propagating and allowing the alignment to restart at any point.
* **Scoring Parameters:** Match (+1), Mismatch (-1), Gap (-2).

---

## **3. Implementation & Complexity Analysis**

I implemented each algorithm using three distinct programming paradigms to benchmark performance:

| Method | Approach | Time Complexity | Memory Complexity | Verdict |
| :--- | :--- | :--- | :--- | :--- |
| **1.1 / 2.1 Naive Recursive** | Direct recurrence relation | $O(3^{n+m})$ | $O(n+m)$ (Stack) | **Inefficient:** Subject to "Redundant Subproblem" explosion. |
| **1.2 / 2.2 Top-Down** | Memoization (Recursive + Cache) | $O(n \times m)$ | $O(n \times m)$ | **Balanced:** Significant speedup via state-retention. |
| **1.3 / 2.3 Bottom-Up** | Tabulation (Iterative Matrix) | $O(n \times m)$ | $O(n \times m)$ | **Optimal:** The industry standard for production-grade tools. |

---

## **4. Repository Structure**
The source code is organized into a single directory for modularity:
```text
└── acb_alignment_algorithms/
    ├── nw_recursive.c    # Global - Naive approach
    ├── nw_top_down.c     # Global - Memoized approach
    ├── nw_bottom_up.c    # Global - Iterative DP (Production)
    ├── sw_recursive.c    # Local - Naive approach
    ├── sw_top_down.c     # Local - Memoized approach
    └── sw_bottom_up.c    # Local - Iterative DP (Production)
```
## **5. Usage & Benchmarking**
```bash
# To compile and execute the algorithms on a Linux/Ubuntu environment:

# 1. Enter the directory
cd acb_alignment_algorithms/

# 2. Compile the Bottom-Up implementation (Example: Needleman-Wunsch)
gcc nw_bottom_up.c -o nw_exec

# 3. Execute and measure runtime using the Linux 'time' utility
time ./nw_exec
```
## **6. Key Observations**

* **The Power of DP:** While the **Naive Recursive** method struggled with sequences longer than 15 characters, the **Bottom-Up** approach handled the 9bp vs 12bp comparison instantaneously.
* **Local vs. Global:** Because Sequence B is significantly longer than Sequence A, the **Smith-Waterman** algorithm successfully isolated the high-similarity core without penalizing the terminal "overhangs" that the Global alignment was forced to account for.
* ## **7. References**

1. **Needleman, S. B., & Wunsch, C. D. (1970).** A general method applicable to the search for similarities in the amino acid sequence of two proteins. *Journal of Molecular Biology*.
2. **Smith, T. F., & Waterman, M. S. (1981).** Identification of Common Molecular Subsequences. *Journal of Molecular Biology*.
3. **Validation Tool:** [Freiburg RNA Tools - Sequence Alignment](https://rna.informatik.uni-freiburg.de/Teaching/index.jsp?toolName=Needleman-Wunsch)

