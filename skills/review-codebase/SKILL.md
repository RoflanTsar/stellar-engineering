---
name: review-codebase
description: "Review full codebase - identify bugs and broken logic, make sure the code is high quality and follows standards."
---

## Process

### 1. Review this codebase for architectural entropy. Each step fully:

1. **Bugs**: Audit for regressions, wrong results, unhandled edge cases, unfinished implementation, and other bullshit.
2. **Robustness:** Check the math and logic and find potential edge cases (including scale) that will break it. Suggest improvements.
    - Are there any better algorithms or formulas that might fit the task better? Is there a more optimal data layout? And so on.
    - Data safe? No unauthorized data loss?
3. **Speed:** Find performance bottlenecks and opportunities for optimization. 
    - Identify unnecessary allocations, repeated work (every frame/never sleep), expensive operations in hot paths, excessive copying, poor data structures, unbounded loops, bad scaling, unnecessary I/O or sync, cpu or disk stall, cache lack or misuse, etc.
5. **Code Quality:** Flag any duplicated code, dead code, fragile logic, suboptimal architecture, or structural decisions that will cause future technical debt.
    - Repo's file like "CODING_STANDARDS.md" or "engineering-standards.md" or "CONTRIBUTING.md" if exists. Make sure audited code quality meets requirements.
    - Similar code which can be merged into helpers.
    - Existing helpers which can be reused.

### 2. Output - does the codebase need improvements?

Separate intended behavior from real issues.

When reporting to user, append brief explanations to issues in everyday language, so that they could understand without looking at code.
Explain a technical term the first time you use it.
Mention affected files if appropriate.

Output all real issues based on their current severity, in markdown format like this (example):

**🔴 CRITICAL: 1. ...**

**🔴 CRITICAL: 2. ...**

---

**🔴 HIGH: 3. ...**

---

**🟡 MEDIUM: 4. ...**

**🟡 MEDIUM: 5. ...**

---

**🟢 LOW: 6. ...**

...
extremely thorough
