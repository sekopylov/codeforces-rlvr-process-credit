# Evaluation log: value teachers and process-credit spans

This is a public summary of the saved June 2026 experiment records. It preserves the reported metrics while omitting internal storage locations, run identifiers, raw trajectories, and infrastructure logs.

## Public-prompt versus editorial-privileged value teacher

Both variants evaluated student-generated Codeforces trajectories and predicted final verifier labels at sampled prefixes. The public-prompt ablation used the same data, model, objective, and random-trajectory validation split but omitted editorial context. The validation view contained 136 balanced trajectories. It was a trajectory-level comparison; the report does not establish generalization to entirely unseen problems.

| Metric, optimizer step 512 | Public prompt | Editorial-privileged prompt |
| --- | ---: | ---: |
| Terminal threshold accuracy | 0.625 | 0.735 |
| Terminal pairwise AUC | 0.688 | 0.809 |
| Prefix binary cross-entropy (lower is better) | 0.675 | 0.614 |

These measurements support better *outcome prediction* with privileged context on this validation view. They do not show that value differences identify causally correct reasoning steps or improve student RLVR training.

## Manual trace audit

The report includes five selected step-512 fragments from Codeforces problems 1175C, 1473D, and 1660B. Several positive value changes coincided with useful algorithmic steps, including a radius/window pivot and a second-maximum condition. Other fragments showed delayed credit, coarse negative credit over mixed-quality reasoning, and useful local progress in a trajectory that ultimately failed. This was qualitative candidate inspection, not a blinded or representative accuracy estimate.

## Twenty-trajectory span-label audit

A separate manually labeled benchmark tested whether value traces could be converted into automatic labels for non-empty newline spans inside the model's reasoning section. Final-answer and code spans were excluded from the revised target. The audit used the saved privileged value-teacher traces at step 512.

- A delta-only heuristic reached approximately **0.256 micro precision** and **0.312 micro recall** in the initial evaluation.
- A level/draw heuristic reached approximately **0.304 micro precision** and **0.299 micro recall** at its best F1-style setting. A very strict setting found just **1 true-positive span out of 3,531 positives**.
- In the revised reasoning-only search, **748 tested configurations** reached neither the target macro precision of 0.95 nor the target macro recall of 0.60 together. The best useful precision/recall frontier was approximately **0.381 macro precision** at **0.616 macro recall**.

The benchmark is small and selected, so these figures should not be extrapolated to every Codeforces trajectory. They do establish that the tested value-only transformations were inadequate as a reliable automatic span-label gate in this setting. Value changes remain a soft diagnostic or candidate-selection feature.

## Interpretation

The result is mixed: editorial context helped predict final outcomes, while mapping those predictions to local semantic credit remained unsolved. The next useful test would compare candidate spans with independent annotations or counterfactual continuations, then evaluate any proposed signal in matched student RLVR runs.
