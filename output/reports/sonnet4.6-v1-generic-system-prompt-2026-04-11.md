# sonnet4.6 v1 범용 시스템 프롬프트 결과물 (2026-04-11)

## 1) 산출물 경로
- 프롬프트 자산: `prompts/system/sonnet4.6-base.md`
- 의사결정 기록: `knowledge/decisions/0002-sonnet4.6-system-prompt.md`

## 2) 네이밍 룰
- 규칙: `{model}-{ver}-{goal}-{date}.md`
- 필드 정의:
  - model: 대상 모델명 (예: sonnet4.6)
  - ver: 프롬프트 버전 태그 (예: v1)
  - goal: 산출물 목적 (예: generic-system-prompt)
  - date: 생성일 (YYYY-MM-DD)
- 예시: `sonnet4.6-v1-generic-system-prompt-2026-04-11.md`

## 3) 프롬프트 설계 요약
- 공통 스키마(역할/목표/제약/출력형식/스타일/모델패치)를 따르는 범용 템플릿으로 작성.
- 불확실성 라벨(evidence/inference/hypothesis)을 기본 규칙에 포함.
- 운영 시 재현성을 위해 기본 출력 순서를 고정.

## 4) 근거 수준
- evidence: 저장소의 프롬프트 스키마 및 운영 규칙 반영.
- inference: 고정 출력 구조는 리뷰/비교 효율을 높일 가능성이 큼.
- hypothesis: sonnet4.6에서 장문 드리프트 완화 효과는 평가 전 잠정.

## 5) 다음 단계
- 평가 플레이북 기준으로 샘플 태스크 10개를 실행해 형식 준수율을 측정.
- 실패 케이스를 수집해 `MODEL_PATCH_SONNET4.6`를 미세 조정.
