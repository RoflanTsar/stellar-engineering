---
name: review-uncommitted
description: "Review uncommitted changes - identify bugs and broken logic, make sure the code is high quality and follows standards."
---

## Process

### 1. Analyze uncommitted changes, each step fully

* Correctness: Audit for regressions, detect bugs and bullshit.
* Integration: Identify exactly where this implementation will break existing features, disrupt connected data flow, or fail at scale.
  * Check callers, dependencies, shared state, APIs, serialization, events and callbacks, async operations and race conditions, public interfaces.
* Robustness: Check the math and logic and find potential edge cases that will break it. Suggest improvements.
  * Are there any better algorithms or formulas that might fit the task better? Is there a more optimal data layout? And so on.
* Speed: Find performance bottlenecks and opportunities for optimization.
  * Identify unnecessary allocations, repeated work, expensive operations in hot paths, excessive copying, poor data structures, unbounded loops, bad scaling, unnecessary I/O or sync, cpu or disk stall, cache lack or misuse, etc.
* Code Quality: Flag any duplicated code, fragile logic, suboptimal architecture, or structural decisions that will cause future technical debt.
  * Use repo's file like "CODING_STANDARDS.md" or "engineering-standards.md" or "CONTRIBUTING.md" if exists. Make sure audited code quality meets requirements.

### 2. Output - safe to commit?

Separate intended behavior from real issues.
When reporting to user, append brief explanations to issues (very simple ELI5 language), so that they could understand.
Mention affected files if appropriate.
Output all real issues based on their current severity, in markdown format like this:

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
