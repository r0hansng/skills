---
name: glyph
description: After building any UI component, extract the visual patterns that matter for consistency and save them to design-registry.md. So every component built after this one matches the established design language instead of drifting over time.
---

UI consistency does not happen by accident. It emerges when every component is built with awareness of existing design patterns.

AI-built interfaces often fail in the same way: components are created in isolation. Without a shared memory of design decisions, spacing drifts, visual weight becomes inconsistent, and interaction patterns diverge. The result is a fragmented interface rather than a coherent system.

This skill prevents that. Run it after building any UI component. It extracts the **design decisions** behind what was just built and stores them in a registry so future components can align with the same system.

One command. Run it every time. That is the whole mechanism.

---

## How to Invoke

After building any UI component:

```
/imprint
```

To target a specific file:

```
/imprint [filepath]
```

To audit an existing UI system for inconsistencies:

```
/imprint audit
```

If no filepath is provided, the system identifies recently created or modified UI components automatically.

---

## When to Use Audit Mode

Use `/imprint audit` when:

- The UI already exists but consistency is unclear
- Multiple sessions have passed without imprinting
- Visual inconsistency is noticeable but not traceable
- Establishing a baseline design system for the first time in an existing project

Always run audit mode before beginning imprint tracking in a mature or partially built UI.

---

## Step 1 — Identify What Was Built

If a filepath is provided, read that file directly.

If not:

- Identify recently created or modified UI components in the session
- Focus only on files that define visual structure or user-facing interface
- If multiple candidates exist, ask:

```
Which component should I extract design patterns from?
```

Do not proceed until the correct scope is confirmed.

---

## Step 2 — Extract Design Patterns (Not Implementation Details)

Extract **design semantics**, not framework-specific values.

Focus on what the UI communicates visually, not how it is implemented.

### Extract the following:

#### Visual Identity
- Surface treatment (card, elevated, flat, overlay, etc.)
- Background behavior (light, dark, muted, contextual)
- Border presence and emphasis
- Elevation or depth (shadow, layering, flatness)

#### Shape Language
- Corner radius style (sharp, soft, rounded, pill-like)
- Consistency of shape across components

#### Typography System
- Hierarchy (title, body, caption, label)
- Weight usage (regular, medium, semibold, bold)
- Semantic meaning of text styles

#### Spacing System
- Internal padding patterns
- Vertical rhythm between elements
- Density (compact, regular, spacious)

#### Interaction Patterns
- Hover behavior (subtle, elevated, highlighted)
- Focus behavior (ring, outline, glow, none)
- Active/pressed states
- Disabled state treatment

#### Color Semantics
- Primary, secondary, muted text roles
- Accent usage behavior
- Error/success/warning semantics (if present)

#### Component Relationships
- Which components share visual structure
- Reused layouts or structural similarities
- Hierarchical consistency between parent/child components

---

### Do NOT extract:

- Framework-specific class names
- Absolute layout values (width/height unless semantically meaningful)
- Implementation details unrelated to visual consistency
- Animation timing unless it defines a system-wide motion language

---

## Step 3 — Write to design-registry.md

Open `design-registry.md`. If it does not exist, create it.

Append a new entry. Never overwrite existing entries unless explicitly updating a shared pattern.

If this component introduces or modifies an existing pattern, update that pattern instead of duplicating it.

---

### Entry Format

```markdown
### [Component Name]

File: [filepath]
Last updated: [date]

## Visual Identity
- Surface:
- Background:
- Border:
- Elevation:

## Shape Language
- Radius:

## Typography
- Hierarchy:
- Weights:

## Spacing
- Internal:
- Layout rhythm:
- Density:

## Interaction
- Hover:
- Focus:
- Active:
- Disabled:

## Color Semantics
- Primary text:
- Secondary text:
- Muted text:
- Accent usage:

## Component Relationships
- Related patterns:
- Matches:
- Inherited styles:

## Pattern Notes
- Why these decisions were made
- What must remain consistent in future components
- Allowed variations
- Known intentional deviations (if any)

## Confidence
- High / Medium / Low
- Reason (if not High)
```

---

## Step 4 — Detect Pattern Drift

Before finalizing the entry:

- Compare extracted patterns with existing registry entries
- Identify any deviation from established design language
- If a deviation exists, determine whether it is intentional

If unclear, flag it:

```
Pattern drift detected:
[description]

Confirm whether this is intentional before updating the registry.
```

Do not silently normalize inconsistencies.

---

## Step 5 — Confirm What Was Captured

After writing to `design-registry.md`, confirm:

```
Imprinted: [Component Name]

Captured Design Patterns:
- Visual Identity: [summary]
- Shape: [summary]
- Typography: [summary]
- Spacing: [summary]
- Interaction: [summary]

Updated Registry: design-registry.md

Future components should align with these patterns unless explicitly overridden.
```

If inconsistencies were found:

```
Note:
[Issue or deviation observed]
```

---

## Audit Mode — /imprint audit

Audit mode establishes or repairs a baseline design system when consistency is already uncertain.

---

### Step 1 — Scan UI system

Identify all UI components across the project.

Extract recurring visual patterns across:

- surfaces
- typography
- spacing
- interaction behavior
- color semantics
- shape language

---

### Step 2 — Identify inconsistencies

Report conflicts across the system:

```
## UI Design Audit

### Conflicts

## Surface patterns
- List variations in card/surface treatment
Recommendation: standardize to [pattern]

## Shape system
- List radius inconsistencies
Recommendation: choose dominant or token-based system

## Typography hierarchy
- List inconsistencies in text roles
Recommendation: standardize semantic roles

## Spacing system
- List spacing inconsistencies
Recommendation: define consistent scale

## Interaction states
- List hover/focus/active variations
Recommendation: unify interaction model

## Color semantics
- List inconsistent usage of text/accent/error/success colors
Recommendation: align with semantic system

## Hardcoded values
- List any raw colors or non-token values
These should be replaced with semantic tokens where applicable.

## Recommended Design Baseline
[Unified system proposal based on existing patterns and design intent, not just majority usage]
```

---

### Step 3 — Confirm baseline

Present audit results. Do not modify anything yet.

Ask:

```
Audit complete. [X] inconsistencies found.

Before updating design-registry.md:

1. Does this baseline reflect the intended design system?
2. Should any patterns be treated as intentional exceptions?
3. Should any inconsistencies be explicitly preserved?
```

---

### Step 4 — Establish baseline

After confirmation, write baseline into `design-registry.md`:

```markdown
## Design System Baseline
Established: [date]

This baseline represents the intended visual system derived from existing UI.

## Core Patterns
- Surface:
- Radius:
- Typography:
- Spacing:
- Interaction:
- Color semantics:
```

---

### Step 5 — Deviation list

```
## Components requiring alignment

- [Component] — deviates in [pattern] → should be [standard]
```

---

## Core Principle

This system does not store code.

It stores **design intent**.

The goal is not to remember how components were implemented.

The goal is to ensure every new component feels like it belongs to the same product.

Consistency is not achieved by repetition of classes or values.

It is achieved by repetition of design decisions.
```