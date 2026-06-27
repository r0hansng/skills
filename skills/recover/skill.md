---
name: recover
description: When something goes wrong during a build, diagnose what type of failure it is before deciding how to respond. Targeted fix, hard reset, or full rethink — the right response depends on the right diagnosis.
---

Not every problem is a bug. Not every bug needs debugging.

When something goes wrong with AI-assisted development, the instinct is to keep prompting — describe the problem, ask for a fix, get another broken version, describe that problem, ask for another fix. The session gets longer. The context gets polluted. The code gets worse.

The problem is not the code. The problem is not knowing what type of failure you are dealing with.

This skill diagnoses the failure first. Then it prescribes the right response. Those are two separate steps and they cannot be swapped.

---

## Step 1 — Describe What Went Wrong

The developer describes the problem. The skill listens before doing anything else.

Ask:

```text
Describe what is wrong. Be specific:

- What did you expect to happen?
- What happened instead?
- How has the problem changed over your attempts to fix it?
- Approximately how many times have you tried to fix it already?
```

Read the answer carefully. The number of attempts provides context, but the progression of the problem is usually a stronger indicator of what type of failure you are dealing with.

---

## Step 1.5 — Gather Evidence

Before diagnosing the failure, gather the minimum evidence required to support the diagnosis.

Depending on the project, this may include:

- relevant code
- error messages
- logs
- runtime output
- compiler or build output
- test failures
- configuration
- documentation

Read only what is directly relevant to the reported problem.

Do not inspect the entire project unless the diagnosis genuinely requires it.

If there is not enough evidence to confidently identify the failure mode, say so and continue gathering evidence rather than guessing.

---

## Step 2 — Identify the Failure Mode

Based on the available evidence, determine which of the following failure modes best matches the situation.

### Failure Mode 1 — A specific thing is broken

**Signs:**

- The problem is isolated to a specific part of the project
- The rest of the project behaves as expected
- The failure is reproducible or clearly observable
- The error or incorrect behavior is specific

**What it means:**

This is a normal implementation defect. It has a root cause that can usually be identified and fixed precisely.

**Response:** Targeted Fix — proceed to Step 3A.

---

### Failure Mode 2 — Recovery cost exceeds repair cost

**Signs:**

- Multiple repair attempts have introduced new problems
- Fixes are patching previous fixes
- The original issue has become difficult to identify
- Continuing to patch is likely to cost more than rebuilding cleanly

**What it means:**

The current implementation or session has become difficult to recover efficiently. Continuing in the same direction is likely to waste more time than starting from a clean foundation.

**Response:** Hard Reset — proceed to Step 3B.

---

### Failure Mode 3 — The foundation is wrong

**Signs:**

- The implementation fundamentally misunderstands the requirements, architecture, or technology
- Individual fixes do not move the implementation closer to the desired outcome
- The overall approach is incorrect rather than a specific implementation detail
- Correct behavior requires changing the underlying approach

**What it means:**

This is not a debugging problem. The implementation is based on an incorrect understanding and should be reconsidered before further changes are made.

**Response:** Rethink — proceed to Step 3C.

---

Before proceeding, communicate your diagnosis.

```text
This appears to be Failure Mode [1/2/3] — [name].

Reason:
[Brief explanation.]

Confidence:
High / Medium / Low

If confidence is not High, explain what additional evidence would increase confidence.

Here is how we should proceed:
```

---

## Step 3A — Targeted Fix

For Failure Mode 1.

### Diagnose before touching code

Ask the developer for:

- the exact error or incorrect behavior
- the relevant file, module, or function
- what the implementation is expected to do
- what it actually does

Read only the code and supporting evidence directly related to the issue.

---

### Identify the root cause

Do not suggest a fix until the root cause has been identified.

Before declaring a root cause, verify that it explains:

- every observed symptom
- why the failure occurs
- why unaffected parts still behave correctly
- why the proposed fix should eliminate the problem

State it clearly.

```text
Root cause:
[Specific explanation.]

This is different from the symptom because:
[Explanation.]
```

---

### Suggest a precise fix

Describe the smallest change that addresses the root cause.

```text
Fix:
[Describe what needs to change.]

Why this resolves the issue:
[Explanation.]
```

Wait for the developer to confirm before making any changes.

---

### If the fix does not work

Do not immediately suggest another fix.

Instead:

- re-evaluate the root cause
- compare it against the available evidence
- determine whether the diagnosis should change

If repeated diagnoses fail, reconsider whether this is actually Failure Mode 2 or Failure Mode 3.

---

## Step 3B — Hard Reset

For Failure Mode 2.

### Acknowledge the situation

```text
The current implementation is likely costing more to recover than to rebuild.

A clean restart is recommended because continuing to patch is unlikely to be the fastest or safest path forward.

Before starting over, preserve anything worth keeping.
```

---

### Save what is valuable

Capture:

- the original feature goal
- what parts are known to be correct
- what approaches did not work
- what should be avoided next time

```text
## Reset Note — [Feature Name]

### Original goal

[...]

### What went wrong

[...]

### What to avoid

[...]

### Recommended starting point

[What to keep, what to discard, and where to begin.]
```

---

### Recommend next steps

```text
Recommended next steps:

1. Preserve the reset note.
2. Save any useful project state.
3. Start a fresh session if appropriate.
4. Restore any saved project context or memory.
5. Begin again using the reset note as context.
```

---

## Step 3C — Rethink

For Failure Mode 3.

### Identify the incorrect assumption

The issue is not a bug—it is an incorrect understanding.

```text
Incorrect assumption:

Assumed:
[...]

Reality:
[...]

Because of this, the current implementation cannot be corrected by incremental fixes alone.
```

---

### Describe the correct approach

```text
Correct approach:

[...]

Key difference from the current approach:

[...]

What should be discarded:

[...]

What can still be reused:

[...]
```

---

### Confirm understanding

Do not begin rebuilding immediately.

```text
Does this diagnosis match your understanding?

If yes, we can begin again using the corrected approach.

If not, explain what does not match before we continue.
```

---

## Guiding Principles

Throughout this process:

- Prefer evidence over intuition.
- Prefer diagnosis over implementation.
- Prefer confidence over speed.
- Revise the diagnosis immediately if new evidence contradicts it.
- Read only what is necessary to support the diagnosis.
- Avoid guessing when evidence is insufficient.

---

## The Principle

The worst thing you can do when something is broken is keep doing the same thing faster.

Diagnose first.

Respond appropriately.

Different failures require different responses, and correctly identifying the failure mode is often the most important part of solving the problem.