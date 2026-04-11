# Prompting Guidance: Qwen2.5-Coder-7B (First Pass)

Status: provisional until local eval data is collected.

## A) System prompt design for this model

### Recommended pattern
1. Keep system prompt compact and operational.
2. Put hard constraints in short bullet rules.
3. Define output contract with exact section headers.
4. Add explicit uncertainty protocol.
5. Add minimal model patch for known/expected drift.

### Why
- Concise rule-first prompts are expected to improve instruction retention in 7B local deployments. (`inference`)
- Format drift is common when output contracts are vague. (`inference`)

### System prompt essentials
- Role and scope.
- Non-negotiable constraints.
- Output structure.
- “If missing info” behavior.
- Length/verbosity controls.

### System prompt optional elements
- Persona/tone details beyond concise professionalism.
- Few-shot demonstrations (prefer user-level insertion for specific tasks first).

## B) User prompt design for this model

### Recommended pattern
- Repeat the required output format in each request for critical tasks.
- Provide concrete acceptance criteria (tests, constraints, done definition).
- Provide context as labeled blocks: `Context A`, `Context B`.
- Ask for assumptions + unknowns when context is incomplete.

### Responsibility split
- **System prompt** should hold stable behavior defaults.
- **User prompt** should hold task specifics, format reinforcement, and domain constraints.

## C) Output-format reinforcement guidance
- Reinforce format in user prompt when:
  1. output must be machine-consumable,
  2. answer length must be bounded,
  3. repeated production consistency matters.
- For strict outputs, require either:
  - exact markdown headers in fixed order, or
  - JSON with exact key list and “no additional keys”.

## D) Scaffolding and structure choices
- **Step-by-step scaffolding:** useful for architecture/design or debugging plans. (`inference`)
- **TOC-style outline prompts:** likely useful for long analyses to reduce omission risk. (`hypothesis`)
- **Concise rule-based vs natural style:** prefer concise rule-based for reliability; natural style can be layered for user-facing polish after correctness is achieved. (`inference`)

## E) Anti-patterns to avoid (model-focused)
1. Mixed hard rules + preferences in one paragraph.
2. Buried constraints after long context dumps.
3. Asking for “best” answer without decision criteria.
4. Requiring strict format without re-stating schema in the user turn.
5. Overly long system prompts that consume local context budget.

## F) First-pass prompt ingredient matrix
| Ingredient | Priority | Notes |
|---|---|---|
| Explicit task goal + success criteria | Essential | Prevents broad/off-target outputs |
| Hard constraints at top | Essential | Improves adherence |
| Output schema (exact headers/keys) | Essential | Reduces format drift |
| Uncertainty protocol | Essential | Reduces overconfident fabrication |
| Verbosity budget | Essential | Controls local token cost |
| Few-shot examples | Optional | Add only for repeated failure modes |
| Rich persona instructions | Optional | Low ROI for coding tasks |

## G) Confidence notes
- Evidence in repo for Qwen-specific behavior: none yet.
- Current guidance is inference/hypothesis and must be validated via `playbooks/evaluate-qwen2.5-coder-7b.md`.
