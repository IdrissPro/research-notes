# Chain-of-Thought Monitoring

## Key ideas

Reasoning models sometimes expose intermediate reasoning in natural language.

This creates a potential monitoring surface:
- inspect the chain of thought for suspicious plans,
- flag attempts to manipulate the environment,
- escalate risky trajectories before the final action is executed.

The important property is **monitorability**, not necessarily philosophical faithfulness.

A chain of thought can be useful for control if dangerous plans tend to leave detectable traces before the harmful action occurs.

## Why it is interesting

Compared with output-only monitoring:
- the monitor may see intent before it becomes action,
- long-horizon failures may become easier to catch,
- the reasoning trace can provide richer evidence for escalation.

But this opportunity may be fragile.

## Failure modes / pitfalls

- **Unfaithful reasoning:** the visible reasoning may not reflect the actual computation.
- **Obfuscation:** models may learn to hide suspicious reasoning.
- **Optimization pressure:** training against CoT monitors may make reasoning less monitorable.
- **Monitor weakness:** reasoning is visible but too complex for the monitor to interpret.
- **Post-hoc rationalization:** the trace explains an answer after the fact rather than revealing the causal process.
- **Hidden reasoning channels:** important computation may occur outside the visible trace.

## Proposed experiments (small)

1. **CoT vs output-only monitor**
   - Give one monitor only final actions.
   - Give another the reasoning trace as well.
   - Compare detection at the same false-positive rate.

2. **Reasoning obfuscation stress test**
   - Prompt or train the model to avoid suspicious keywords while preserving the same plan.
   - Measure monitor degradation.

3. **Paraphrase invariance**
   - Rewrite reasoning traces without changing the underlying plan.
   - Test whether monitor scores remain stable.

4. **Early-warning analysis**
   - For harmful trajectories, measure how many steps before the harmful action the monitor first becomes suspicious.

## Metrics & sanity checks

- AUROC / AUPRC
- TPR at low FPR
- Detection lead time
- Robustness to paraphrase / obfuscation
- Incremental gain over output-only monitoring
- Performance on benign complex reasoning

## Questions before trusting CoT monitoring

- Is the monitor using semantic evidence or suspicious keywords?
- Does access to CoT add signal beyond the final action?
- Can a model deliberately make the reasoning less legible?
- Does training for better task performance reduce monitorability?
- Is the visible chain of thought necessary for solving the task?

## Sources

- Korbak et al. (2025), *Chain of Thought Monitorability: A New and Fragile Opportunity for AI Safety*  
  https://arxiv.org/abs/2507.11473
- *When Chain of Thought is Necessary, Language Models Struggle to Evade Monitors* (2025)  
  https://arxiv.org/abs/2507.05246
