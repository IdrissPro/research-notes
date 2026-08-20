# Scalable Oversight

## Key ideas

Scalable oversight is the problem of supervising systems that may be better than the supervisor at the task being judged.

The core difficulty is an **asymmetry of competence**: generating a correct answer may require more expertise than the human has, while checking a convincing but subtly wrong answer may also require more expertise than the human has.

Possible approaches include:
- AI-assisted human evaluation,
- debate / adversarial critique,
- decomposition,
- recursive supervision,
- weak-to-strong generalization,
- selective escalation to experts.

A useful experimental trick is **sandwiching**:
1. choose tasks where an expert can establish ground truth,
2. hide that expertise from the simulated weak supervisor,
3. test whether an oversight method lets the weak supervisor approach expert-level judgment.

## Assumptions

- Current weak-vs-strong gaps are useful proxies for future human-vs-superhuman gaps.
- Ground truth is recoverable by an expert or stronger reference process.
- The oversight method does not merely leak the answer.
- Strong models do not systematically manipulate the evaluator.

## Failure modes / pitfalls

- **Assistance without verification:** the strong model gives the answer and the supervisor simply accepts it.
- **Persuasiveness bias:** eloquent wrong answers beat awkward correct ones.
- **Shared blind spots:** critic and answerer fail in the same way.
- **Weak-task proxy:** the benchmark is difficult for the weak judge for irrelevant reasons.
- **Judge manipulation:** agents optimize for what convinces the judge rather than what is true.
- **Ceiling effects:** the weak judge was already good enough.

## Proposed experiments (small)

1. **Weak judge / strong agent**
   - Use a weaker model as judge and stronger model as answerer.
   - Compare direct answering, critique, and debate.

2. **Hidden-ground-truth sandwich**
   - Pick questions with expert-verified answers.
   - Give the judge incomplete information.
   - Measure how much different assistance protocols recover.

3. **Persuasion stress test**
   - Construct correct-but-poorly-written and wrong-but-persuasive answers.
   - Test whether oversight tracks correctness or presentation.

4. **Supervisor scaling curve**
   - Evaluate the same protocol with judges of increasing capability.
   - Ask whether gains persist as the capability gap grows.

## Metrics & sanity checks

- Judge accuracy
- Improvement over unaided weak judge
- Gap to expert/reference accuracy
- False acceptance of incorrect answers
- Calibration
- Sensitivity to answer style
- Performance as the agent-judge gap increases

## Questions before trusting a scalable-oversight result

- Is the task hard for the judge for the right reason?
- Does the judge verify evidence, or just defer to the stronger model?
- What happens when the strong model is adversarial?
- Are agent and judge errors correlated?
- Does the method still help when the capability gap is larger?

## Sources

- Bowman et al. (2022), *Measuring Progress on Scalable Oversight for Large Language Models*  
  https://arxiv.org/abs/2211.03540
- Burns et al. (2023), *Weak-to-Strong Generalization*  
  https://arxiv.org/abs/2312.09390
