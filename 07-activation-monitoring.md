# Activation Monitoring & Linear Probes

## Key ideas

Behavioral monitoring only sees what the model exposes externally.

Activation monitoring instead reads internal hidden states and trains a lightweight classifier — often a linear probe — to detect a safety-relevant property.

Generic setup:

1. Run the model on labeled examples.
2. Extract hidden states from one or more layers/tokens.
3. Train a probe on frozen activations.
4. Produce a continuous suspiciousness score.
5. Choose an operating threshold based on the deployment trade-off.

Important distinction:
- **probe separability:** a concept is linearly predictable from activations,
- **causal representation:** the probed direction actually participates in producing the behavior.

High probe accuracy does **not** by itself establish a causal mechanism.

## What makes probes attractive

- Cheap relative to a second large monitor.
- Can expose information hidden from final outputs.
- Provide a continuous risk score.
- Can be combined with behavioral monitoring.
- Layer-wise analysis can show where signal becomes available.

## Failure modes / pitfalls

- **Spurious correlation:** probe learns topic, style, length, or prompt template.
- **Distribution shift:** strong in-domain AUROC collapses on new attack families.
- **Token leakage:** representations contain explicit textual evidence rather than hidden intent.
- **Layer cherry-picking:** selecting the best layer on the test set inflates results.
- **Class imbalance:** accuracy looks strong while rare harmful cases are missed.
- **Adaptive evasion:** a capable model may learn representations that avoid the monitor.
- **Non-causal probe:** classification succeeds without identifying a mechanism that controls behavior.

## Proposed experiments (small)

1. **Cross-domain transfer matrix**
   - Train on attack family A.
   - Test on A, B, C, and benign hard negatives.
   - Repeat for each training domain.

2. **Layer sweep**
   - Fit identical probes across layers.
   - Select the layer on validation data only.
   - Report the full layer curve.

3. **Hard-negative evaluation**
   - Add benign samples that share vocabulary/style with harmful samples.
   - Check whether performance survives.

4. **Behavior-vs-activation complementarity**
   - Compare errors made by an LLM monitor and activation probe.
   - Measure whether an ensemble improves the Pareto frontier.

5. **Causal follow-up**
   - Steer or ablate the detected direction.
   - Check whether the targeted behavior changes while unrelated capabilities remain stable.

## Metrics & sanity checks

- AUROC
- AUPRC
- TPR at fixed low FPR
- Calibration
- Cross-domain AUROC matrix
- Layer stability
- Performance on hard negatives
- Error overlap with behavioral monitor
- Safety/usefulness after thresholding

## Threshold selection

Do not choose the threshold on the test set.

A reasonable workflow:
1. train the probe on training data,
2. choose hyperparameters and layer on validation data,
3. choose a threshold using the deployment cost trade-off or a target FPR,
4. report final metrics once on untouched test data.

For rare catastrophic failures, **TPR at a very low FPR** can be more informative than accuracy at 0.5.

## Questions before trusting an activation monitor

- What nuisance variable could the probe be reading?
- Does it generalize to a genuinely new attack distribution?
- Does it still work on difficult benign negatives?
- How was the layer chosen?
- How was the threshold chosen?
- Does the probe add information beyond a text monitor?
- Can the monitored model adapt to evade it?

## Sources

- Goldowsky-Dill et al. (2025), *Detecting Strategic Deception Using Linear Probes*  
  https://arxiv.org/abs/2502.03407
- *Detecting High-Stakes Interactions with Activation Probes* (2025)  
  https://arxiv.org/abs/2506.10805
- *One Probe Won't Catch Them All* (2026)  
  https://arxiv.org/abs/2602.01425
