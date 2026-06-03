# Prompt Hardening Skill V1

## Purpose
Transform any loose technical/coding request into a self-contained, contract-style prompt that forces an AI to produce correct, one-shot output by eliminating ambiguity, lifecycle errors, and state-transition bugs. Optimised for small, quantized local models (like Qwen 28B) running in agent harnesses.

## When to Use
- User provides an underspecified coding request (game, script, UI, config).
- Output must be a single, immediately usable artifact (HTML file, Python script, etc.).
- Target AI has limited context or reasoning depth.

## Instructions to the Hardening AI
1. Receive the loose prompt.
2. Extract every implied number → create named constants.
3. Define the complete state schema with initial values.
4. Order tasks into linear, dependent segments.
5. List domain-specific pitfalls → explicit bans.
6. Define the exact output format (first character, no fences, no preamble).
7. Create 10-15 testable acceptance criteria.
8. Add a Dependency Checklist for each feature.
9. Declare State Invariants - conditions that must always hold.
10. NEW: Define State Transition Tables - for each major entity, list allowed states and transitions.
11. Write Interaction Trace Tests - step-by-step event sequences.
12. Assign System Ownership - each state field/function owned by one system.
13. Operationalise Final Audit - map each acceptance criterion to concrete code elements.
14. Include a Context Budget Advisory for small models.

## Mandatory Sections

### A. Opening Contract Statement
```
You are building a complete, self-contained [project type]. This is a contract: you must satisfy every specification below. Before outputting, mentally verify that your code meets all acceptance criteria.
```

### B. Exact Constants
```
EXACT CONSTANTS
CONSTANT_NAME = value   // explanation
... (list every magic number here; no other hardcoded numbers allowed)
```

### C. State Initialisation Schema
```
STATE INITIALISATION
stateName = {
  field: initialValue,
  ...
}
```

### D. Implementation Segments (ordered)
```
SEGMENT [N] - [Title]
1. [Step-by-step instruction with exact values]
2. ...
```

### E. Dependency Checklist
```
DEPENDENCY CHECKS
Before implementing each feature, verify the following requirements are met.

Feature [X] requires:
- state field [Y] to be initialised
- helper function [Z] to exist
- timer [T] to be updated with deltaTime
...
```

### F. State Invariants
```
STATE INVARIANTS
The following must always be true:
- [invariant, e.g., health >= 0]
- [invariant, e.g., health <= MAX_HEALTH]
...
```

### G. State Transition Tables (NEW)
```
STATE TRANSITION TABLES
For each major entity, the allowed states and transitions are:

Entity [name]:
- [State A] -> [State B]  (trigger: ...)
- [State B] -> [State C]  (trigger: ...)
...
No other transitions are permitted. Implement these transitions exactly.

Example for an enemy:
Enemy states: SPAWNED -> GROWING -> FLASHING -> REMOVED
- SPAWNED: initial state, immediately transitions to GROWING.
- GROWING: size increases; on click, transitions to FLASHING; on reaching max size, deals damage and transitions directly to REMOVED (no flash).
- FLASHING: drawn white, timer counts down; when timer expires, transitions to REMOVED.
- REMOVED: enemy is deleted from array.
```

### H. System Ownership
```
SYSTEM OWNERSHIP
Assign each piece of state and each helper function to a single owner. No other system may modify owned state directly.

[System 1] owns:
- state fields: ...
- functions: ...

[System 2] owns:
- ...
```

### I. Common Pitfalls Blacklist
```
COMMON PITFALLS - EXPLICIT SAFEGUARDS
- Never use setInterval/setTimeout; use requestAnimationFrame with deltaTime.
- Never create multiple AudioContexts.
- Never hardcode a value that has a constant.
- Never modify state owned by another system.
- Never skip a required state transition (see Transition Tables).
- All time-based updates must use deltaTime (seconds).
- Do not show reasoning, planning, or explanations in the output.
```

### J. Output Requirements (Absolute)
```
OUTPUT REQUIREMENTS (ABSOLUTE)
- The final output must be [format, e.g., single HTML file with everything embedded].
- The response must start with [first characters, e.g., <!DOCTYPE html>] as the very first characters.
- No markdown code fences (```).
- No preamble, no commentary, no "Here is the code".
- The very first character of the response must be [e.g., <].
```

### K. Acceptance Criteria Self-Test
```
ACCEPTANCE CRITERIA (SELF-TEST BEFORE SUBMITTING)
Verify that your code meets all these points. If any fails, fix it before finalising.
1. [Testable statement]
2. ...
```

### L. Interaction Trace Tests
```
INTERACTION TRACE TESTS
Trace the following events step-by-step through your code. For each, verify all state changes, render calls, and cleanup actions.

1. **[Trace name]**
   - Trigger: ...
   - Expected: ...
...
```

### M. Operational Final Audit
```
FINAL AUDIT - OPERATIONAL CHECK
Before submitting, map each acceptance criterion to a concrete code element:

Criterion 1: [statement] -> found in [function name / event listener / state field]
...
Also confirm:
- Every field in the state schema is initialised exactly once.
- Every timer update uses deltaTime (seconds) consistently.
- No constant is hardcoded.
- All required event listeners exist.
- All state transitions follow the Transition Tables.
- The HTML boilerplate matches the template exactly (no drift).
```

### N. Context Budget Advisory
```
CONTEXT BUDGET ADVISORY
If the target model has limited context (e.g., < 8K tokens), prioritise these sections in order:
1. Exact Constants
2. State Schema
3. Interaction Traces
4. State Transition Tables
5. Acceptance Criteria
6. Dependency Checklist
7. State Invariants
8. System Ownership
The Final Audit may be dropped if necessary, but never drop Interaction Traces or State Transition Tables.
```

## How to Use This Skill in Hermes
1. Copy the entire V4 description into the agent's system prompt or as a custom skill.
2. When a user submits a loose request, the hardening AI will output the hardened prompt containing all the mandatory sections.
3. Feed that hardened prompt to the target 28B model as a /goal (or equivalent) command.
4. The model will generate code that adheres to the contract; any remaining errors will be trivial, localisable, and easy to patch.

This skill is designed to be the final blueprint for your Hermes agent. It transforms a vague idea into a precise specification that even a heavily quantized model can execute reliably. Test it with a new project, and you should see the lifecycle bugs vanish. Good luck, and let me know how it goes!
