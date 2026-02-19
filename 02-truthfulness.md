# Truthfulness & Hallucination: Measuring "Saying True Things"

## Key ideas
Truthfulness is not just "factual accuracy":
- **Factuality:** statements match reality
- **Faithfulness:** statements match *sources provided* (in RAG)
- **Epistemic humility:** admits uncertainty; avoids inventing specifics
- **Attribution quality:** cites the right evidence for the right claim

Useful decomposition:
- Retrieval errors (no evidence)
- Reasoning errors (evidence misused)
- Generation errors (confident fabrication)

## Assumptions
- Ground truth exists or can be approximated (via references / datasets).
- We can label claims at a reasonable granularity (claim-level vs answer-level).

## Failure modes / pitfalls
- **Overconfidence:** correct tone, wrong content.
- **Truthiness:** plausible but unverified details.
- **Hidden multi-claim answers:** one wrong claim ruins the whole answer.
- **Cite laundering:** citations that look legit but don't support claims.

## Proposed experiments (small)
1. **Claim-level scoring**
   - For each answer, extract 3–8 atomic claims.
   - Label each as supported/unsupported/unknown given references.
2. **Uncertainty prompting**
   - Compare baseline vs "If unsure, say so" system instruction.
   - Track accuracy and abstention rates.
3. **Adversarial fact traps**
   - Ask questions with subtle false premises.
   - Measure: does the model correct the premise?

## Metrics & sanity checks
- Claim precision (% supported claims)
- Unsupported-citation rate
- Abstention calibration (abstains more on harder questions)
- Premise correction rate
