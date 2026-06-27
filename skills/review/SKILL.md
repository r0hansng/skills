---
name: review
description: After building a feature, verify it matches what was planned, respects the project's architecture and conventions, and is ready for production. Reports issues clearly so the developer decides what to fix.
---

Building is not done when the code runs. It is done when the code is correct.

AI moves fast. Fast means things get built that work on the surface but drift from the architecture, violate established conventions, or miss important edge cases. This skill catches those issues before they compound into bigger problems.

Run this after every feature. Before you move on.

## What This Skill Does Not Do

It does not fix anything. It reports what it finds and lets the developer decide what matters and what to do about it. Fixing without understanding is how problems get buried, not solved.

It reviews the implementation relative to the project's established architecture, conventions, and documented standards—not personal preferences or framework-specific best practices.

Do not report an issue solely because you would have implemented it differently.

Do not assume behavior that cannot be verified from the available code, tests, logs, documentation, or project context. If something cannot be verified, report it under **Not Verified** rather than presenting it as a confirmed issue.

---

## Step 1 — Understand What Should Have Been Built

Before reviewing anything, establish the benchmark.

Read in this order:

- The implementation plan from `/architect` if one exists
- The feature description or task that was given
- Any relevant context files — architecture boundaries, coding standards, design rules, or project conventions

If no plan exists, ask the developer to describe what the feature was supposed to do before reviewing. You cannot verify correctness without knowing what correct looks like.

Review the implementation relative to the project's own architecture, conventions, and constraints.

Do not assume particular languages, frameworks, folder structures, design patterns, or technologies unless they are present in the project or explicitly documented.

---

## Step 1.5 — Establish Review Scope

Identify what belongs to this feature before reviewing.

Where applicable, include:

- Modified source files
- Public interfaces
- Modules or packages
- Configuration changes
- Persistent storage changes
- Automated verification
- Documentation updates

A review that misses part of the implementation is not a complete review.

---

## Step 2 — Review in Three Layers

The purpose of this review is to determine whether the implementation is correct within the context of this project—not whether it matches a generic ideal.

Evaluate the implementation relative to:

- the agreed implementation plan
- the project's architecture
- the project's conventions
- the project's documented standards

Do not introduce new standards during the review.

### Layer 1 — Does it match the plan?

Compare what was built against what was planned.

Check:

- Every part of the feature description — is it all there?
- The decisions made during planning — are they reflected in the implementation?
- The scope — did the implementation stay within bounds or add things that were not asked for?

Flag anything that was planned but missing.

Flag anything that was built but not planned.

---

### Layer 2 — Does it integrate correctly with the existing system?

This is where AI drift most commonly happens. The feature works, but it violates the project's established structure.

Check:

- **Architecture boundaries** — do responsibilities remain within the project's architectural boundaries? Compare against the existing architecture rather than assuming one.
- **Project conventions** — does the implementation follow the project's established conventions, reusable abstractions, and patterns?
- **Code standards** — does the implementation follow the project's naming conventions, organization, error handling strategy, typing strategy, documentation standards, or equivalent practices?
- **Existing patterns** — does this introduce a new approach where an established project pattern should have been reused?
- **Regression risk** — could this change unintentionally affect existing behavior or compatibility?

---

### Layer 3 — Is it production ready?

Check:

- Error handling — what happens when things go wrong? Are failures handled appropriately?
- Operational states — where applicable, are initialization, shutdown, retries, unavailable dependencies, invalid inputs, empty results, and partial failures handled correctly?
- Runtime diagnostics — are there any warnings, runtime errors, failed builds, failing tests, exceptions, or other diagnostics relevant to this project?
- Obvious defects — anything that would clearly fail under normal usage?
- Security and data handling — where applicable, are access controls, input validation, sensitive data handling, and exposed interfaces implemented appropriately?
- Performance sanity check — are there any obvious inefficiencies or unnecessary work that would materially affect normal usage?
- Automated verification — if the project includes tests or another verification strategy, does this feature integrate with it appropriately?

---

## Step 3 — Report What You Found

After completing all three layers, produce a clear report.

Do not bury issues.

Do not soften them.

Report only what you could verify.

```text
## Review — [Feature Name]

### Layer 1 — Plan Alignment
PASS / ISSUES FOUND

[List any gaps between what was planned and what was built]

### Layer 2 — System Integration
PASS / ISSUES FOUND

[List any architecture, convention, or project standard violations]

### Layer 3 — Production Readiness
PASS / ISSUES FOUND

[List any production concerns, edge cases, runtime issues, or defects]

### Not Verified

[List anything that could not be verified from the available context.]

### Summary

[X] issues found across [Y] layers.

### Recommendation

Choose one:

- Ship
- Ship with known issues
- Do not ship
```

---

## Step 4 — Let the Developer Decide

After presenting the report, stop.

Do not begin fixing issues.

Do not suggest fixes unless the developer explicitly asks.

Wait for the developer to:

- Ask you to fix a specific issue
- Tell you an issue is intentional and can be ignored
- Confirm everything is resolved and ready to move on

The developer owns the quality decision.

You inform it.

---

## Severity Guide

Not all issues are equal.

Label every issue with one of the following severities.

### Blocking — Do not ship

- Security vulnerabilities
- Data loss risks
- Core functionality missing
- Production crashes
- Implementation does not satisfy the agreed requirements

### Critical — Fix before moving on

- Architecture violations that will negatively affect future work
- Missing error handling causing incorrect behavior
- Major regression risks

### Important — Fix soon

- Violations of established project conventions
- User-facing edge cases
- Maintainability issues that will compound over time

### Minor — Fix when convenient

- Naming inconsistencies
- Readability improvements
- Non-essential optimizations
- Cosmetic inconsistencies

---

## The Standard

The question this skill answers is not:

> "Does it work?"

The question is:

> "Is it correct within the context of this project?"

Working and correct are not the same thing.

A feature can work today while introducing architectural drift, regressions, or long-term maintenance problems.

Review exists to catch that difference.