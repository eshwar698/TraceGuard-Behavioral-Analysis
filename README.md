# TraceGuard — Behavioural Analysis Module

**A Transformer-based temporal behavioural analysis component for a
behaviour-aware Anti-Money Laundering (AML) research framework.**

TraceGuard's behavioural module learns representations of transaction
histories and produces behavioural risk scores for downstream AML components.

> **Scope:** This repository documents the behavioural analysis module.
> It is not a complete AML platform, production deployment, or standalone
> financial-crime decision system.

## Overview

- Temporal transaction-sequence modelling with a Transformer encoder.
- 128-dimensional behavioural embeddings.
- Behavioural risk scores exposed as raw logits for downstream integration.
- Controlled sequence-length experiments.
- Behavioural representation and validation analyses.
- Frozen final model selection and handoff evidence.

## Final model

The final locked candidate is **GELU, history length 20 (L20)**.

| Property | Value |
|---|---|
| Architecture | Transformer encoder V3 |
| Activation | GELU |
| History length | 20 |
| Input features | 45 |
| Model dimension | 128 |
| Attention heads | 8 |
| Encoder layers | 2 |
| Feed-forward dimension | 256 |
| Dropout | 0.10 |
| Embedding dimension | 128 |
| Parameters | 296,193 |
| Best epoch | 10 |

## Final locked evaluation

| Split | PR-AUC | ROC-AUC |
|---|---:|---:|
| Validation | 0.1526 | 0.8517 |
| Test | 0.1863 | 0.8512 |

Validation metrics were used for model selection. Test metrics are reported
as final observational evaluation, not as a selection criterion.

The test set and stress evaluation were not used to select the final model.

## Repository structure

```text
TraceGuard-Behavioral-Analysis/
├── README.md
├── LICENSE
├── CITATION.cff
├── .gitignore
├── docs/
│   ├── methodology.md
│   ├── results.md
│   ├── model_card.md
│   ├── limitations.md
│   └── evidence/
├── notebooks/
├── results/
│   └── figures/
└── artifacts/
```

## Notebooks

1. Data preparation and temporal sequences
2. Behavioural Transformer architecture
3. Training and sequence-length experiments
4. Behavioural embedding quality
5. Hard-negative learning and ablation
6. Final validation and model handoff

These notebooks are curated research walkthroughs. The original private
data and model checkpoints are not included, so full training is not
reproducible from this repository alone.

## Evidence

Selected experiment outputs and the final model lock are available under
[`docs/evidence/`](docs/evidence/). See the evidence manifest for file
integrity hashes and source-artifact lineage.

## Limitations

- The model is a research component, not a calibrated probability engine.
- A raw risk logit is not a probability or an AML decision.
- No claim of real-world deployment effectiveness is made.
- Dataset access and checkpoint availability are restricted/not included.
- Human review and independent validation remain necessary.

## Status

**Behavioural analysis module completed; wider TraceGuard integration remains ongoing.**
