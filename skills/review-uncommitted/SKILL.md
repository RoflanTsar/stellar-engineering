---
name: review-uncommitted
description: "Review the uncommitted changes - identify bugs and broken logic, make sure the code is high quality and follows standards."
---

## Process

### 1. Analyze uncommitted changes, each step fully

* Correctness: Audit for regressions, bugs and detect bullshit.
* Code Quality: Flag any duplicated code, fragile logic, suboptimal architecture, or structural decisions that will cause future technical debt.
  * Use repo's file like "CODING_STANDARDS.md" or "engineering-standards.md" or "CONTRIBUTING.md" if exists. Make sure audited code quality is up to.
* Integration: Identify exactly where this implementation will break existing features, disrupt connected data flow, or fail at scale.
  * Check callers, dependencies, shared state, APIs, serialization, events and callbacks, async operations, public interfaces.
* Robustness: Check the math and logic and find potential edge cases that will break it. Suggest improvements.
  * Are there any better algorithms or formulas that might to the task faster? Is there a more optimal data layout?
* Speed: Find performance bottlenecks and opportunities for optimization.
  * Check unnecessary allocations, repeated work, expensive operations in hot paths, excessive copying, poor data structures, unbounded loops, bad scaling, unnecessary I/O or sync, cpu or disk stalling, cache misuse.

### 2. Output - safe to commit?

Separate intended behavior from real issues.

Output all real issues based on their current severity, in this format:

```text
🔴 CRITICAL: 1. ...

🔴 CRITICAL: 2. ...

---

🔴 HIGH: 3. ...

---

🟡 MEDIUM: 4. ...

🟡 MEDIUM: 5. ...

---

🟢 LOW: 6. ...
```

Continue as needed.
