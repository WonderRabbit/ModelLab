# 사용자 프롬프트 강화 패턴: qwen2.5-coder-7b

이 패턴은 `prompts/system/qwen2.5-coder-7b-base.md`와 함께 사용한다.

## 1) 코딩 작업 패턴
```md
작업: <무엇을 만들거나 고칠지>
언어/스택: <언어, 프레임워크, 버전>
제약:
- <하드 규칙 1>
- <하드 규칙 2>
출력 형식(필수): Summary, Assumptions, Solution, Validation, Next Step.
검증 요구사항:
- 실행해야 할 정확한 명령/테스트를 제시.
컨텍스트:
<코드 스니펫 또는 파일 요약>
```

## 2) 아키텍처 / 설계 분석 패턴
```md
다음 설계 결정을 분석하라: <결정>
선택지:
- A: ...
- B: ...
결정 기준:
- <지연시간>
- <복잡도>
- <운영 리스크>
출력 형식(필수):
1) Summary
2) Assumptions
3) 선택지 비교 표
4) 권고안
5) 위험 및 완화책
6) 다음 단계
250단어 이하로 작성.
```

## 3) 요약 패턴
```md
다음 텍스트를 <독자>용으로 요약하라.
반드시 포함:
- 핵심 포인트 5개 글머리표
- 열린 질문 3개
- 포인트별 신뢰 태그: evidence/inference/hypothesis
출력 형식(필수): Summary, Assumptions, Solution, Validation, Next Step.
텍스트:
<텍스트 삽입>
```

## 4) 구조화 출력 요청 패턴
```md
JSON만 반환하라.
스키마(정확한 키만, 추가 금지):
{
  "summary": "string",
  "assumptions": ["string"],
  "actions": ["string"],
  "risks": ["string"],
  "next_step": "string"
}
작업:
<작업>
컨텍스트:
<컨텍스트>
```

## 5) 반복 개선 패턴
```md
수정 라운드: <n>
변경하지 말 것:
- <제약>
변경 요청:
- <구체 조정사항>
이전 답변의 실패:
- <형식 이탈 / 세부 누락 / 잘못된 가정>
출력 형식(필수): Summary, Assumptions, Solution, Validation, Next Step.
```

## 강화 메모
- 중요 출력은 사용자 프롬프트에서 스키마 요구를 반복한다.
- 문체 요청보다 구체 제약을 우선한다.
- 출력이 이탈하면 섹션 순서 + 단어 예산 + “추가 섹션 금지”를 강화한다.
