# Playbook: Build System Prompt

## Goal
Transform model research into reusable, model-aware system prompts.

## Inputs
- Common schema (`knowledge/prompting/schema.md`)
- Model profile
- Target task type/domain

## Procedure
1. Draft common core prompt (model-agnostic baseline).
2. Add model-specific patch from profile implications.
3. Add task-specific variation (if needed).
4. Define output contract and failure behavior.
5. Run quick sanity evaluation (format + instruction adherence).
6. Store prompt asset under `prompts/` and, if reusable, template under `.codex/templates/`.

## Design rules
- Keep common core stable; isolate volatility in model patch.
- Use explicit constraints and measurable output format.
- Keep patches minimal and evidence-backed.

## Required outputs
- Prompt file with version tag
- Change rationale
- Known risks and TODO tests
