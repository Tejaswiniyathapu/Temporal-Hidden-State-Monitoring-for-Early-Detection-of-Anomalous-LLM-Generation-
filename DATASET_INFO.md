# Dataset Information

## Benchmarks Used

### 1. HaluEval
- Used for hallucination-related evaluation.
- It is the main dataset used in the final quantitative experiment.
- The original HaluEval QA dataset contains 10,000 records.
- Each record contains knowledge, question, right answer, and hallucinated answer.
- For the controlled experiment, 100 questions were selected.
- Two conditions were created for each question:
  - Correct-answer condition
  - Hallucinated-answer condition
- This resulted in 200 controlled samples.

### 2. TruthfulQA
- Used for truthfulness-related evaluation and analysis.
- It was considered as part of the broader evaluation context of the project.
- TruthfulQA was not used for the final quantitative evaluation.

### 3. XSTest
- Used to explore safe-vs-unsafe generation behaviour.
- It was considered as an additional benchmark during the experimental investigation.
- XSTest was not used for the final quantitative evaluation.

## Model

The project uses a frozen GPT-2 Medium model. The model parameters are not fine-tuned.

## Features Extracted

The project extracts features from the model's internal representations, including:

- Hidden-state norms
- Hidden-state transitions
- Cosine similarity
- Relative state change
- Token probability
- Token entropy

Hidden states from layers 3, 4, 5 and 6 are monitored.

## Evaluation

The final detector uses Logistic Regression to classify the controlled generation conditions.

Group-aware 5-fold cross-validation is used for evaluation.
