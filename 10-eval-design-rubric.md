# Rubric: Is This AI Safety Evaluation Actually Informative?

This is a checklist to use before taking an evaluation result seriously.

## 1. Threat model

- What failure are we trying to detect?
- Is the model merely unreliable, or intentionally adversarial?
- What does the model know about the evaluator?
- What counts as an unacceptable outcome?
- What resources, tools, memory, and context does the model have?

If the threat model is vague, the metric is hard to interpret.

## 2. Construct validity

Ask whether the benchmark measures the thing it claims to measure.

Examples:
- a "deception" dataset may really measure writing style,
- "jailbreak robustness" may measure keyword refusal,
- "evaluation awareness" may measure benchmark formatting,
- a "harmfulness probe" may measure topic.

Useful test:

> Name the simplest nuisance variable that could explain the result, then build a hard-negative set that contains that nuisance variable without the target property.

## 3. Baselines

At minimum compare against:
- trivial/base-rate predictor,
- simple heuristic,
- weaker model,
- strong behavioral baseline,
- random auditing where relevant.

A complicated method is not useful if a cheap baseline captures the same signal.

## 4. Data splitting

Avoid random splits when neighboring examples are near-duplicates.

Prefer splits by:
- task family,
- attack family,
- template,
- source dataset,
- participant,
- time,
- environment.

The split should reflect the generalization claim.

## 5. Distribution shift

Report both:
- in-distribution performance,
- out-of-distribution performance.

For safety monitoring, the second is often more important.

Useful stressors:
- paraphrases,
- unseen attack strategies,
- hard benign negatives,
- new domains,
- different model sizes,
- model updates / fine-tuning,
- adaptive attacks.

## 6. Operating point

AUROC is useful but deployment requires a threshold.

Report metrics such as:
- TPR at 1% FPR,
- precision at fixed review budget,
- escapes at fixed audit budget,
- usefulness at fixed safety level.

Thresholds must be selected on validation data, not the test set.

## 7. Adversarial adaptation

If the safety claim concerns strategic models:
- let the attacker know the defense,
- let it optimize against the monitor,
- evaluate unseen adaptive attacks.

A non-adaptive benchmark can substantially overstate robustness.

## 8. Error analysis

Manually inspect:
- false positives,
- false negatives,
- highest-confidence mistakes,
- examples where two monitors disagree.

Error overlap is especially important when evaluating ensembles.

## 9. Ablations

Useful ablations:
- remove CoT,
- remove activations,
- randomize labels,
- shuffle temporal order,
- remove suspicious keywords,
- swap model layer,
- reduce context,
- replace learned monitor with a heuristic.

## 10. Reproducibility

Record:
- model/version,
- prompt templates,
- decoding parameters,
- seeds,
- dataset construction,
- split logic,
- threshold-selection procedure,
- exact metric definitions.

## Minimal result table

| Setting | AUROC | TPR @ 1% FPR | FPR | Accuracy | Notes |
|---|---:|---:|---:|---:|---|
| In-distribution | | | | | |
| OOD attack family | | | | | |
| Hard negatives | | | | | |
| Adaptive attack | | | | | |

## One-sentence test

Before publishing a result, try to complete:

> "This experiment is evidence that **[method]** detects/prevents **[specific failure]** under **[specific threat model]**, including **[specific shift/adversary]**, at a cost of **[specific false-positive/audit/usefulness cost]**."

If that sentence is hard to write, the claim is probably still underspecified.
