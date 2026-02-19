# Robustness & Distribution Shift

## Key ideas
Robustness in aligned behavior means:
- Stable helpfulness and safety across:
  - paraphrases
  - formatting changes
  - multilingual / code-mixed inputs
  - noisy inputs (typos, ASR artifacts)
  - different user personas

Distribution shift matters because real users ≠ benchmark prompts.

## Assumptions
- Shifts can be simulated with transformations (paraphrase, noise, translation).
- "Robustness" is measurable without full real-world deployment.

## Failure modes / pitfalls
- **Fragile refusal boundaries:** small changes flip safe/unsafe decisions.
- **Spurious cues:** model keys on keywords rather than intent.
- **Adversarial style transfer:** policy evasion via roleplay/fiction wrappers.

## Proposed experiments (small)
1. **Transformation suite**
   - For a query set, apply transformations:
     - paraphrase, typo noise, indirect request, roleplay wrapper
   - Measure deltas in safety outcomes.
2. **Keyword dependence test**
   - Remove/replace "trigger words" while keeping intent.
   - Detect reliance on surface cues.
3. **Cross-lingual robustness**
   - Translate queries (FR/EN) and compare safety decisions.

## Metrics & sanity checks
- Robust accuracy: min accuracy across transformations
- Safety stability: % unchanged safety classification
- Worst-case performance (not just average)
