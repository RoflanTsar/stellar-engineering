---
name: review-codebase
description: "Review full codebase - identify bugs and broken logic, make sure the code is high quality and follows standards."
---

## Process

### 1. Review this codebase for architectural entropy. Each step fully:

* Code Quality: Flag any duplicated code, fragile logic, suboptimal architecture, or structural decisions that will cause future technical debt.
  * Use repo's file like "CODING_STANDARDS.md" or "engineering-standards.md" or "CONTRIBUTING.md" if exists. Make sure audited code quality is up to.
* Correctness: Detect bugs and bullshit/obviously wrong behavior.
* Robustness: Check the math and logic and find potential edge cases (including scale) that will break it. Suggest improvements.
  * Are there any better algorithms or formulas that might fit the task better? Is there a more optimal data layout?
* Speed: Find performance bottlenecks and opportunities for optimization.
  * Identify unnecessary allocations, repeated work, expensive operations in hot paths, excessive copying, poor data structures, unbounded loops, bad scaling, unnecessary I/O or sync, cpu or disk stall, cache lack or misuse.

### 2. Output - safe to commit?

Separate intended behavior from real issues.

Output all real issues based on their current severity, in this markdown format:

**🔴 CRITICAL: 1. ...**

**🔴 CRITICAL: 2. ...**

---

**🔴 HIGH: 3. ...**

---

**🟡 MEDIUM: 4. ...**

**🟡 MEDIUM: 5. ...**

---

**🟢 LOW: 6. ...**

Continue as needed.
