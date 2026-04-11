# Prompt Optimization Evaluation Rubric

Use this rubric to evaluate model+prompt combinations consistently.

## Scoring scale
- 1 = poor / frequently fails
- 2 = weak / unstable
- 3 = acceptable baseline
- 4 = strong
- 5 = excellent / reliable

## Criteria

| Criterion | What to check | Score (1-5) | Notes |
|---|---|---:|---|
| Instruction following | Follows explicit directives and constraints |  |  |
| Format adherence | Meets required schema/headers/JSON validity |  |  |
| Reasoning quality | Produces sound decomposition and justified conclusions |  |  |
| Verbosity control | Matches requested length/detail level |  |  |
| Task fitness | Output usefulness for target task/domain |  |  |
| Cross-run consistency | Similar quality across repeated runs |  |  |
| Hallucination risk | Unsupported claims, fabricated details, overconfidence |  |  |
| Context handling quality | Correctly uses relevant context, ignores distractors |  |  |

## Run record template

```md
# Evaluation Run
- Date:
- Evaluator:
- Model:
- Prompt version:
- Task set:
- Context size/type:

## Scores
| Criterion | Score | Evidence |
|---|---:|---|
| Instruction following |  |  |
| Format adherence |  |  |
| Reasoning quality |  |  |
| Verbosity control |  |  |
| Task fitness |  |  |
| Cross-run consistency |  |  |
| Hallucination risk |  |  |
| Context handling quality |  |  |

## Stability assessment
- Stable / provisional / inconclusive:
- Why:

## Implications for prompt strategy
- Keep:
- Change:
- Test next:
```

## Interpretation bands
- **4.3+**: production candidate with minor hardening.
- **3.5-4.2**: workable with targeted patching.
- **2.5-3.4**: needs prompt redesign and tighter constraints.
- **<2.5**: poor fit for this task setup; reconsider model or approach.
