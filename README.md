# research-notes

Short research notes on AI safety papers, blog posts, talks, and experiments.

These are not intended to be literature-review-quality summaries. The goal is to keep track of:
- the core claim,
- the threat model,
- assumptions,
- failure modes,
- experiments that would change my mind,
- useful evaluation metrics.

## Notes

### Evaluation & robustness

1. [Alignment Evaluation: What Are We Measuring?](01-alignment-evaluation.md)
2. [Truthfulness & Hallucination](02-truthfulness.md)
3. [Robustness & Distribution Shift](03-robustness-distribution-shift.md)

### AI control & oversight

4. [AI Control: Safety Under Intentional Subversion](04-ai-control.md)
5. [Scalable Oversight](05-scalable-oversight.md)
6. [Strategic Behavior & Evaluation Awareness](06-strategic-behavior-and-evaluation-awareness.md)
7. [Activation Monitoring & Linear Probes](07-activation-monitoring.md)
8. [Chain-of-Thought Monitoring](08-chain-of-thought-monitoring.md)
9. [Evaluator Gaming, Judge Hacking & Spot-Checking](09-evaluator-gaming-and-spot-checking.md)

### Research / evaluation rubrics

10. [Is This AI Safety Evaluation Actually Informative?](10-eval-design-rubric.md)
11. [Comparing Two Safety Monitors](11-monitoring-experiment-rubric.md)

### Templates

- [Research Note Template](NOTE_TEMPLATE.md)

## General principles

1. **Threat model before metric.** A high score is meaningless if it is unclear what failure it rules out.
2. **Average-case performance is not enough.** Test safety methods under distribution shift and, when relevant, adaptive pressure.
3. **Separate detection from mechanism.** Predicting a property from activations does not automatically show that the representation is causal.
4. **Compare at deployment-relevant operating points.** Thresholds, false positives, audit budgets, and usefulness matter.
5. **Look at disagreements and failures.** The most informative examples are often where monitors disagree or confidently fail.
6. **Ask what would falsify the claim.** Every note should end with an experiment that could materially reduce confidence in the result.
