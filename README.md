# The MassBank contributions of the mFam Collaboration – Chemical space explorer

This repository contains the code and data required to reproduce **Figure 3** from:

> *The MassBank contributions of the mFam Collaboration: A Global Push to Boost the Coverage and Structural Diversity of MassBank*

The analysis compares the chemical space of the mFam contributions to a previous MassBank release (2025.05.1) using molecular fingerprints, UMAP embedding, and nearest-neighbor similarity analysis.

---

## Input data

Two input tables are required:

### 1) MassBank baseline (2025.05.1)

`data/MassBank_master_with_smiles.tsv`

Must contain at least:
- accession
- a SMILES column

### 2) mFam contribution

`data/mFam_master_raw.csv`

Must contain at least:
- accession
- a SMILES column

The notebook automatically:
- normalizes SMILES
- computes fingerprints
- handles headered or headerless files

---

## Environment setup

Create the conda environment:

```bash
conda env create -f environment.yml
conda activate mfam-figure3
```

Then launch Jupyter:

```bash
jupyter lab
```
---

## What the notebook does

The notebook:

1. Loads both datasets
2. Canonicalizes SMILES
3. Computes ECFP4 (Morgan radius = 2) fingerprints (2048 bits)
4. Computes UMAP embedding (Jaccard metric)
5. Calculates nearest-neighbor Tanimoto similarity (mFam → MassBank 2025.05.1)
6. Generates Figure 3 panels:
  - UMAP projection (MassBank vs mFam)
  - Similarity distribution (excluding near-identical matches ≥ 0.99)
  - Structures of the top 20 most structurally distinct mFam compounds

All figures are written to the results/ directory.

---

## Reproducibility notes

- UMAP layout is deterministic due to a fixed random seed.
- Fingerprints: ECFP4 (radius = 2, 2048 bits).
- Similarity: Tanimoto coefficient (RDKit implementation).
- Novelty threshold for filtering near-identical matches: ≥ 0.99.

---

## Computational requirements

- RAM usage depends on the size of the MassBank baseline dataset.
- The nearest-neighbor similarity step may take several minutes for large datasets.

---

## Contact
For questions regarding the analysis or implementation:

Esteban Charria-Girón (esteban.charriagiron@wur.nl)
mFam Collaboration