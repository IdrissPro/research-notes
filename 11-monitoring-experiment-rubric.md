# Rubric: Comparing Two Safety Monitors

Suppose monitor A and monitor B both output continuous suspiciousness scores.

The goal is not simply to ask which has the higher AUROC.

## Step 1 — Define the deployment decision

Examples:
- block the output,
- send to a stronger monitor,
- send to a human,
- rerun with a trusted model,
- allow the action.

This determines which errors matter.

## Step 2 — Keep the test set untouched

Use:
- train set for fitting,
- validation set for hyperparameters / layer / threshold,
- test set for the final comparison.

Do not repeatedly inspect test performance while designing the monitor.

## Step 3 — Compare full score distributions

Inspect:
- clean score distribution,
- harmful score distribution,
- hard-negative distribution,
- OOD harmful distribution.

A single threshold can hide important structure.

## Step 4 — Compare at equal operating points

Useful comparisons:
- TPR at the same FPR,
- FPR at the same TPR,
- detection at the same human-review budget,
- safety at the same usefulness.

This is more interpretable than comparing two arbitrary thresholds.

## Step 5 — Inspect disagreement

| Monitor A | Monitor B | Interpretation |
|---|---|---|
| correct | correct | easy/shared signal |
| correct | wrong | unique signal for A |
| wrong | correct | unique signal for B |
| wrong | wrong | shared blind spot |

Manually inspect disagreement examples.

This tells us whether combining the monitors is likely to help.

## Step 6 — Build the ensemble on validation data

Simple combination rules:
- max suspiciousness,
- weighted average,
- logistic regression over monitor scores,
- cascade: cheap monitor first, expensive monitor on uncertain cases.

Do not tune ensemble weights on the test set.

## Step 7 — Evaluate robustness separately

Repeat on:
- unseen attack families,
- benign hard negatives,
- paraphrases,
- longer contexts,
- different coding styles / domains,
- model updates if relevant.

## Step 8 — Report the Pareto frontier

For each threshold or audit budget:
- x-axis: cost / false positives / fraction escalated,
- y-axis: harmful cases caught / safety.

A monitor is clearly better when it improves the frontier, not merely one arbitrary operating point.

## Minimal reporting table

| Monitor | AUROC | AUPRC | TPR @ 1% FPR | TPR @ 5% FPR | OOD AUROC |
|---|---:|---:|---:|---:|---:|
| Behavioral | | | | | |
| Activation | | | | | |
| Combined | | | | | |

## Sanity checks

- Random-label probe should be near chance.
- Threshold is chosen before test evaluation.
- Hard negatives share superficial cues with harmful examples.
- OOD split is genuinely different.
- No duplicate or near-duplicate examples cross splits.
- Combined-monitor gain is not caused by test-set tuning.
