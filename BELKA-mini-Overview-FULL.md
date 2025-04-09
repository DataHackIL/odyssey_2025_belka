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

###  The Original Problem Description

Small molecule drugs are chemicals that interact with cellular protein machinery and affect the functions of this machinery in some way. Often, drugs are meant to inhibit the activity of single protein targets, and those targets are thought to be involved in a disease process. A classic approach to identify such candidate molecules is to physically make them, one by one, and then expose them to the protein target of interest and test if the two interact. This can be a fairly laborious and time-intensive process.

The US Food and Drug Administration (FDA) has approved roughly 2,000 novel molecular entities in its entire history. However, the number of chemicals in druglike space has been estimated to be 10^60, a space far too big to physically search. There are likely effective treatments for human ailments hiding in that chemical space, and better methods to find such treatments are desirable to us all.

To evaluate potential search methods in small molecule chemistry, competition host Leash Biosciences physically tested some 133M small molecules for their ability to interact with one of three protein targets using DNA-encoded chemical library (DEL) technology. This dataset, the Big Encoded Library for Chemical Assessment (BELKA), provides an excellent opportunity to develop predictive models that may advance drug discovery.

Datasets of this size are rare and restricted to large pharmaceutical companies. The current best-curated public dataset of this kind is perhaps bindingdb, which, at 2.8M binding measurements, is much smaller than BELKA.

This competition aims to revolutionize small molecule binding prediction by harnessing ML techniques. Recent advances in ML approaches suggest it might be possible to search chemical space by inference using well-trained computational models rather than running laboratory experiments. Similar progress in other fields suggest using ML to search across vast spaces could be a generalizable approach applicable to many domains. We hope that by providing BELKA we will democratize aspects of computational drug discovery and assist the community in finding new lifesaving medicines.

Here, you’ll build predictive models to estimate the binding affinity of unknown chemical compounds to specified protein targets. You may use the training data provided; alternatively, there are a number of methods to make small molecule binding predictions without relying on empirical binding data (e.g. DiffDock, and this contest was designed to allow for such submissions).

Your work will contribute to advances in small molecule chemistry used to accelerate drug discovery.


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

## 🧪 Additional Details

### Chemical Representations

One of the goals of this competition is to explore and compare many different ways of representing molecules. Small molecules have been represented with SMILES, graphs, 3D structures, and more, including more esoteric methods such as spherical convolutional neural nets. We encourage competitors to explore not only different methods of making predictions but also to try different ways of representing the molecules.

We provide the molecules in SMILES format.

### SMILES

SMILES is a concise string notation used to represent the structure of chemical molecules. It encodes the molecular graph, including atoms, bonds, connectivity, and stereochemistry as a linear sequence of characters, by traversing the molecule graph. SMILES is widely used in machine learning applications for chemistry, such as molecular property prediction, drug discovery, and materials design, as it provides a standardized and machine-readable format for representing and manipulating chemical structures.

The SMILES in this dataset should be sufficient to be translated into any other chemical representation format that you want to try. A simple way to perform some of these translations is with RDKit.

### Details about the Experiments

DELs are libraries of small molecules with unique DNA barcodes covalently attached. Traditional high-throughput screening requires keeping individual small molecules in separate, identifiable tubes and demands a lot of liquid handling to test each one of those against the protein target of interest in a separate reaction. The logistical overhead of these efforts tends to restrict screening collections, called libraries, to 50K–5M small molecules.

A scalable solution to this problem, DNA-encoded chemical libraries, was described in 2009. As DNA sequencing got cheaper and cheaper, it became clear that DNA itself could be used as a label to identify, and deconvolute, collections of molecules in a complex mixture. DELs leverage this DNA sequencing technology.

These barcoded small molecules are in a pool (many in a single tube, rather than one tube per small molecule) and are exposed to the protein target of interest in solution. The protein target of interest is then rinsed to remove small molecules in the DEL that don’t bind the target, and the remaining binders are collected and their DNA sequenced.

### DELs Are Manufactured by Combining Different Building Blocks

An intuitive way to think about DELs is to imagine a Mickey Mouse head as an example of a small molecule in the DEL. We attach the DNA barcode to Mickey’s chin. Mickey’s left ear is connected by a zipper; Mickey’s right ear is connected by Velcro. These attachment points of zippers and Velcro are analogies to different chemical reactions one might use to construct the DEL.

We could purchase ten different Mickey Mouse faces, ten different zipper ears, and ten different Velcro ears, and use them to construct our small molecule library. By creating every combination of these three, we’ll have 1,000 small molecules, but we only needed thirty building blocks (faces and ears) to make them. This combinatorial approach is what allows DELs to have so many members: the library in this competition is composed of 133M small molecules. The 133M small molecule library used here, AMA014, was provided by AlphaMa. It has a triazine core and superficially resembles the DELs described here.

---

## 🔗 Citations & Credits

> Andrew Blevins, Ian K Quigley, Brayden J Halverson, Nate Wilkinson, Rebecca S Levin, Agastya Pulapaka, Walter Reade, and Addison Howard.  
> **NeurIPS 2024 - Predict New Medicines with BELKA**  
> https://kaggle.com/competitions/leash-BELKA

This BELKA-mini adaptation was created for educational use and rapid experimentation.

Special thanks to **Leash Biosciences** for releasing the BELKA dataset and making this work possible.
