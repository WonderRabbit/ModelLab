# 0004. OpenCode에서 Qwen Code 활용전략 v1.1 채택

- 상태: 승인(초안 v1.0 → 운영 v1.1 보정)
- 작성일: 2026-04-29
- 범위: OpenCode + Ollama/Msty + Continue + MCP + 검증 파이프라인

## 1) 의사결정(Decision)

- `Claude 문서`는 **v1.0 초안으로 채택**한다.
- 팀 운영 표준은 **v1.1 보정본**을 사용한다.
- 반영 비율:
  - 채택 80%
  - 수정 15%
  - 추가 5%

## 2) 규칙(Rules)

### 2.1 모델 운용 규칙
- 작은 모델의 역할은 `분석가`가 아니라 `evidence summarizer`로 한정한다.
- 출력은 반드시 `VERIFIED / INFERRED / UNKNOWN / RISK`를 분리한다.
- 증거 미존재 시 `UNKNOWN`, 동적 SAP RFC는 `UNKNOWN_DYNAMIC`을 강제한다.
- 긴 컨텍스트 확장보다 evidence bundle 축소를 우선한다.

### 2.2 파라미터 규칙(Ollama)
- 기본값(채택):
  - `temperature=0`
  - `top_p=1.0`
  - `top_k=40`
  - `repeat_penalty=1.08`
  - `repeat_last_n=256` (v1.1 신규 필수)
  - `num_ctx=32768`
  - `num_predict=800~1200`
  - `stop="### END"`

### 2.3 `/no_think` 규칙 개정
- 기존: `Qwen3-Coder 필수`
- 개정: `Qwen 계열 혼용 시 안전장치`
- 해설: Qwen3-Coder-30B-A3B는 non-thinking only 특성을 가지므로 기능상 필수 제어가 아니라 안전장치로 취급한다.

### 2.4 Modelfile `FROM` 규칙
- 예시 태그를 그대로 복사하지 않는다.
- 반드시 `ollama list`와 `ollama show --modelfile <모델명>`로 실모델 태그/경로를 확인한다.
- 허용 형태:
  - `FROM <실제 등록 모델명:태그>`
  - `FROM ./<GGUF 파일 경로>`

### 2.5 Continue 규칙
- `context.provider: codebase`는 운영 표준에서 제거한다.
- `file/code/diff` + 사내 scanner/MCP/evidence bundle 중심으로 운용한다.
- `mcpServers`를 명시한다(최소 `repo-facts`, `claim-verifier`).

### 2.6 OpenCode 규칙
- Msty endpoint(`http://localhost:10000/v1`)는 환경 의존 옵션으로 주석과 함께 사용한다.
- 직접 Ollama 사용 시 provider/baseURL을 별도 검증한다.
- permission은 wildcard 기반이므로 `opencode debug config`로 실제 tool 매칭을 검증한다.

### 2.7 MCP 최소 셋 규칙
- 초기 활성 서버는 3개만 권장:
  1. `repo_facts`
  2. `repo_ast`
  3. `claim_verifier`
- 외부 지식형 MCP(GitHub/Jira/Confluence)는 초기 비활성 권장.
- 출력 제한:
  - `search_exact.max_results <= 20`
  - `read_range.max_lines <= 150`
  - 전체 파일 read 금지
  - 제외 경로: `node_modules/build/target/.git`
  - 비밀파일 제외: `secret/.env/pem/key`

### 2.8 검증 규칙(verifier)
- `verify-claims.sh` 단독 운영을 중단하고 Python verifier를 표준으로 승격한다.
- 필수 검증:
  1. report의 `file:line` citation 파싱
  2. 파일 존재/라인 범위 유효성
  3. claim symbol의 범위 내 실존 여부
  4. class.method 동파일 근접 검증
  5. RFC literal/config/enum/dynamic 분류
  6. UNKNOWN_DYNAMIC 정책 위반 탐지
  7. `L0/L1/L2/L3` 등급 출력

### 2.9 ast-grep 규칙 개정
- 기존: `정밀 추출`
- 개정: `후보 추출`
- 판정 기준:
  - `rg` → L1 candidate
  - `ast-grep` → L1~L2 candidate
  - `verifier 통과` → L2 verified
  - `runtime trace` → L3 verified

## 3) 지식(Knowledge)

### 3.1 v1.1 Modelfile 기준
```modelfile
# 실제 환경에 맞게 교체
FROM qwen3-coder-30b-a3b-q5:latest
PARAMETER temperature 0
PARAMETER top_p 1.0
PARAMETER top_k 40
PARAMETER min_p 0.0
PARAMETER repeat_penalty 1.08
PARAMETER repeat_last_n 256
PARAMETER num_ctx 32768
PARAMETER num_predict 1000
PARAMETER stop "### END"
PARAMETER stop "<|im_end|>"
PARAMETER stop "<|endoftext|>"
```

### 3.2 Continue 기준
- `provider: ollama`
- analyzer/explorer/autocomplete/embed 모델 분리
- `context: file, code, diff`
- `mcpServers` 명시

### 3.3 OpenCode 기준
- project root `opencode.json` 우선
- `permission`: allow/ask/deny 정책 + tool name 실검증
- `mcp`: `repo_facts/repo_ast/claim_verifier` 구성

## 4) 근거 수준(Evidence / Inference / Hypothesis)

- `evidence`: 요청 본문에서 제시된 운영 보정안(모델 파라미터, MCP 보강, verifier 강화, codebase provider 제거, endpoint 환경의존성)이 상호 일관됨.
- `inference`: v1.0 유지 + v1.1 보정 방식이 운영 리스크와 변경비용을 동시에 줄이는 타협안으로 적절함.
- `hypothesis`: repo별 언어/프레임워크 다양성이 높을수록 Python verifier의 정적 규칙은 추가 보강이 필요할 수 있음.

## 5) 실행 체크리스트(운영 반영용)

- [ ] `/no_think 필수` 문구를 `안전장치`로 수정
- [ ] Modelfile `FROM`을 실제 Ollama tag/GGUF로 교체
- [ ] `repeat_last_n 256` 추가
- [ ] Continue `provider: codebase` 제거
- [ ] Continue `mcpServers` 추가
- [ ] OpenCode `mcp` 섹션 추가
- [ ] Msty OpenAI-compatible endpoint 활성 여부 확인
- [ ] `opencode debug config`로 permission 매칭 검증
- [ ] `verify-claims.sh` → Python verifier 전환
- [ ] ast-grep를 `후보 추출`로 명시
- [ ] Golden Set 결과를 `.ai/eval/results.md`에 저장

## 6) 다음 단계 권고

1. `.ai/rules/grounded-analysis.md`를 v1.1 규칙에 맞춰 동기화.
2. `.ai/scripts/verify_claims.py`를 저장소 표준 스크립트로 추가.
3. Golden Set 자동채점 파이프라인(CI 또는 로컬 태스크) 연결.
