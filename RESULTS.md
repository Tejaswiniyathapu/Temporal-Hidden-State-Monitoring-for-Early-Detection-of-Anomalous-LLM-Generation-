# Results

## Feature Ablation Results

The model was evaluated using group-aware 5-fold cross-validation.

| Feature Configuration | Mean ROC-AUC |
|---|---:|
| Trajectory-only | 0.7700 |
| Uncertainty-only | 0.6030 |
| All features | 0.7500 |

The trajectory-only features performed better than the uncertainty-only
and all-feature configurations in the controlled experiment.

## Checkpoint-wise Results

The trajectory-based detector was evaluated at different generation
checkpoints.

| Checkpoint | Tokens Seen | Tokens Remaining | Mean ROC-AUC |
|---|---:|---:|---:|
| 25% | 8 | 23 | 0.9095 |
| 50% | 16 | 15 | 0.7625 |
| 75% | 24 | 7 | 0.7090 |
| 100% | 31 | 0 | 0.7030 |

## Key Finding

The best early detection performance was obtained at the 25% checkpoint,
with a mean ROC-AUC of 0.9095.

This indicates that useful information may be present in the temporal
hidden-state trajectory early during generation.
