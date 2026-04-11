# User Prompt Reinforcement Patterns: qwen2.5-coder-7b

Use these patterns with `prompts/system/qwen2.5-coder-7b-base.md`.

## 1) Coding task pattern
```md
Task: <what to build/fix>
Language/stack: <lang, framework, versions>
Constraints:
- <hard rule 1>
- <hard rule 2>
Output format (required): Summary, Assumptions, Solution, Validation, Next Step.
Validation requirement:
- Provide exact commands/tests I should run.
Context:
<code snippet or file summary>
```

## 2) Architecture / design analysis pattern
```md
Analyze this design decision: <decision>
Options:
- A: ...
- B: ...
Decision criteria:
- <latency>
- <complexity>
- <operational risk>
Output format (required):
1) Summary
2) Assumptions
3) Option comparison table
4) Recommendation
5) Risks and mitigations
6) Next step
Keep to <= 250 words.
```

## 3) Summarization pattern
```md
Summarize the following text for <audience>.
Must include:
- 5 bullet key points
- 3 open questions
- Confidence tag per point: evidence/inference/hypothesis
Output format (required): Summary, Assumptions, Solution, Validation, Next Step.
Text:
<insert text>
```

## 4) Structured output request pattern
```md
Return JSON only.
Schema (exact keys, no extras):
{
  "summary": "string",
  "assumptions": ["string"],
  "actions": ["string"],
  "risks": ["string"],
  "next_step": "string"
}
Task:
<task>
Context:
<context>
```

## 5) Iterative refinement pattern
```md
Revision round: <n>
Keep unchanged:
- <constraint(s)>
Change requested:
- <specific adjustment>
Failure seen in prior answer:
- <format drift / missing detail / wrong assumption>
Output format (required): Summary, Assumptions, Solution, Validation, Next Step.
```

## Reinforcement notes
- Repeat schema requirements in user prompts for critical outputs.
- Prefer concrete constraints over stylistic requests.
- If output drifts, tighten: section order + word budget + “no extra sections”.
