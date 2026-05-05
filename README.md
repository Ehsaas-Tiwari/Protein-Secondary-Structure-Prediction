# Protein Secondary Structure Prediction using Sequence Models

## Overview

This project focuses on predicting the **secondary structure of proteins** from amino acid sequences using deep learning. The task is formulated as a **sequence-to-sequence problem**, where each amino acid in the input sequence is mapped to a structural label.

The model predicts both:

* **Q8 (eight-state classification)**
* **Q3 (three-state classification)**

The solution was developed using PyTorch and achieved a **Kaggle leaderboard score of 0.43**.

---

## Problem Statement

Given a peptide sequence (e.g., amino acid string), the objective is to predict its corresponding **secondary structure sequence** of the same length.

This is a **token-level prediction problem**, where each input element maps to an output label.

---

## Dataset Description

### Input

* `seq`: Amino acid sequence

### Output

* `sst8`: Eight-state structure labels
  `{H, G, I, E, B, T, S, C}`

* `sst3`: Three-state structure labels derived from Q8

  * Helix: (H, G, I) → H
  * Strand: (E, B) → E
  * Coil: (C, S, T) → C

### Files

* `train.csv`: Sequences with labels
* `test.csv`: Sequences without labels
* `sample_submission.csv`: Submission format

---

## Approach

### Data Preprocessing

* Encoded amino acid sequences into numerical representations
* Handled masked residues (`*`)
* Ensured input-output sequence alignment
* Applied padding/truncation for batch processing

---

### Model Architectures

#### 1. Bidirectional RNN

* Captures contextual dependencies in both forward and backward directions
* Learns sequence patterns for structure prediction

#### 2. Bi-LSTM / GRU

* Improved long-range dependency handling
* Better performance compared to vanilla RNN
* Used for sequence-to-sequence prediction

---

### Training Strategy

* Token-level prediction for each sequence position
* Loss computed across entire sequence
* Optimized using standard optimizers (e.g., Adam)
* Logged experiments using TrackIO

---

### Inference

* Loaded trained model from saved checkpoints
* Generated predictions for test sequences
* Ensured output sequence length matches input sequence
* Created submission file with both Q8 and Q3 predictions

---

## Results

* Achieved a **Kaggle leaderboard score of 0.43**
* Bi-directional sequence models improved contextual understanding
* Bi-LSTM/GRU models performed better than basic RNN
* Multi-label prediction (Q8 and Q3) successfully implemented

---

## Tech Stack

* Python
* PyTorch
* NumPy, Pandas
* TrackIO (Hugging Face Spaces integration)

---

## Future Improvements

* Use Transformer-based architectures (e.g., BERT for proteins)
* Apply attention mechanisms for better sequence modeling
* Improve handling of long sequences
* Hyperparameter tuning
* Use pretrained protein embeddings (e.g., ESM, ProtBERT)
