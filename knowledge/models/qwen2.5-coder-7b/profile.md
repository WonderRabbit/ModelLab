# Qwen2.5-Coder-7B Profile (First Pass)

## 1) Metadata
- Model name: Qwen2.5-Coder-7B-Instruct
- Provider: Qwen (Alibaba Cloud)
- Version/date: Qwen2.5-Coder release line (2024)
- Parameter/class: ~7B class instruct-tuned coding model (HF page reports 8B params display)
- Last updated: 2026-04-11
- Owner: Codex session
- Target status: **provisional target** (not yet confirmed as deployed local model)

## 2) Local-use assumptions (this run)
- Runtime assumption: local inference through llama.cpp/vLLM/Ollama-compatible stack. (`hypothesis`)
- Primary usage assumption: coding + technical analysis, with some general assistant use. (`inference`)
- Prompt sensitivity assumption: medium-high sensitivity to explicit format contracts for deterministic output. (`inference`)
- Resource assumption: fits on commodity single-GPU or quantized CPU/GPU mixed setups used for local experimentation. (`inference`)

## 3) Summary
Qwen2.5-Coder-7B-Instruct is selected as the **initial local Qwen target** because it is coding-oriented, widely distributed for local deployment, and likely to be a pragmatic first optimization target for system-prompt work. At this stage, repository-local behavioral evidence is not yet available, so practical guidance below is intentionally labeled as inference/hypothesis and should be validated via controlled evaluations. (`evidence`: target selection process in this repo; `inference`: behavioral expectations)

## 4) Strengths
- Likely strong baseline on code generation, code transformation, and code explanation compared with non-coder 7B peers. (`inference`)
- Good candidate for structured task execution when output schema is explicit. (`inference`)
- Broad local ecosystem support (quantizations/serving options) makes repeatable experiments practical. (`evidence`: public model distribution; `inference`: experimentation practicality)

### Prompt consequences
- **Essential ingredients:** explicit task goal, language/runtime target, acceptance checks, output schema.
- **Optional ingredients:** long persona framing, heavy stylistic constraints.
- **Avoid:** vague “improve this” prompts without objective criteria.

## 5) Weaknesses
- Potential drift on long multi-constraint prompts if constraints are buried. (`hypothesis`)
- Increased hallucination risk in factual/non-code domains without provided context. (`inference`)
- Possible over-verbosity when not given length/structure controls. (`hypothesis`)

### Prompt consequences
- Put non-negotiables near top, in bullets.
- Force uncertainty handling (“state assumptions / unknowns”).
- Cap response length or section count for routine tasks.

## 6) Instruction-following tendency
- Working assumption: **moderate-to-strong** when constraints are concise, ordered, and measurable. (`hypothesis`)
- Degrades when directives conflict or mix hard rules with preferences. (`inference`)

### System vs user split
- **System prompt:** stable global rules, tone, refusal/uncertainty behavior, default output contract.
- **User prompt:** task-specific schema details, language/toolchain constraints, edge-case emphasis.

## 7) Format adherence tendency
- Working assumption: better adherence with repeated schema reminders and exact headers/keys. (`hypothesis`)
- Risk: markdown/header drift in longer answers unless explicitly constrained. (`hypothesis`)

### Essential vs optional
- **Essential:** explicit schema, “return only X sections”, fallback behavior on missing info.
- **Optional:** few-shot examples (use when failures persist).

## 8) Verbosity tendency
- Likely defaults to medium-long explanatory style for coding questions. (`hypothesis`)
- Better control expected via direct budgets: “max N bullets”, “<= M lines per section”. (`inference`)

## 9) Reasoning behavior
- Likely useful decomposition for practical coding tasks; may still produce confident but brittle plans without verification instructions. (`inference`)
- Improves with checklist-style visible reasoning outputs (assumptions, plan, result, validation). (`inference`)

## 10) Context handling notes
- Large advertised context exists in model family documentation, but effective context utilization under local serving/quantization needs empirical validation. (`evidence` + `inference`)
- For first pass, treat context quality as capacity-constrained and prioritize relevance filtering. (`inference`)

## 11) Preferred prompt style
- Concise, rule-based, sectioned prompts are likely to outperform narrative prompts for reliability. (`inference`)
- TOC/outline scaffolding should help for complex analysis tasks. (`hypothesis`)

## 12) Recommended use cases
- **Good fit (first-pass):** code edits, refactors, test drafting, API usage examples, architecture tradeoff memos with bounded scope. (`inference`)
- **Acceptable with guardrails:** summarization of provided technical docs; structured extraction from user-provided text. (`inference`)
- **Weak/risky without retrieval:** open-ended factual research, policy/legal/medical advice. (`inference`)

## 13) Caution points
- Require explicit uncertainty protocol for factual claims.
- Reinforce that unsupported claims must be labeled.
- Keep system prompt compact to preserve task-context budget for local runs.

## 14) Prompt strategy implications (required)
- **System prompt implications:** keep compact, rule-forward, define deterministic sectioned output and unknown-handling.
- **User prompt implications:** repeat format contract and task acceptance criteria at request time.
- **Context/retrieval implications:** provide curated context snippets with source labels; avoid full dumps.
- **Output contract implications:** prefer markdown schemas or strict JSON with explicit keys and failure mode.

## 15) Confidence and evidence notes
- **Evidence:**
  - Repository contains no prior Qwen-specific findings (search over repo returned none).
  - Model card exists for Qwen2.5-Coder-7B-Instruct with broad public availability.
- **Inference:** model behavior expectations based on coder-model class behavior and prompt-engineering priors.
- **Hypothesis:** exact adherence/verbosity/context traits until local evaluation runs are completed.
- **Test references:** none yet; initialize in `output/eval-results/qwen2.5-coder-7b/`.
