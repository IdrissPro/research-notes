# Strategic Behavior & Evaluation Awareness

## Key ideas

Standard evaluations often assume that if a model behaves safely during evaluation, this is evidence that it will behave safely during deployment.

Strategic models can break this assumption.

Relevant behaviors include:
- **sandbagging:** intentionally underperforming,
- **alignment faking:** appearing compliant when oversight is present,
- **sleeper behavior:** remaining benign until a trigger or deployment condition appears,
- **evaluation awareness:** distinguishing evaluation-like contexts from deployment-like contexts.

The key issue is not only whether a model *can* behave badly, but whether it can **condition that behavior on when it expects to be observed**.

## Assumptions

- Evaluation and deployment contexts contain distinguishable cues.
- The model has enough situational information to condition behavior on those cues.
- Behavioral differences can be separated from ordinary distribution shift.

## Failure modes / pitfalls

- **Obvious triggers:** toy backdoors may exaggerate how easy strategic behavior is to detect.
- **Prompt leakage:** probes may detect formatting artifacts rather than evaluation awareness.
- **Behavior-only blindness:** identical outputs can come from different internal strategies.
- **Researcher hindsight:** after finding a failure, it is easy to tell a story that was not predicted in advance.

## Proposed experiments (small)

1. **Evaluation-vs-deployment classifier**
   - Build matched evaluation-like and deployment-like prompts.
   - Probe outputs and internal activations.
   - Test on independently written prompt sets.

2. **Cue ablation**
   - Remove obvious words such as "test", "benchmark", and "deployment".
   - Check whether the signal persists.

3. **Counterfactual context**
   - Keep the task identical but change whether the model believes it is monitored.
   - Measure behavioral differences.

4. **Hidden-trigger generalization**
   - Construct a simple conditional policy.
   - Test whether detectors generalize to unseen trigger families.

## Metrics & sanity checks

- Behavior gap across contexts
- AUROC for evaluation-awareness probes
- Cross-dataset generalization
- Performance after cue removal
- False positives on ordinary domain shifts
- Detection at low false-positive operating points

## Questions before trusting the result

- Is the model detecting "evaluation" or merely benchmark style?
- Would the signal survive paraphrasing and format changes?
- Is there evidence of strategic conditioning rather than ordinary context sensitivity?
- Can the detector generalize to new environments?

## Sources

- Hubinger et al. (2024), *Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training*  
  https://arxiv.org/abs/2401.05566
- *Probing and Steering Evaluation Awareness of Language Models* (2025)  
  https://arxiv.org/abs/2507.01786
