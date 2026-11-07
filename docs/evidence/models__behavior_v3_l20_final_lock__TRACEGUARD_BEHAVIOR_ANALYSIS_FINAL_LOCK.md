# TraceGuard Behavioral Analysis — Official Final Model Lock

**Status:** FINAL  
**Decision:** GELU L20 SELECTED  
**Decision basis:** Validation-first model selection using validation PR-AUC  
**Date recorded:** 2026-09-30 07:37:30

---

## 1. Official Final Model

The official TraceGuard Behavioral Analysis model is:

- **Architecture:** TraceGuard Behavioral Transformer V3
- **Activation:** GELU
- **History length:** 20 transactions
- **Input dimension:** 45
- **Transformer dimension:** 128
- **Attention heads:** 8
- **Transformer layers:** 2
- **Feed-forward dimension:** 256
- **Dropout:** 0.1
- **Norm-first:** True
- **Batch-first:** True
- **Positional encoding:** False
- **Pooling:** Padding-aware mean pooling
- **Behavioral embedding:** 128 dimensions
- **Total parameters:** 296,193

---

## 2. Model Selection

Selection was performed using a validation-first procedure.

The test set and stress-test set were not used for model selection.

### Selected model

**GELU L20**

Validation metrics:

- **PR-AUC:** 0.152630297708
- **ROC-AUC:** 0.851712034221

The model was selected from the controlled activation × history-length comparison.

---

## 3. Frozen Test Evaluation

After selection, the test set was evaluated as a frozen observational evaluation.

- **Test PR-AUC:** 0.186282136893
- **Test ROC-AUC:** 0.851212431471

These test metrics were **not used to select the model**.

---

## 4. Exact Checkpoint

Checkpoint:

`models/sequence_length_experiment/results/final_controlled_experiment/checkpoints/traceguard_behavior_v3_sequence_length_L20_best.pt`

SHA-256:

`dd5b28e1c86c5e9b7f4b925b1fded9278d2c1e830d45ffa1c5cc4cf9bb51ed67`

Best training epoch:

**10**

---

## 5. Official Handoff

The official downstream handoff is:

`models/behavior_v3_l20_handoff`

It contains frozen outputs for:

- TRAIN
- VALIDATION
- TEST
- STRESS

The handoff is aligned using:

`Original_Index`

The handoff provides:

1. **128-dimensional behavioral embedding**
2. **Raw behavioral risk logit**

The behavioral risk output is **not a calibrated probability**.

No sigmoid is applied in the handoff.

No threshold is embedded in the handoff.

---

## 6. Final T4 Reproduction Audit

The frozen handoff was independently reproduced on a **Tesla T4 GPU** using:

- the exact checkpoint identified above,
- the canonical L20 test tensor,
- the canonical causal history indices,
- the exact TEST `Original_Index` ordering,
- padding-aware inference,
- `torch.inference_mode()`,
- batch size 4096.

### Alignment

- Official TEST rows: 208,325
- Handoff rows: 208,325
- `Original_Index` membership: EXACT
- `Original_Index` order: EXACT

### Behavioral embedding reproduction

- Maximum absolute difference: **0.0**
- Mean absolute difference: **0.0**

Therefore the stored 128-D behavioral embeddings were reproduced exactly.

### Behavioral risk reproduction

- Maximum absolute difference: **2.86102294921875e-06**
- Mean absolute difference: **4.307244125811849e-07**
- Stored mean: **-8.759546279907227**
- Reproduced mean: **-8.759546279907227**
- Stored median: **-9.228229522705078**
- Reproduced median: **-9.228229522705078**

The observed risk difference is at floating-point numerical precision and does not represent a substantive handoff discrepancy.

### Fully padded sequences

There were 4 fully padded TEST rows.

For all of them:

- Behavioral embedding = exactly zero
- Behavioral risk = exactly zero

---

## 7. Artifact Preservation

No previous artifact was deleted.

The following are preserved for experiment history and auditability:

- Original V3 L10 ReLU handoff
- ReLU L20 alternative handoff
- Previous ReLU final-lock record
- All sequence-length experiment checkpoints
- All comparison and evaluation artifacts

The GELU L20 handoff supersedes the previous ReLU selection as the official final Behavioral Analysis model.

---

## 8. Downstream Interface

The Behavioral Analysis module hands downstream systems:

```text
Original_Index
        |
        +-- behavior_embedding      [128-D]
        |
        +-- behavioral_risk_score   [raw logit]
```

These outputs are intended for downstream fusion with other TraceGuard intelligence, including graph/relationship representations and subsequent risk scoring.

The Behavioral Analysis module itself does not constitute the final fused AML decision layer.

---

## FINAL STATUS

**TRACEGUARD BEHAVIORAL ANALYSIS — FINALIZED**

**Official model: GELU L20**

**Official handoff: behavior_v3_l20_handoff**

**Checkpoint identity: VERIFIED**

**Handoff alignment: VERIFIED**

**Numerical reproduction: VERIFIED**

**Existing handoff modified: NO**

**Test/stress data used for model selection: NO**