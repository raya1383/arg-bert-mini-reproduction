# ARG-BERT Mini Reproduction with Confidence-Aware Selective Prediction

A resource-constrained implementation inspired by:

> Yagimoto K, Hosoda S, Sato M, Hamada M.  
> **Prediction of antibiotic resistance mechanisms using a protein language model.**  
> Bioinformatics, 2024.

## Overview

The original ARG-BERT study fine-tunes ProteinBERT to classify antibiotic resistance genes (ARGs) into six resistance mechanisms.

A complete reproduction of the original study is computationally expensive and the full HMD-ARG training dataset used by the authors is not distributed with the official ARG-BERT repository.

This project therefore implements a smaller, reproducible version of the original idea using:

- CARD-derived protein sequences
- Pretrained ProteinBERT representations
- Logistic Regression for resistance-mechanism classification
- A lightweight amino-acid 3-mer baseline
- Confidence-aware selective prediction as a creative extension

The goal is not to reproduce the exact numbers reported in the original paper, but to reproduce the main modeling idea under limited computational resources.

---

## Resistance Mechanisms

The classification task contains the same six resistance-mechanism categories considered in the ARG-BERT paper:

1. antibiotic efflux
2. antibiotic inactivation
3. antibiotic target alteration
4. antibiotic target protection
5. antibiotic target replacement
6. others

---

## Dataset

The original HMD-ARG dataset was not publicly distributed with the ARG-BERT implementation.

Therefore, a reproducible dataset was constructed using protein sequences from the Comprehensive Antibiotic Resistance Database (CARD).

For the mini experiment, a small stratified subset was selected to make the experiment feasible on limited hardware.

Mini dataset size:

- Total proteins: 158
- Training proteins: 118
- Test proteins: 40

Class distribution:

| Class | Samples |
|---|---:|
| antibiotic efflux | 30 |
| antibiotic inactivation | 30 |
| antibiotic target alteration | 30 |
| antibiotic target protection | 30 |
| antibiotic target replacement | 30 |
| others | 8 |

---

## Method

### Baseline

A lightweight sequence baseline was implemented using:

```text
Protein sequence
→ amino-acid 3-mer TF-IDF
→ Logistic Regression
→ resistance mechanism
