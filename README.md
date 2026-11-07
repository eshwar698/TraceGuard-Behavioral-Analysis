# TraceGuard — Behavioural Analysis Module

**A Transformer-based temporal behavioural modelling component for a behaviour-aware Anti-Money Laundering (AML) research framework.**

TraceGuard's behavioural module learns representations of transaction histories and produces behavioural risk scores for downstream AML components.

> **Scope:** This repository documents the behavioural analysis module only. It is not a complete AML platform, production deployment, or standalone financial-crime decision system.

## Research snapshot

| Component | Final configuration |
|---|---|
| Architecture | Transformer encoder V3 |
| Activation / history | GELU / L20 |
| Input features | 45 |
| Model dimension | 128 |
| Attention heads / layers | 8 / 2 |
| Feed-forward dimension | 256 |
| Dropout | 0.10 |
| Embedding dimension | 128 |
| Parameters | 296,193 |
| Best epoch | 10 |

## Final locked evaluation

| Split | PR-AUC | ROC-AUC |
|---|---:|---:|
| Validation | 0.152630 | 0.851712 |
| Test | 0.186282 | 0.851212 |

Validation PR-AUC was used for candidate selection. Test metrics are observational and were not used to select the model. Stress evaluation was also excluded from model selection.

## What this repository contains

- Temporal transaction-sequence modelling with a Transformer encoder.
- Behavioural representation and embedding-quality analyses.
- Controlled sequence-length experiments.
- Hard-negative learning and ablation analyses.
- Final validation, model-lock, and downstream handoff evidence.

## Research walkthroughs

1. [Data preparation and temporal sequences](notebooks/01_data_preparation_and_temporal_sequences.ipynb)
2. [Behavioural Transformer architecture](notebooks/02_behavioral_transformer_architecture.ipynb)
3. [Training and sequence-length experiments](notebooks/03_training_and_sequence_length_experiments.ipynb)
4. [Behavioural embedding quality](notebooks/04_behavioral_embedding_quality.ipynb)
5. [Hard-negative learning and ablation](notebooks/05_hard_negative_learning_and_ablation.ipynb)
6. [Final validation and model handoff](notebooks/06_final_validation_and_model_handoff.ipynb)

These are curated research walkthroughs. Original private data and model checkpoints are not included; therefore, full training is not reproducible from this repository alone.

## Documentation and evidence

- [Methodology](docs/methodology.md)
- [Results and interpretation](docs/results.md)
- [Model card](docs/model_card.md)
- [Limitations](docs/limitations.md)
- [Final model-lock JSON](docs/evidence/models__behavior_v3_l20_final_lock__TRACEGUARD_BEHAVIOR_ANALYSIS_FINAL_LOCK.json)
- [Final model-lock report](docs/evidence/models__behavior_v3_l20_final_lock__TRACEGUARD_BEHAVIOR_ANALYSIS_FINAL_LOCK.md)
- [Evidence manifest and SHA-256 hashes](docs/evidence/evidence_manifest.json)
- [Evidence directory](docs/evidence/)

## Interpretation and limitations

- The model is a research component, not a calibrated probability engine.
- Behavioural risk scores are raw logits; they are not probabilities or AML decisions.
- Offline metrics do not establish real-world or operational AML effectiveness.
- Original dataset access is restricted, and model checkpoints are not included in this repository.
- Human review and independent validation remain necessary.

## Project status

**Behavioural analysis module completed; wider TraceGuard integration remains ongoing.**
