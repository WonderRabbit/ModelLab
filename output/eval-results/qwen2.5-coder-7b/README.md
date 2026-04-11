# 평가 결과: qwen2.5-coder-7b

## 상태
아직 로컬 평가 실행이 기록되지 않았다.

## 대상
- 모델: qwen2.5-coder-7b (잠정 대상)
- 기준 시스템 프롬프트: `prompts/system/qwen2.5-coder-7b-base.md`
- 평가 플레이북: `playbooks/evaluate-qwen2.5-coder-7b.md`

## 디렉터리 규칙
날짜 폴더를 생성한다.
- `output/eval-results/qwen2.5-coder-7b/YYYY-MM-DD/`

각 날짜 폴더 내부:
- `run-01.md`, `run-02.md`, ...
- `raw/` (무편집 원시 출력)
- 선택: `score-summary.md`

## 최소 실행 메타데이터
각 실행은 다음을 기록한다.
- 날짜/시간
- 런타임 스택(엔진, 양자화, 컨텍스트 설정)
- 프롬프트 변형 ID
- 작업 ID
- 루브릭 점수 + 짧은 근거
- 안정성 관찰

## 메모
현재 지식은 로컬 근거가 확보되기 전의 1차 추론/가설 중심이다.
