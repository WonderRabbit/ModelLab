# PLANS

## Phase 0: Scaffold (current)
- Initialize repository structure and baseline docs.
- Define prompt schema, rubric, anti-patterns, and playbooks.
- Add starter model profile templates and initial targets.

## Phase 1: Baseline model research
- Run first-pass evaluations for 3-5 target models.
- Populate `knowledge/models/*` with evidence-labeled findings.
- Save raw outputs under `output/evaluations/`.

## Phase 2: Prompt system iteration
- Build common core system prompt.
- Build model-specific patches and task variations.
- Track changes and rationale in `knowledge/decisions/`.

## Phase 3: Operational hardening
- Add consistency checks and lightweight QA.
- Promote stable findings from provisional to validated.
- Curate reusable prompt kits under `prompts/` and `.codex/templates/`.
