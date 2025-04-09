## 🧬 BELKA-mini Hackathon Challenge

**Predict small molecule-protein interactions using a scaled-down version of the BELKA dataset.**

---

## 🧭 Overview

In this hackathon challenge, you’ll develop machine learning (ML) models to predict the binding of small molecules to specific protein targets – a critical step in drug development. Your models will help determine which drug-like small molecules are likely to bind to any of **three protein targets**.

This competition is inspired by the [NeurIPS 2024 BELKA Challenge](https://www.kaggle.com/competitions/leash-BELKA), adapted into a lightweight, hackathon-friendly format using a curated subset of the original data.

---

## 🧪 Motivation

Traditional drug discovery involves labor-intensive experiments. DNA-encoded chemical libraries (DELs) let researchers test millions of molecules in parallel using DNA barcodes to track binding interactions. The BELKA dataset was built using such DEL technology and is one of the largest binding datasets ever released (~133 million molecules tested against 3 protein targets).

Machine learning offers a powerful alternative: **use data to predict binding affinity computationally**, helping reduce cost and accelerate drug discovery.

---

## 📦 Dataset Description

You are provided with a curated subset of the BELKA dataset:

Each row in the dataset includes:
- `id`: molecule ID
- `buildingblock1/2/3_smiles`: SMILES of the three building blocks
- `molecule_smiles`: full SMILES of the molecule
- `protein_name`: one of {HSA, BRD4, sEH}
- `binds`: binary binding label (1 = binds, 0 = non-binder)
- `is_novel`: **test set only** — whether the molecule contains a building block not seen in training

---

## 🧬 Goal

Build a model that predicts the probability of binding (`binds`) given a molecule’s SMILES and protein target. You’ll be evaluated on **average precision**, especially in **novel generalization cases** where building blocks differ from those seen during training.

---

## 📊 Evaluation Metric

We use **average precision (AP)** as the scoring metric, calculated per (protein, novelty group), then averaged.

---

## 📤 Submission Format

Submit a `.csv` file with:
```
id,binds
100000001,0.014
100000002,0.987
...
```

Your predictions should be probabilities between 0 and 1.

---

## 🧠 What Makes This Challenge Special?

- **Novelty-aware generalization**: Part of the test set includes novel building blocks not seen during training.
- **Real-world molecular data**: Derived from one of the largest DEL experiments ever conducted.
- **Explore different molecule representations**: Try ECFPs, graphs, SMILES transformers, or 3D embeddings.
- **Minimal setup**: All data is in `.csv`, with starter notebooks to help you hit the ground running.

---

## 🧱 DEL & Chemistry Context (Simplified)

DELs (DNA-Encoded Libraries) are mixtures of small molecules tagged with DNA barcodes. They enable ultra-high-throughput binding assays by letting scientists track which molecules bind to protein targets.

Each molecule in BELKA was assembled from **3 building blocks** (like chemical "ears" and a "face"). The combination of these parts gives rise to over 133 million molecules, but from a relatively small set of building blocks.

---

## 🔗 Citations & Credits

> Andrew Blevins, Ian K Quigley, Brayden J Halverson, Nate Wilkinson, Rebecca S Levin, Agastya Pulapaka, Walter Reade, and Addison Howard.  
> **NeurIPS 2024 - Predict New Medicines with BELKA**  
> https://kaggle.com/competitions/leash-BELKA

This BELKA-mini adaptation was created for educational use and rapid experimentation.

Special thanks to **Leash Biosciences** for releasing the BELKA dataset and making this work possible.
