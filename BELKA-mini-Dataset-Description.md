# 📦 BELKA-mini Dataset Description

## Overview

The BELKA-mini dataset is a lightweight version of the BELKA competition dataset, containing labeled examples of whether a small molecule binds to one of three protein targets. The data were generated using **DNA-Encoded Library (DEL)** technology and formatted for easy use in machine learning.

Molecules are represented using **SMILES** (Simplified Molecular-Input Line-Entry System), and the target label is a binary value (`binds` = 1 or 0) for each protein target.

---

## 📁 Files

You will find the following files:

- `train.csv` — training data with full labels
- `val.csv` — validation data with labels
- `test.csv` — test data including a column `is_novel` to identify molecules using unseen building blocks
- `sample_submission.csv` — example format for making submissions

Each file contains:

| Column | Description |
|--------|-------------|
| `id` | Unique identifier for each molecule-target pair |
| `buildingblock1_smiles` | SMILES string of the first building block |
| `buildingblock2_smiles` | SMILES string of the second building block |
| `buildingblock3_smiles` | SMILES string of the third building block |
| `molecule_smiles` | Full molecule SMILES (includes building blocks and core) |
| `protein_name` | One of three protein targets: `sEH`, `BRD4`, or `HSA` |
| `binds` | Binary label (1 = binder, 0 = non-binder); not available in competition test set |
| `is_novel` | Only in test set — indicates use of novel building blocks (compared to training) |

---

## 📊 Data Summary

In the original BELKA competition, over **133 million molecules** were screened against 3 protein targets. In BELKA-mini, we provide a **representative subset (~900,000 molecules)** with the same class imbalance (~0.5% binders). A portion of the test set contains **novel building blocks not seen during training**, allowing for generalization testing.

---

## 🧬 Targets

We evaluate binding against three proteins:

### EPHX2 (sEH)

- **Gene name**: EPHX2
- **Common name**: Soluble Epoxide Hydrolase (sEH)
- **Function**: Enzyme involved in blood pressure and diabetes regulation
- **DEL screened protein**: Purchased from Cayman Chemical
- **Structure**:
  - UniProt: P34913 (positions 2–555)
  - Crystal: PDB 3i28
  - AlphaFold: P34913

### BRD4

- **Gene name**: BRD4
- **Function**: Regulates transcription through histone binding; relevant in cancer
- **DEL screened protein**: Purchased from Active Motif
- **Structure**:
  - UniProt: O60885-1 (positions 44–460)
  - Crystal: PDB 7USK
  - AlphaFold: O60885

### ALB (HSA)

- **Gene name**: ALB
- **Common name**: Human Serum Albumin (HSA)
- **Function**: Transports ligands and regulates osmotic pressure
- **DEL screened protein**: Purchased from Active Motif
- **Structure**:
  - UniProt: P02768 (positions 25–609)
  - Crystal: PDB 1AO6
  - AlphaFold: P02768

---

## 🧪 Experimental Context

DELs are large libraries of small molecules, each tagged with a unique DNA barcode. These libraries allow pooled screening of millions of molecules in a single experiment.

Instead of testing molecules one by one, DELs are exposed to a protein target. After rinsing away non-binders, the DNA tags of bound molecules are sequenced to identify them. This allows **massive parallel binding assays**.

### Building Blocks

Each molecule in BELKA was assembled from three building blocks attached to a central scaffold. This combinatorial design means:
- Few building blocks → Many molecules
- Each row in the dataset corresponds to one such combination

---

## 🧠 Representation

All molecules are provided as **SMILES strings**, which can be easily converted to:
- Molecular graphs
- 3D conformers
- Fingerprints (e.g., ECFP)
- Pretrained representations (e.g., Mol2Vec, ChemBERTa)

RDKit can be used for parsing, featurizing, and manipulating SMILES.

---

## 🧪 Note on Novelty

The `test.csv` split includes a column `is_novel` that flags whether any of the building blocks are **not present in training**. These examples are used to test model generalization across unseen chemical space.

---

## 🔗 Reference

BELKA dataset created and released by [Leash Biosciences](https://leash.bio), as part of the NeurIPS 2024 BELKA Challenge.

