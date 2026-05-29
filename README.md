# Arabic Narrative Question Answering using mT5

This repository contains the code, data files, predictions, and evaluation outputs for an Arabic narrative question-answering project using a transformer-based encoder-decoder model. The main model used is `google/mt5-large`, evaluated before and after fine-tuning on a curated Arabic QA dataset.

The final report, proposal, and presentation are submitted separately.

## Project Overview

The task is Arabic text-to-text question answering.
Given an Arabic question and a related context passage, the model generates an Arabic answer grounded in the provided source.

The project compares:

1. **Baseline mT5-large**
   The original `google/mt5-large` model without fine-tuning.

2. **Fine-tuned mT5-large with full context**
   The model is fine-tuned using the full available context.

3. **Fine-tuned mT5-large with BM25-focused context**
   BM25 is used to select more focused context sentences before answer generation.

4. **ChatGPT API baseline**
   A separate API-based baseline tested on the same held-out QA data.

## Repository Structure

```text
mt5-arabic-narrative-qa-finetuning/
│
├── chat-gpt5.4-nano-model/
│   └── chatgpt_api_test_heldout_qa.ipynb
│
├── data/
│   ├── docs.csv
│   └── train_qa.csv
│
├── data extraction and processing/
│   ├── answers_with_refs.ipynb
│   ├── data_preprocessing_nlp_project.ipynb
│   ├── Howiyya_article_extraction.ipynb
│   └── Video_text_extraction.ipynb
│
├── mt5-large-model/
│   ├── mt5_large_full_context.ipynb
│   ├── baseline_test_metrics_corrected.csv
│   ├── baseline_test_prediction_details.csv
│   ├── fine_tuned_test_metrics_corrected.csv
│   ├── fine_tuned_test_prediction_details.csv
│   ├── fine_tuned_test_prediction_details_corrected_metrics.csv
│   ├── config (1).json
│   └── spiece (1).model
│
├── mt5-large-bm25-model/
│   ├── NLP_Project_mt5_large_BM25_final.ipynb
│   ├── bm25_focused_trained_test_predictions.csv
│   ├── bm25_focused_trained_test_prediction_details.csv
│   ├── error_analysis - Selected_30.csv
│   ├── config.json
│   └── spiece.model
│
└── README.md
```

## Data

The dataset is stored in:

```text
data/train_qa.csv
data/docs.csv
```

The dataset contains Arabic question-answer pairs with related source/context information. The data was cleaned and prepared using the notebooks inside:

```text
data extraction and processing/
```

The dataset was split into training, validation, and held-out test data for fair comparison between the baseline and fine-tuned systems.

## Models

The main transformer model is:

```text
google/mt5-large
```

This is a multilingual encoder-decoder transformer model. The encoder processes the question and context, while the decoder generates the final Arabic answer.

## Main Experiments

### 1. Baseline mT5-large

Notebook:

```text
mt5-large-model/mt5_large_full_context.ipynb
```

Outputs:

```text
baseline_test_metrics_corrected.csv
baseline_test_prediction_details.csv
```

### 2. Fine-tuned mT5-large with Full Context

Notebook:

```text
mt5-large-model/mt5_large_full_context.ipynb
```

Outputs:

```text
fine_tuned_test_metrics_corrected.csv
fine_tuned_test_prediction_details.csv
fine_tuned_test_prediction_details_corrected_metrics.csv
```

### 3. Fine-tuned mT5-large with BM25 Context

Notebook:

```text
mt5-large-bm25-model/NLP_Project_mt5_large_BM25_final.ipynb
```

Outputs:

```text
bm25_focused_trained_test_predictions.csv
bm25_focused_trained_test_prediction_details.csv
```

### 4. ChatGPT API Baseline

Notebook:

```text
chat-gpt5.4-nano-model/chatgpt_api_test_heldout_qa.ipynb
```

This experiment tests an API-based baseline on the same held-out test set.

## Evaluation

The systems were evaluated using automatic generation metrics, including lexical and semantic similarity metrics. The final comparison was performed on the same held-out test set to ensure fair baseline-vs-fine-tuned evaluation.

The key result is that fine-tuning improved the model compared with the non-fine-tuned baseline. The BM25-focused fine-tuned model achieved the best overall performance, showing that focused context selection was more effective than passing the full context directly.

## Error Analysis

The file below contains 30 selected representative failure cases:

```text
mt5-large-bm25-model/error_analysis - Selected_30.csv
```

The errors are categorized and discussed in the final report as dataset-related, model-related, or evaluation-related problems.

## Reproducibility

To reproduce the experiments:

1. Install the required Python libraries:

```bash
pip install pandas numpy torch transformers datasets evaluate rouge-score bert-score sentencepiece rank-bm25 scikit-learn
```

2. Run the preprocessing notebooks in:

```text
data extraction and processing/
```

3. Run the full-context mT5 notebook:

```text
mt5-large-model/mt5_large_full_context.ipynb
```

4. Run the BM25-focused mT5 notebook:

```text
mt5-large-bm25-model/NLP_Project_mt5_large_BM25_final.ipynb
```

5. Review the generated metrics and prediction files in the corresponding model folders.

## Notes on Checkpoints

The repository includes model configuration and tokenizer files. Full trained checkpoints may be too large for direct GitHub upload. If needed, the model can be reproduced by running the provided training notebooks with the same dataset, hyperparameters, and random seed settings documented in the notebooks.

## Submitted Separately

The following files are submitted separately from this repository:

```text
final report
final presentation
approved proposal
```
