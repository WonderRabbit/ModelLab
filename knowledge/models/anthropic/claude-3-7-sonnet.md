# Claude 3.7 Sonnet (레거시 메모)

상태: 레거시 모델 메모로 전환 (2026-04-11).

- [evidence] Anthropic 모델 폐기 문서에서 `claude-3-7-sonnet-20250219`는 deprecated로 표시되며, retirement date는 2026-02-19로 기재되어 있다.
  - 출처: https://platform.claude.com/docs/en/about-claude/model-deprecations
- [inference] 신규 워크로드 기본값으로는 Claude 3.7 Sonnet 대신 Claude Sonnet 4.6 채택이 바람직하다.
- [hypothesis] 기존 3.7 기반 프롬프트는 Sonnet 4.6 이관 시 출력 길이/형식 편차가 일부 발생할 수 있으므로 회귀 테스트가 필요하다.

연계 문서:
- `knowledge/models/anthropic/claude-opus-sonnet-research-2026-04.md`
