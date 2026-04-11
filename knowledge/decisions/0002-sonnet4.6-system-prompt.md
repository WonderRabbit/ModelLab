# 0002 - sonnet4.6 범용 시스템 프롬프트 및 출력 네이밍 규칙

## 의사결정
1. `prompts/system/sonnet4.6-base.md`를 범용 기본 시스템 프롬프트(v1.0, 잠정)로 추가한다.
2. output 산출물 파일명 규칙을 다음으로 고정한다.
   - `{model}-{ver}-{goal}-{date}.md`
   - 예: `sonnet4.6-v1-generic-system-prompt-2026-04-11.md`

## 근거 수준
- evidence:
  - 저장소 운영 규칙상 산출물은 `output/`에 저장해야 하며, 재사용 가능한 자산은 `prompts/`에 분리해야 한다.
  - 프롬프트 구성은 `knowledge/prompting/schema.md`의 표준 레이아웃을 따른다.
- inference:
  - 모델/버전/목표/날짜를 포함한 파일명은 추적성과 비교 실험 관리에 유리하다.
- hypothesis:
  - 본 규칙이 장기적으로 중복 파일 생성을 줄일 것으로 예상되나, 2주 이상 운영 데이터로 재검증이 필요하다.

## 결과
- 모델별 프롬프트 확장 시 일관된 베이스라인을 확보한다.
- 출력 파일 검색(모델, 목표, 날짜 필터)이 쉬워진다.

## 다음 단계 권고
- `playbooks/evaluate-model.md` 흐름으로 sonnet4.6 프롬프트의 준수율/형식 안정성 평가를 수행한다.
- 평가 결과를 `output/evaluations/`에 저장하고, 필요 시 v1.1 패치를 만든다.
