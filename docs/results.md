# Results

## Final locked GELU L20

The final model lock reports:

| Evaluation | PR-AUC | ROC-AUC |
|---|---:|---:|
| Validation | 0.152630 | 0.851712 |
| Test | 0.186282 | 0.851212 |

Validation was used for candidate selection. Test results are observational.

## V1 versus V3

A separate V1/V3 evidence summary reports:

| Model | Test PR-AUC | Test ROC-AUC |
|---|---:|---:|
| V1 | 0.061587 | 0.787951 |
| V3 | 0.134444 | 0.819771 |

This comparison belongs to a separate evidence lineage and is not the
final GELU L20 evaluation.

## Interpretation

- PR-AUC is reported alongside ROC-AUC because class imbalance makes
  precision-recall performance especially informative.
- Results are offline research evaluations.
- Stress results represent a separate evaluation population and are not
  interpreted as proof of generalization to all real-world settings.
- Metrics do not establish operational AML effectiveness.

Detailed selected artifacts are retained in `docs/evidence/`.
