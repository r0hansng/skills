# AI Engineering Skills Toolkit

License: MIT

AI agents are powerful. They are also stateless systems (no persistent memory between sessions) and pattern-driven tools that will confidently produce incorrect or inconsistent results if left unchecked.

This toolkit introduces structured engineering discipline into AI-assisted development: planning before execution, diagnosis before fixing, verification after implementation, design consistency over time, and externalized memory across sessions.

It is a set of operational skills, not a framework.

---

# Philosophy

Most AI development failures are not technical — they are procedural.

The core issues are:
- starting implementation without alignment
- debugging without diagnosing failure type
- reviewing only for “does it run”
- losing design consistency across UI components
- losing context between sessions

This toolkit enforces the missing discipline.

It keeps the developer in control of reasoning, not just output.

---

# Install

If distributed as a package:

```bash
npx skills@latest add your-org/skills
```

Or manually include the SKILL.md definitions in your agent configuration.

---

## Skills

### /architect

Use before building anything.

This skill ensures alignment before implementation begins.

It:
- clarifies ambiguous terminology
- aligns scope and expectations
- surfaces important design decisions
- produces a structured implementation plan
- prevents incorrect assumptions from entering the codebase

This is a collaborative engineering thinking step, not a specification exercise.

### /recover

Use when something breaks during development.

Not every failure is a bug, and not every bug requires the same response.

This skill classifies failures into:
* Targeted Fix → isolated issue with clear root cause
* Hard Reset → session is polluted, continue would degrade quality
* Rethink → foundational misunderstanding of requirements or approach

It prevents endless debugging loops and forces correct recovery strategy selection.

### /review

Use after building a feature.

This skill validates correctness beyond runtime behavior.

It evaluates:
 - alignment with the original plan
 - system and architectural consistency
 - production readiness and edge cases
 - deviations from established patterns

It explicitly separates:

- what works
- vs what is correct

It does not fix issues — it reports them so the developer decides.

### /imprint

Use after building any UI component.

This skill enforces long-term UI consistency by extracting design intent from components and storing it in a shared registry.

It captures:
 - visual hierarchy
 - spacing systems
 - typography rules
 - color semantics
 - interaction patterns
 - shape language
 - relationships between components

Instead of storing implementation details, it stores design decisions.

Output is written to design-registry.md.

This ensures that every future component is built using the same visual logic.

### /remember

Use at the start and end of every session.

This skill provides session persistence for stateless AI systems.

It creates continuity across conversations by externalizing memory.

Commands
* /remember save → stores current session state into memory.md
* /remember restore → restores previous session context before continuing

It captures:

- what was built
- key decisions
- current state
- next steps
- unresolved questions

It prevents context loss between sessions.

How to Use

```
/architect  →  Build  →  /review  →  Ship
                 ↓
/imprint  (after every UI component)
/remember  (end and start of every session)
/recover   (when something breaks)
```

Skill Interaction Rules
* /architect → prevents incorrect builds
* /recover → fixes failure classification before action
* /review → validates correctness after implementation
* /imprint → enforces UI consistency across time
* /remember → preserves state across sessions

Each skill solves a different failure mode. They are not interchangeable.

Output Artifacts

Some skills generate persistent files:

* /architect → implementation plan (in-session reference)
* /review → structured review report
* /imprint → design-registry.md
* /remember → memory.md
Why This Exists

AI does not fail because it cannot write code.

It fails because:

* it does not know when to stop and plan
* it does not diagnose failure modes correctly
* it does not evaluate correctness beyond execution
* it does not preserve design consistency
* it does not retain memory across sessions

This toolkit restores those missing constraints.

Installation Principle

These skills are not a library.

They are a discipline layer on top of AI-assisted development.

They work best when used consistently, not selectively.

A skill used occasionally is not a system. It is a suggestion.

Minimal Operating Rules

If you remember nothing else:

Plan before building → /architect
Diagnose before fixing → /recover
Verify after building → /review
Maintain consistency → /imprint
Persist context → /remember
Outcome

When used correctly, this system produces:

fewer incorrect implementations
reduced debugging cycles
consistent architectural decisions
stable UI design systems
continuity across sessions

It does not make AI faster.

It makes AI disciplined.