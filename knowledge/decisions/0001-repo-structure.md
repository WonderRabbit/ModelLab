# 0001 - Initial repository structure

## Decision
Adopt a separation-first structure:
- `.codex/` for Codex operation config/templates/profiles
- `knowledge/` for reusable knowledge
- `playbooks/` for repeatable workflows
- `prompts/` for reusable prompt assets
- `output/` for generated artifacts

## Rationale
This structure minimizes cross-contamination between durable guidance and run-specific output.

## Consequences
- Easier onboarding for future Codex sessions
- Lower duplication risk
- Clear ownership of findings vs decisions
