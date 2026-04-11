# Anthropic Claude Opus · Sonnet 리서치 (2026-04-11)

## 1) 리서치 범위
- 대상: Anthropic Claude 계열 중 **Opus**와 **Sonnet** 라인업.
- 목적: 운영 관점에서 모델 선택, 버전 고정 전략, 마이그레이션 리스크를 빠르게 판단할 수 있는 기초 지식 정리.
- 조사 시점: 2026-04-11 (UTC).

## 2) 관찰된 사실 (Evidence)
- [evidence] Anthropic 공식 모델 개요 문서 기준, 최신 비교 테이블에 **Claude Opus 4.6 / Claude Sonnet 4.6**가 표시되며, 두 모델 모두 Extended thinking을 지원한다. 또한 Opus 4.6은 최대 출력 128k, Sonnet 4.6은 최대 출력 64k로 제시된다.
  - 출처: https://platform.claude.com/docs/en/about-claude/models/overview
- [evidence] 같은 문서에서 컨텍스트 윈도는 Opus 4.6/ Sonnet 4.6 모두 **1M tokens**로 제시된다.
  - 출처: https://platform.claude.com/docs/en/about-claude/models/overview
- [evidence] Opus 소개 페이지에는 Opus 4.6 공지일이 **2026-02-05**로 기재되어 있으며, Claude Platform 및 Bedrock/Vertex/Foundry 사용 가능하다고 명시되어 있다.
  - 출처: https://www.anthropic.com/claude/opus
- [evidence] Sonnet 4.6 발표 글은 **2026-02-17** 게시이며, Sonnet 4.5 대비 코딩·지시 준수·컴퓨터 사용 성능 개선을 강조한다.
  - 출처: https://www.anthropic.com/news/claude-sonnet-4-6
- [evidence] Claude Code 모델 설정 문서에서 Opus 4.6/ Sonnet 4.6의 1M 컨텍스트 사용(예: `model[1m]`) 및 모델 alias(`opus`, `sonnet`)가 최신 버전으로 이동할 수 있음을 설명한다.
  - 출처: https://code.claude.com/docs/en/model-config
- [evidence] 모델 폐기(deprecation) 문서에는 `claude-3-7-sonnet-20250219`가 폐기(deprecated) 상태이며, 퇴역일이 **2026-02-19**로 기록되어 있다.
  - 출처: https://platform.claude.com/docs/en/about-claude/model-deprecations

## 3) 해석 (Inference)
- [inference] 2026-04-11 기준 신규 도입은 Sonnet 3.7이 아니라 **Sonnet 4.6**을 기본으로 삼는 것이 운영 리스크(퇴역/호환성) 측면에서 유리하다.
- [inference] 비용·지연시간·성능의 균형이 필요하면 Sonnet 4.6, 난도 높은 복합 과업(복잡한 에이전트 루프·대규모 코드베이스·고난도 추론)은 Opus 4.6 우선 전략이 합리적이다.
- [inference] `opus`/`sonnet` alias는 편하지만, 배포 안정성이 중요한 프로덕션은 버전 ID 고정(예: `claude-opus-4-6`, `claude-sonnet-4-6`)이 필요하다.

## 4) 잠정 가설 (Hypothesis)
- [hypothesis] 동일한 프롬프트 계약(출력 스키마·실패 시 재시도 정책) 하에서 Sonnet 4.6이 대부분의 일반 코딩 태스크에서 비용 대비 성능 우위를 보일 가능성이 높다.
- [hypothesis] Opus 4.6의 장점은 단발 정답률보다도, 장시간 다단계 작업에서의 누적 오류 억제(재계획·자기 수정)에서 더 크게 나타날 가능성이 있다.

## 5) 운영 의사결정 초안
- 기본 모델: `claude-sonnet-4-6`
- 고난도 승격 모델: `claude-opus-4-6`
- 프로덕션 원칙: alias 대신 버전 ID 고정, 분기별 모델 재평가.
- 컨텍스트 정책: 200k 기본, 장문 레포/장기 세션에서만 1M 확장 사용.

## 6) 알려진 한계
- 본 문서는 공식 문서 기반의 1차 조사이며, 우리 저장소 태스크셋에 대한 실측 벤치마크는 아직 수행하지 않았다.
- 벤더 발표 성능은 실서비스 데이터/도메인 분포에 따라 재현되지 않을 수 있다.

## 7) 다음 단계 권고
1. `playbooks/evaluate-model.md` 기반으로 Opus 4.6 / Sonnet 4.6 동일 과제 A/B 평가를 수행한다.
2. 결과를 `output/eval-results/anthropic-opus-vs-sonnet-2026-04/`에 저장한다.
3. 평가 결과를 반영해 `knowledge/decisions/`에 모델 라우팅 정책(기본·승격·폴백) 결정을 기록한다.
