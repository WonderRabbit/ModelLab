# Playbook: Evaluate Model

## Goal
Run repeatable evaluations for a target model and update reusable guidance.

## Inputs
- Target model
- Prompt version(s)
- Task set (at least 3 tasks)
- Evaluation rubric (`knowledge/prompting/evaluation-rubric.md`)

## Procedure
1. Define scope and hypotheses.
2. Execute tasks with controlled variations (same tasks, same format contract).
3. Run at least 3 repeated runs for consistency checks.
4. Score using rubric.
5. Save raw outputs in `output/evaluations/<model>/<date>/`.
6. Update model profile with evidence/inference/hypothesis labels.
7. Record major decisions in `knowledge/decisions/` if strategy changes.

## Required artifacts
- Evaluation run report (markdown)
- Score table
- Stability assessment
- Prompt strategy implications

## Exit criteria
- Rubric completed for all criteria
- Evidence paths linked
- Next experiment clearly defined
