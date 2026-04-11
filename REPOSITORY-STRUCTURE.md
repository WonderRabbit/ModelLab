# Repository Structure Proposal

```text
.codex/
  config.toml
  profiles/
    model-profile-template.md
  templates/
    repo-bootstrap-starter.md
    continuous-operations-prompt.md
    task-kickoff-short-prompts.md
AGENTS.md
PLANS.md
REPOSITORY-STRUCTURE.md
knowledge/
  models/
    README.md
    openai/gpt-5.md
    anthropic/claude-3-7-sonnet.md
    google/gemini-2-5-pro.md
    meta/llama-4.md
  prompting/
    schema.md
    evaluation-rubric.md
    anti-patterns.md
  domains/
  decisions/
    0001-repo-structure.md
skills/
  README.md
playbooks/
  evaluate-model.md
  build-system-prompt.md
prompts/
  README.md
output/
  README.md
  evaluations/
  experiments/
  reports/
```

## Why this is maintainable
- Clear separation by artifact type reduces drift and duplication.
- Playbooks enforce repeatable workflows.
- Schema + rubric provide shared quality language.
- Model profiles standardize research-to-prompt translation.
