# AI Control: Safety Under Intentional Subversion

## Key ideas

AI control asks a different question from ordinary alignment evaluation:

> Can we use a capable model safely even if it is actively trying to cause an unacceptable outcome?

A control protocol usually combines:
- an **untrusted model** that is useful but may be adversarial,
- weaker or more trusted monitors,
- limited human auditing,
- escalation, editing, blocking, or replacement rules.

The important object is the **whole protocol**, not just the monitor.

Useful distinction:
- **Safety:** probability the protocol avoids catastrophe under an adversarial strategy.
- **Usefulness:** how much task performance we retain relative to using the capable model freely.

## Assumptions

- We can specify a concrete unacceptable outcome.
- We can construct a red-team strategy that meaningfully approximates intentional subversion.
- Trusted components are actually trusted enough for the threat model.
- Audit budgets and deployment constraints are realistic.

## Failure modes / pitfalls

- **Weak red team:** the protocol looks safe only because the attack is bad.
- **Monitor overfitting:** suspiciousness works on known attacks but not new ones.
- **Collusion:** multiple untrusted components may coordinate.
- **Audit-budget mismatch:** a protocol is safe only with unrealistically frequent review.
- **Distribution shift:** deployment attacks differ from attacks used in the control evaluation.
- **Safety through uselessness:** the protocol blocks so much work that it is safe but not useful.

## Proposed experiments (small)

1. **Trusted-monitor baseline**
   - Generate clean and backdoored outputs.
   - Score both with a weaker trusted model.
   - Sweep the suspiciousness threshold.
   - Plot safety vs usefulness.

2. **Adaptive attack evaluation**
   - Give the attacker information about the monitor.
   - Compare against attacks designed without monitor knowledge.
   - Measure how much safety degrades.

3. **Audit-budget sweep**
   - Vary the fraction of cases that can receive expensive review.
   - Compare random auditing vs suspiciousness-based auditing.

4. **Monitor complementarity**
   - Compare behavioral, activation-based, and combined monitors.
   - Ask whether the combination catches genuinely different failures.

## Metrics & sanity checks

- Attack success / escape rate
- False-positive rate on clean behavior
- Usefulness retained
- Safety-usefulness frontier
- Performance under unseen attack strategies
- Safety as a function of audit budget

## Questions before trusting a control result

- What exactly is the attacker allowed to know?
- How strong is the red team relative to the blue team?
- Would a stronger model discover a qualitatively different strategy?
- Does the protocol still work when the attack distribution changes?
- Are results driven by one easy-to-detect attack family?

## Sources

- Greenblatt et al. (2024), *AI Control: Improving Safety Despite Intentional Subversion*  
  https://arxiv.org/abs/2312.06942
- Mallen et al. (2025), *Subversion Strategy Eval*  
  https://arxiv.org/abs/2412.12480
