# AGENTS.md

## Repository purpose
This repository is a Codex-operated workspace for model-aware prompt optimization: research model behavior, design reusable prompt strategies, and accumulate durable knowledge.

## Operating rules
1. Read this file first, then follow `PLANS.md` and relevant playbooks.
2. Prefer extending existing docs over creating duplicates.
3. Separate **rules**, **knowledge**, **outputs**, and **decisions**.
4. Mark uncertain claims with evidence level (`evidence`, `inference`, `hypothesis`).
5. Do not present high-confidence model claims without traceable evidence.

## Directory guidance
- `.codex/`: Codex runtime config, profiles, reusable prompt templates.
- `knowledge/`: reusable KB (models, prompting methods, domains, decisions).
- `playbooks/`: repeatable operational workflows.
- `prompts/`: production-ready prompt assets and variants.
- `output/`: experiment logs, evaluations, generated artifacts.
- `skills/`: optional task-specific automation skills.

## Uncertainty handling rules
- Always separate observed behavior from interpretation.
- Record test scope and known limitations.
- Label findings as provisional until replicated.

## Done criteria
A task is done when:
- artifacts are saved in the correct directory,
- reusable knowledge is updated (not only ad-hoc notes),
- decisions/assumptions are documented,
- next-step recommendation is provided.

## References
- Operating plan: `PLANS.md`
- Prompt schema: `knowledge/prompting/schema.md`
- Evaluation rubric: `knowledge/prompting/evaluation-rubric.md`
- Anti-patterns: `knowledge/prompting/anti-patterns.md`
- Build flow: `playbooks/build-system-prompt.md`
- Evaluation flow: `playbooks/evaluate-model.md`
