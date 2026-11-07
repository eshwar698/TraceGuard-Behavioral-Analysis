# Methodology

## 1. Objective

Learn temporal representations of transaction behaviour from historical
transaction sequences and provide behavioural signals for downstream AML
risk analysis.

## 2. Sequence representation

The behavioural pipeline transforms transaction histories into fixed-length
sequences with 45 input features. Experiments compare history lengths
L5, L7, L10, L15 and L20.

Sequence construction, preprocessing and split membership are documented
in the research notebooks and retained experiment artifacts. The row
identifier used for final handoff is `Original_Index`.

## 3. Transformer encoder

The selected V3 encoder uses:

- Input feature dimension: 45
- Model dimension: 128
- Attention heads: 8
- Encoder layers: 2
- Feed-forward dimension: 256
- Dropout: 0.10
- GELU activation
- Batch-first processing
- Pre-normalization (`norm_first`)
- Padding-aware mean pooling
- 128-dimensional behavioural embedding

The final architecture does not use positional encoding. Therefore,
claims about explicit positional encoding should not be attributed to
this final model.

## 4. Training and selection

Controlled experiments evaluated multiple sequence lengths. Candidate
selection was validation-first using PR-AUC. Test and stress evaluations
were not used to select the model.

The final lock records GELU L20 as the selected candidate and identifies
its checkpoint by SHA-256. Training was not changed after final selection.

## 5. Handoff

The handoff exports:

- 128-dimensional behavioural embeddings
- Raw behavioural risk logits
- Original row identity/order

The handoff does not apply sigmoid conversion, probability calibration,
or a final operational threshold. Downstream systems must define and
validate those decisions independently.

## 6. Evidence lineage

The repository preserves distinct evidence families:

- Controlled GELU sequence-length experiment
- Historical ReLU candidate experiments
- V1 versus V3 comparison
- GELU L20 final lock and handoff validation

These are separate experiment lineages and their metrics must not be
combined as if they were one evaluation.
