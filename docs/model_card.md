# Model Card — TraceGuard Behavioural Transformer

## Model identity

- Model: TraceGuard Behavioural Transformer V3
- Final selected candidate: GELU L20
- Research component: behavioural analysis for AML
- Status: frozen final model lock

## Intended use

Research and downstream integration of transaction behavioural
representations and raw behavioural risk scores.

## Out-of-scope use

This model must not independently:
- accuse an individual or entity of financial crime;
- make autonomous account closures or law-enforcement decisions;
- be interpreted as a calibrated probability of money laundering;
- replace human review, compliance controls, or legal obligations.

## Architecture

Transformer encoder; 45 input features; history length 20; dimension 128;
8 attention heads; 2 encoder layers; feed-forward dimension 256;
GELU; dropout 0.10; padding-aware mean pooling; 128-dimensional output.

## Evaluation

Final lock:
- Validation PR-AUC: 0.152630
- Validation ROC-AUC: 0.851712
- Test PR-AUC: 0.186282
- Test ROC-AUC: 0.851212

Selection was based on validation PR-AUC. Test metrics were not used for
selection.

## Output

The handoff produces a behavioural embedding and a raw risk logit.
The logit is not calibrated and is not a probability.

## Data

The underlying transaction dataset is not distributed in this repository.
Dataset provenance, access permissions, and representativeness must be
assessed before reuse.

## Limitations and risks

- Potential dataset and label bias.
- Distribution shift across institutions, geography, and time.
- Limited evidence of real-world deployment effectiveness.
- No calibrated operational threshold supplied.
- Behavioural signals can be incomplete or misleading.
- Outputs require independent validation and human oversight.

## Reproducibility

Selected evidence and a final lock are provided. Full reproduction requires
authorized source data, training environment, and the identified model
checkpoint, which are not included here.
