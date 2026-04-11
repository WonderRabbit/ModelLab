# Reusable Prompt Schema

Purpose: define a shared prompt contract that can be reused across models while allowing model-specific patches.

## Schema sections

| Section | Description | Status | Model-sensitive |
|---|---|---|---|
| Role | Who the model is acting as | Mandatory | Low |
| Goal | Task objective and success criteria | Mandatory | Medium |
| Context | Domain info, input docs, constraints from environment | Optional (required when non-trivial) | High |
| Constraints | Hard rules, do/don't rules, safety, scope limits | Mandatory | High |
| Output format | Required structure/schema/examples | Mandatory | High |
| Reasoning strategy | How to approach problem decomposition and checking | Optional | High |
| Style | Tone, verbosity, language, audience | Optional | Medium |
| Model-specific patch | Provider/model tweaks overriding defaults | Optional (mandatory for production model-targeted prompts) | Very high |

## Canonical layout

```md
[ROLE]
...

[GOAL]
...

[CONTEXT]
...

[CONSTRAINTS]
...

[OUTPUT_FORMAT]
...

[REASONING_STRATEGY]
...

[STYLE]
...

[MODEL_PATCH]
...
```

## Guidance by section

### 1) Role (mandatory)
- Keep short and operational (1-3 lines).
- Avoid personality-heavy instructions.

### 2) Goal (mandatory)
- Define exact completion target and acceptance conditions.
- Include what *not* to optimize for.

### 3) Context (optional/model-sensitive)
- Include only relevant context; avoid dumping full history.
- Prefer structured context blocks with source labels.

### 4) Constraints (mandatory/model-sensitive)
- Put non-negotiables first.
- Use measurable constraints (length, schema keys, prohibited actions).

### 5) Output format (mandatory/model-sensitive)
- Use explicit contract (fields/order/types).
- Add fallback behavior when uncertain.

### 6) Reasoning strategy (optional/model-sensitive)
- Specify decomposition/checklist style without requiring hidden chain-of-thought exposure.
- Encourage verification steps and assumption listing.

### 7) Style (optional)
- Control verbosity and tone explicitly.
- For operational tasks, default to concise + structured bullets.

### 8) Model-specific patch (optional/model-sensitive)
- Use for observed model behaviors (e.g., format drift, verbosity drift).
- Keep patch small and test-backed.

## Minimal production skeleton

```md
[ROLE]
You are ...

[GOAL]
Deliver X with success criteria A/B/C.

[CONSTRAINTS]
- Must ...
- Must not ...

[OUTPUT_FORMAT]
Return markdown with sections: Summary, Evidence, Next Step.

[MODEL_PATCH]
- Reinforce strict format with exact section headers.
- Keep response under N bullets.
```
