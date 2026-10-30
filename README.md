# Temporal Hidden-State Monitoring for Early Detection of Anomalous LLM Generation

## Overview

This project investigates whether the internal hidden-state representations of a frozen GPT-2 Medium model can be used to detect anomalous or hallucination-related generation at an early stage.

Instead of analyzing only the final generated response, the project studies how the model's hidden states change during token-by-token generation.

The extracted temporal and uncertainty features are used with a lightweight Logistic Regression detector.

## Objectives

- Monitor hidden-state representations during text generation.
- Extract temporal trajectory features from hidden states.
- Extract uncertainty features from token generation.
- Evaluate detection at 25%, 50%, 75%, and 100% generation checkpoints.
- Investigate whether anomalous generation can be detected before the complete response is generated.

## Methodology

The overall workflow is:

**Input Prompt → Frozen GPT-2 Medium → Token Generation → Hidden-State Extraction → Feature Extraction → Feature Aggregation → Logistic Regression → Risk Classification**

The monitored hidden-state features include:

- Hidden-state norms
- Hidden-state transitions
- Cosine similarity
- Relative state change

Uncertainty features include:

- Token probability
- Token entropy

Hidden states from layers 3, 4, 5, and 6 are used for the analysis.

## Datasets and Benchmarks

### HaluEval

HaluEval is the main dataset used for the final quantitative experiment.

The original HaluEval QA dataset contains 10,000 records with knowledge, question, right answer, and hallucinated answer.

For the controlled experiment, 100 questions were selected and two conditions were created for each question:

- Correct-answer condition
- Hallucinated-answer condition

This resulted in 200 controlled samples.

### TruthfulQA

TruthfulQA was considered for truthfulness-related evaluation and analysis.

It was not used for the final quantitative evaluation.

### XSTest

XSTest was considered for analysing safe-versus-unsafe generation behaviour.

It was not used for the final quantitative evaluation.

More details are available in `DATASET_INFO.md`.

## Results

### Feature Ablation

| Feature Configuration | Mean ROC-AUC |
|---|---:|
| Trajectory-only | 0.7700 |
| Uncertainty-only | 0.6030 |
| All features | 0.7500 |

### Checkpoint-wise Evaluation

| Checkpoint | Tokens Seen | Tokens Remaining | Mean ROC-AUC |
|---|---:|---:|---:|
| 25% | 8 | 23 | 0.9095 |
| 50% | 16 | 15 | 0.7625 |
| 75% | 24 | 7 | 0.7090 |
| 100% | 31 | 0 | 0.7030 |

The best early detection performance was obtained at the 25% checkpoint, with a mean ROC-AUC of 0.9095.

Complete results are available in `RESULTS.md`.

## Repository Contents

- `Notebook_1.ipynb` – Source code and experiments
- `Notebook_2.ipynb` – Additional experiments/analysis
- `DATASET_INFO.md` – Dataset and benchmark information
- `RESULTS.md` – Experimental results

## Requirements

The project is implemented using Python and deep learning / machine learning libraries used in the provided notebooks.

## How to Run

1. Open either `.ipynb` notebook.
2. Open the notebook in Google Colab.
3. Install the required Python packages if prompted.
4. Provide the required dataset/model resources.
5. Run the notebook cells sequentially.
6. Review the generated features, predictions, and evaluation results.

## Model

The project uses a frozen GPT-2 Medium model.

The underlying language model is not fine-tuned. Hidden-state representations are extracted and analysed while the original model remains unchanged.

## Evaluation

Group-aware 5-fold cross-validation is used for the main feature comparison to reduce data leakage between related samples.

## Key Finding

The results indicate that temporal hidden-state trajectory features can provide a useful signal for distinguishing the controlled generation conditions, including at an early stage of generation.

## Authors

**Dynamites Team**

Academic Deep Learning Project
