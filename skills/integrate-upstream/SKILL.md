---
name: integrate-upstream
description: "Integrate and merge upstream commits to a local codebase without breaking features."
---

# Goal

Integrate all pending upstream commits into the current local codebase, **one commit at a time**, without creating any Git commits.

Repeat the workflow below until all relevant commits are processed.

## 1. Scope and Commit Order

Branches with pending commits are `upstream/master` and `upstream/release`, unless others are mentioned in the user message.

The local branch `R` is a tracking marker (unless other name is mentioned in the user message). It points to the **last upstream commit that we already processed**.

The first commit to process may be mentioned in the user message.

Identify all subsequent commits from both upstream branches.

- Process each unique commit exactly once.
- Preserve dependency order.
- Account for commits shared between the two branches.
- Do not assume both branches have a single linear history.
- Handle merge commits carefully. Do not guess which parent to use.

## 2. Integration Loop

For **each pending upstream commit**, complete the following steps before moving to the next.

### Step A — Apply

Apply the upstream commit without creating a local commit.

Use `git cherry-pick --no-commit` or an equivalent safe method.

**Important:**
- Never create commits.
- Preserve all existing local changes.
- Preserve previously staged integrations.
- Keep the current commit's changes separate from previously integrated changes.
- Prefer keeping the incoming changes unstaged during analysis.
- Remember that `cherry-pick --no-commit` stages changes by default. Handle the index carefully.

### Step B — Analyze

Thoroughly analyze the incoming changes against the current local architecture.

Determine:

1. **Functional purpose:** What does this commit do? Explain in simple language.
2. **Technical changes:** What code, systems, and behavior does it modify?
3. **Relevance:** Do we need these changes? Are they useful for our local codebase?
4. **Compatibility:** Does anything conflict with our advanced local architecture?
5. **Duplication:** Have we already implemented equivalent or better functionality locally?
6. **Integration requirements:** What additional changes are necessary to integrate this correctly?
7. **Regression risks:** Could this break existing features, behavior, or architectural guarantees?

Analyze the actual code and its dependencies. Do not rely only on commit messages.

### Step C — Decide and Plan

Choose the best outcome:

- **Integrate:** The upstream implementation fits the local architecture.
- **Adapt:** The functionality is useful, but its implementation must change to fit the local architecture.
- **Skip:** The changes are unnecessary, obsolete, duplicated, or incompatible.

Prefer the architecturally correct solution over the easiest or smallest patch.

For features, ensure that they work naturally with existing local systems.

Preserve local improvements. Do not replace advanced local implementations with simpler upstream versions.

Determine the exact modifications needed before applying the final integration.

**If the decision involves significant uncertainty or an important architectural trade-off, stop and ask me.**

### Step D — Implement

Execute the integration plan.

- Resolve conflicts correctly.
- Adapt upstream code to the local architecture where necessary.
- Preserve existing local features and behavior.
- Avoid duplicate systems or unnecessary compatibility layers.
- Update related code and dependencies when required.
- Ensure the changes work together as one coherent implementation.

If the commit should be skipped, remove only its incoming changes.

Never discard unrelated local work.

### Step E — Verify

Check the final result before proceeding.

- Review the complete integration diff.
- Check for unintended changes.
- Check compatibility with existing systems.
- Run relevant builds and tests where practical.
- Fix problems introduced by the integration.
- Ensure the local codebase remains consistent.

Do not treat a successful cherry-pick as proof of correct integration.

### Step F — Stage

Stage the completed integration.

**Do not commit.**

Preserve all previously staged integrations.

If the commit was skipped, ensure its unwanted changes are not left in the working tree or index.

### Step G — Advance R

Move the `R` branch reference to the **original upstream commit SHA** that was just processed.

`R` must always identify the last fully processed upstream commit, regardless of whether its changes were integrated or skipped.

Do not reset or switch the working branch when updating this marker.

Advance `R` only after the current commit has been fully processed and verified.

### Step H — Repeat

Continue with the next pending upstream commit.

Repeat Steps A–G until all relevant commits from `upstream/master` and `upstream/release` have been processed.

## 3. Global Rules

1. **Never create Git commits.** All accepted integrations must remain staged.
2. **Never lose local changes.** Preserve both staged and unstaged work.
3. **Protect local architecture.** Adapt upstream changes to our design, not the other way around.
4. **Prioritize correctness.** Do not blindly accept upstream implementations.
5. **Maintain compatibility.** New features must integrate naturally with existing features.
6. **Do not accumulate unresolved problems.** Complete and verify each integration before advancing.
7. **Ask only when necessary.** Resolve routine implementation decisions independently. Stop for genuinely ambiguous or high-impact architectural decisions.
8. **Maintain progress records.** Track each processed SHA, integration decision, important modifications, and verification results.

## 4. Completion Criteria

The task is complete when:

- Every relevant upstream commit has been evaluated.
- All accepted changes have been correctly integrated.
- All rejected changes have been safely excluded.
- The local architecture and existing functionality are preserved.
- All accepted changes are staged.
- No new Git commits have been created.
- `R` points to the last processed upstream commit.
- No unresolved conflicts or known integration regressions remain.

**Continue autonomously until these conditions are satisfied or an important decision requires my input.**
