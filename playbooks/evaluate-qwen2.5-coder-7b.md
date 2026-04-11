# Playbook: Evaluate qwen2.5-coder-7b Prompt Variants

## Goal
Run repeatable, evidence-producing evaluations for system prompt variants targeting local Qwen2.5-Coder-7B usage.

## Scope (first pass)
- Model target: `qwen2.5-coder-7b` (provisional target)
- Prompt baseline: `prompts/system/qwen2.5-coder-7b-base.md`
- Compare at least 3 variants:
  - V0: baseline
  - V1: stricter format constraints
  - V2: shorter constraints + stronger user-side reinforcement

## What to test
1. Coding transformation task (edit/refactor with constraints).
2. Architecture tradeoff analysis task.
3. Summarization with evidence/inference/hypothesis labeling.
4. Structured output task (strict JSON or fixed markdown headers).

## Experimental controls
- Same task set across all variants.
- Same context payload per task.
- Minimum 3 repeated runs per task/variant.
- Fixed decoding parameters when possible.
- Record runtime setup (quantization, context window, sampler settings).

## Scoring rubric
Use `knowledge/prompting/evaluation-rubric.md`.
Score each run for:
- instruction following
- format adherence
- reasoning quality
- verbosity control
- task fitness
- cross-run consistency
- hallucination risk
- context handling quality

## Artifacts to save
Save under:
- `output/eval-results/qwen2.5-coder-7b/<YYYY-MM-DD>/run-<id>.md`
- `output/eval-results/qwen2.5-coder-7b/<YYYY-MM-DD>/raw/` (raw model outputs)

Each run report must include:
- prompt variant ID
- exact task prompt
- model runtime config
- rubric table with evidence excerpts
- pass/fail notes for output contract

## How to compare variants
1. Compute per-criterion average for each variant.
2. Compute stability note from repeated runs (stable/provisional/inconclusive).
3. Check failure mode frequency:
   - format drift
   - missed constraints
   - unsupported claims
4. Prefer variants that improve format adherence and instruction following **without** degrading task fitness.

## Improvement decision rule (first-pass)
A variant is “better” if:
- +0.4 or greater average gain in format adherence **and** instruction following,
- no >0.3 drop in task fitness,
- same or lower hallucination risk score,
- stable in at least 2 of 3 repeated runs.

## Post-run updates required
- Update `knowledge/models/qwen2.5-coder-7b/profile.md` evidence section.
- Update `knowledge/models/qwen2.5-coder-7b/prompting.md` with confirmed patterns.
- If strategy shifts materially, add a decision record in `knowledge/decisions/`.
