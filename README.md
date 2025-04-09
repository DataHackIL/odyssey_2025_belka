## 🧬 BELKA-mini: Predict Small Molecule Binding

Welcome to the **BELKA-mini** challenge — a scaled-down version of the [BELKA competition from NeurIPS 2024](https://www.kaggle.com/competitions/leash-BELKA). In this hackathon-style challenge, your goal is to **predict whether a small molecule binds to a specific protein target** based on its SMILES representation.

This repo provides everything you need to get started.

---

## 📁 Repository Contents

| File / Folder                      | Description |
|-----------------------------------|-------------|
| `small_belka_splits/`             | Cleaned and balanced `train.csv`, `val.csv`, `test.csv` files |
| `small_belka_splits_900k/`        | A larger version of the problem; use it if you can, computationally. |
| `starter_model.ipynb`             | A baseline model using ECFPs + Random Forest |
| `belka_hint_exploration.ipynb`    | A deeper exploration notebook (shared later during the hackathon) |
| `submission.csv` (optional)       | Example format for leaderboard submission |
| `BELKA-mini-Overview.md`          | A detailed overview of the challenge |
| `BELKA-mini-Dataset-Description.md`| A detailed description of the dataset |
| `README.md`                       | You’re here! |

---

## 🎯 Challenge Overview

Given:
- A small molecule's **SMILES** string (representing its structure)
- The **protein target** name

Your task is to:
- Predict whether the molecule will **bind** to the target.

This is a **binary classification problem**. Binding is highly imbalanced (less than 1% of molecules bind), so careful modeling and evaluation are key!

---

## 🔬 Dataset Structure

Each row contains:
- `id`: unique identifier
- `buildingblock1/2/3_smiles`: SMILES for each component
- `molecule_smiles`: full molecule SMILES (including triazine core)
- `protein_name`: one of three targets (HSA, BRD4, sEH)
- `binds`: 1 if the molecule binds the protein, 0 otherwise
- `is_novel`: **(test only)** 1 if the molecule includes building blocks not seen in the training set

---

## 🧪 Evaluation Metric

Submissions are scored using **average precision (AP)**.  
Final score = average AP **per protein + novelty group** (as in the original BELKA challenge).

---

## 🚀 How to Get Started

1. Open `starter_model.ipynb`
2. Run the featurization and baseline training
3. Submit predictions on the `test.csv` molecules

You’ll be using:
- **ECFP fingerprints** (via RDKit)
- **Protein one-hot encoding**
- A simple **Random Forest**

This notebook is designed to work directly on Kaggle with no extra setup.

---

## 💡 Hint Notebook (Advanced)

Once you’ve got a baseline, check out `belka_hint_exploration.ipynb`:

- Analyze **class imbalance**
- Explore **novel vs. known** molecules
- Evaluate predictions **by protein or novelty**
- Learn how the **test set was constructed for generalization**

Use this notebook to improve how you evaluate and tune your models.

---

## 🧠 Tips for Participants

- The test set contains molecules from **new parts of chemical space**
- A good model should **generalize**, not just memorize
- Try:
  - Graph neural networks (GNNs)
  - 3D-aware models
  - Contrastive learning on SMILES
  - Pre-trained chemical embeddings (ChemBERTa, Mol2Vec)

---

## 📤 Submitting Predictions

Your submission should be a CSV with:
```
id,binds
123456789,0.013
123456790,0.872
...
```

Submit to the platform’s leaderboard for evaluation!

---

## 🙌 Credits

This mini-challenge is derived from the original **BELKA** dataset by Leash Biosciences, restructured for educational use.

Special thanks to NeurIPS 2024 + BELKA organizers for sharing this awesome dataset.
