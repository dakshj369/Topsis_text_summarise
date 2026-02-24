# Applying TOPSIS to Select the Best Pre-Trained Text Summarization Model

## Overview

This project applies the **TOPSIS (Technique for Order Preference by Similarity to Ideal Solution)** method to rank multiple pre-trained text summarization models using a structured multi-criteria decision-making approach.

Instead of selecting a model based on a single metric (e.g., ROUGE), this project evaluates models across multiple performance and computational criteria to determine the most balanced and optimal model.

---

## Problem Statement

Selecting a pre-trained text summarization model requires balancing:

- Summary quality  
- Semantic similarity  
- Factual consistency  
- Inference speed  
- Model size  

Some metrics must be maximized (e.g., ROUGE, BERTScore), while others must be minimized (e.g., inference time, model size).

TOPSIS provides a mathematical framework to rank alternatives based on their distance from an ideal best and ideal worst solution.

---

## Models Compared

The following diversified models were selected to ensure meaningful performance differences:

- BART-large-CNN  
- PEGASUS-large  
- T5-base  
- FLAN-T5-small  
- DistilBART-CNN-12-6  

These models vary in architecture, size, and performance characteristics.

---

## Evaluation Criteria

| Criterion              | Type         | Objective |
|------------------------|-------------|------------|
| ROUGE-1                | Benefit (+) | Higher is better |
| ROUGE-L                | Benefit (+) | Higher is better |
| BERTScore              | Benefit (+) | Higher is better |
| Factual Consistency    | Benefit (+) | Higher is better |
| Inference Time (sec)   | Cost (-)    | Lower is better |
| Model Size (MB)        | Cost (-)    | Lower is better |

---

## Criteria Weights

The following weights reflect the relative importance of each criterion:

`[0.20, 0.15, 0.25, 0.20, 0.10, 0.10]`

Greater emphasis is placed on semantic and factual quality metrics while still considering computational efficiency.

Total Weight = 1.00

---

## Impact Vector

`[+, +, +, +, -, -]`

- "+" indicates benefit criteria  
- "-" indicates cost criteria  

---

## TOPSIS Methodology

The ranking process follows these steps:

1. Construct the decision matrix  
2. Normalize the matrix using vector normalization  
3. Apply weights to the normalized matrix  
4. Determine the Ideal Best and Ideal Worst solutions  
5. Compute Euclidean distances from both ideals  
6. Calculate the TOPSIS score  

Final score formula:

`Ci = S- / (S+ + S-)`

Where:

- S+ = Distance from ideal best  
- S- = Distance from ideal worst  

A higher Ci value indicates a better alternative.

---

## Project Structure

```
topsis_pretrained/
│
├── data/
│   └── decision_matrix.csv
│
├── notebook/
│   └── analysis.ipynb
│
├── output/
│   ├── closeness_bar_chart.png
│   ├── rouge_comparison.png
│   ├── inference_time_comparison.png
│   └── normalized_heatmap.png
│
├── results/
│   └── topsis_scores.csv
│
└── README.md
```

---

## Visualization

### Model Ranking

The closeness coefficient for each model is plotted to visualize the final ranking.

[Closeness Chart](./output/closeness_bar_chart.png)

### Normalized Decision Matrix Heatmap

The heatmap shows the normalized values of each criterion across models.

[normalised Heatmap](./output/normalized_heatmap.png)

---

## Results

The complete TOPSIS scores and ranking are available in:

`results/topsis_scores.csv`

The model with the highest TOPSIS score is considered the most balanced solution, considering both summarization quality and computational efficiency.

---

## How to Run

1. Install dependencies:

`pip install numpy pandas matplotlib`

2. Open the notebook:

`jupyter notebook notebook/analysis.ipynb`

3. Run all cells to:

- Load the decision matrix  
- Apply TOPSIS  
- Generate ranking scores  
- Save intermediate matrices  
- Produce visualization plots  

---

## Why TOPSIS?

- Handles conflicting criteria effectively  
- Provides objective mathematical ranking  
- Balances performance and computational constraints  
- Suitable for practical model selection problems  

---

## Key Insight

While larger transformer models achieve slightly higher ROUGE and semantic scores, smaller and distilled models often provide better trade-offs between performance and efficiency.

TOPSIS helps identify the best compromise solution rather than optimizing a single metric.

