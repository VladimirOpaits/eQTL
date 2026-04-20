# ISOFORM CLASSIFAER

## DATA

- **Isoforms**: ENCODE ENCFF370SDY (WTC11, PacBio Iso-Seq via TALON)
- **Reference**: GENCODE v39, hg38
- **Processing**: SQANTI3 QC + TD2 ORF prediction (run separately)

## Target Classes

Two versions are compared:

**4-class version** (`target_4class`):

| Class | Description |
|-------|-------------|
| `real_high` | High confidence real isoform (FSM reference_match, NIC known junctions) |
| `real_mid` | Moderate confidence (FSM mono-exon, NIC known splicesites) |
| `uncertain` | Ambiguous — could be real or artifact (ISM, NNC) |
| `artifact` | Likely sequencing artifact (genic_intron, intergenic, antisense...) |

**3-class version** (`target_3class`): `real_high` and `real_mid` merged into `real`.

Both versions are trained and compared to assess whether the model
can distinguish confidence levels within real isoforms.

## Experiments

| # | Model | Input |
|---|-------|-------|
| 1 | Random Forest | Tabular features only (baseline) |
| 2 | Conv1D | Nucleotide sequence only |
| 3 | Conv1D + MLP | Sequence + tabular features |