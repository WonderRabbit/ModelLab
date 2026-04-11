# 저장소 구조 제안

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

## 유지보수 가능한 이유
- 산출물 유형별 명확한 분리는 드리프트와 중복을 줄인다.
- 플레이북은 반복 가능한 워크플로를 강제한다.
- 스키마 + 루브릭은 공통 품질 언어를 제공한다.
- 모델 프로필은 연구 결과를 프롬프트로 표준 전환한다.
