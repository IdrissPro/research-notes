# Alignment Evaluation: What Are We Measuring?

## Key ideas
Alignment evaluation is not one thing. "Good behavior" decomposes into:
- **Capability** (can the model do X?)
- **Intent / objectives** (does it *try* to do X?)
- **Reliability** (does it do X across contexts, prompts, and distributions?)
- **Constraint adherence** (policy / safety constraints)
- **Calibration & uncertainty** (does it know when it doesn't know?)

A practical evaluation suite should separate:
- **Task performance** vs **safety performance**
- **In-distribution** vs **out-of-distribution**
- **Benign** vs **adversarial** interaction

## Assumptions
- We can define a proxy for "aligned" behavior (often multi-objective).
- Benchmark tasks approximate real-world use.
- Evaluation prompts represent realistic and adversarial conditions.

## Failure modes / pitfalls
- **Goodharting:** optimizing the metric breaks what you care about.
- **Contamination:** model saw the benchmark (or similar) in pretraining.
- **Evaluator bias:** LLM-as-a-judge correlates with style, not truth.
- **Prompt brittleness:** evaluation changes drastically with formatting.
- **Over-refusal:** looks safe but becomes useless.

## Proposed experiments (small)
1. **Prompt sensitivity audit**
   - Take 100 queries; create 5 paraphrases each.
   - Measure variance in: correctness, refusal, safety compliance.
2. **Policy vs helpfulness frontier**
   - Create mixed queries (safe + unsafe requests).
   - Plot helpfulness score vs refusal/unsafe rate under different system prompts.
3. **Adversarial distribution shift**
   - Evaluate on clean prompts vs "noisy" prompts (typos, dialect, indirect requests).

## Metrics & sanity checks
- Agreement between human labels and automatic judge
- Variance across paraphrases (robustness)
- False refusal rate vs unsafe compliance rate
- Calibration checks (confidence vs accuracy)
