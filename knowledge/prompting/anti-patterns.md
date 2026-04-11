# Prompting Anti-Patterns

## 1) Goal ambiguity
- Symptom: broad answers, missed intent.
- Fix: define explicit success criteria and boundaries.

## 2) Constraint burial
- Symptom: important rules ignored.
- Fix: place non-negotiables near top in bullet form.

## 3) Overloaded context dump
- Symptom: model latches onto irrelevant details.
- Fix: curate context and annotate relevance.

## 4) Output contract vagueness
- Symptom: formatting drift, inconsistent structure.
- Fix: provide schema/header contract and examples.

## 5) Mixing policy and preference
- Symptom: hard rules treated as optional style.
- Fix: separate mandatory constraints from style guidance.

## 6) No uncertainty protocol
- Symptom: confident hallucinations.
- Fix: require assumption labeling and evidence grading.

## 7) One-shot overfitting
- Symptom: prompt works once but not across tasks.
- Fix: evaluate across varied tasks and repeated runs.

## 8) Model-agnostic stubbornness
- Symptom: same prompt underperforms on specific models.
- Fix: keep common core + model patch strategy.

## 9) Excessive verbosity instructions
- Symptom: bloated responses, hidden errors.
- Fix: set tight length budget and structure.

## 10) Missing handoff artifacts
- Symptom: future sessions cannot continue work.
- Fix: store results in `knowledge/`, `output/`, and `decisions/` systematically.
