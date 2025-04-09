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

## Detailed Description of Targets

Proteins are encoded in the genome, and names of the genes encoding those proteins are typically bestowed by their discoverers and regulated by the Hugo Gene Nomenclature Committee. The protein products of these genes can sometimes have different names, often due to the history of their discovery.

We screened three protein targets for this competition.

### EPHX2 (sEH)

The first target, epoxide hydrolase 2, is encoded by the EPHX2 genetic locus, and its protein product is commonly named “soluble epoxide hydrolase”, or abbreviated to sEH. Hydrolases are enzymes that catalyze certain chemical reactions, and EPHX2/sEH also hydrolyzes certain phosphate groups. EPHX2/sEH is a potential drug target for high blood pressure and diabetes progression, and small molecules inhibiting EPHX2/sEH from earlier DEL efforts made it to clinical trials.

EPHX2/sEH was also screened with DELs, and hits predicted with ML approaches, in a recent study but the screening data were not published. We included EPHX2/sEH to allow contestants an external gut check for model performance by comparing to these previously-published results.

We screened EPHX2/sEH purchased from Cayman Chemical, a life sciences commercial vendor. For those contestants wishing to incorporate protein structural information in their submissions, the amino sequence is positions 2-555 from UniProt entry P34913, the crystal structure can be found in PDB entry 3i28, and predicted structure can be found in AlphaFold2 entry 34913. Additional EPHX2/sEH crystal structures with ligands bound can be found in PDB.

### BRD4

The second target, bromodomain 4, is encoded by the BRD4 locus and its protein product is also named BRD4. Bromodomains bind to protein spools in the nucleus that DNA wraps around (called histones) and affect the likelihood that the DNA nearby is going to be transcribed, producing new gene products. Bromodomains play roles in cancer progression and a number of drugs have been discovered to inhibit their activities.

BRD4 has been screened with DEL approaches previously but the screening data were not published. We included BRD4 to allow contestants to evaluate candidate molecules for oncology indications.

We screened BRD4 purchased from Active Motif, a life sciences commercial vendor. For those contestants wishing to incorporate protein structural information in their submissions, the amino acid sequence is positions 44-460 from UniProt entry O60885-1, the crystal structure (for a single domain) can be found in PDB entry 7USK and predicted structure can be found in AlphaFold2 entry O60885. Additional BRD4 crystal structures with ligands bound can be found in PDB.

### ALB (HSA)

The third target, serum albumin, is encoded by the ALB locus and its protein product is also named ALB. The protein product is sometimes abbreviated as HSA, for “human serum albumin”. ALB, the most common protein in the blood, is used to drive osmotic pressure (to bring fluid back from tissues into blood vessels) and to transport many ligands, hormones, fatty acids, and more.

Albumin, being the most abundant protein in the blood, often plays a role in absorbing candidate drugs in the body and sequestering them from their target tissues. Adjusting candidate drugs to bind less to albumin and other blood proteins is a strategy to help these candidate drugs be more effective.

ALB has been screened with DEL approaches previously but the screening data were not published. We included ALB to allow contestants to build models that might have a larger impact on drug discovery across many disease types. The ability to predict ALB binding well would allow drug developers to improve their candidate small molecule therapies much more quickly than physically manufacturing many variants and testing them against ALB empirically in an iterative process.

We screened ALB purchased from Active Motif. For those contestants wishing to incorporate protein structural information in their submissions, the amino acid sequence is positions 25 to 609 from UniProt entry P02768, the crystal structure can be found in PDB entry 1AO6, and predicted structure can be found in AlphaFold2 entry P02768. Additional ALB crystal structures with ligands bound can be found in PDB.

---

## 🔗 Reference

BELKA dataset created and released by [Leash Biosciences](https://leash.bio), as part of the NeurIPS 2024 BELKA Challenge.

