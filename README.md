# Reading Level Text Classification
This project explores whether a modern language model can classify short fiction passages into three educational reading levels: Elementary, Middle, and High School.

## Repo Structure
```

reading-level-classification
├── data/
│   ├── fiction.csv         # dataset of fiction passages
│   ├── id_df.csv           # in-domain results from final model
│   ├── nonfiction.csv      # dataset of nonfiction passages
│   └── ood_df.csv          # out-of-domain results from final model
├── .gitignore
├── README.md
├── analysis.ipynb          # contains analysis/visualizations of final model results
├── notebook.ipynb          # contains code for model training and testing
└── requirements.txt

```

## Research Question
How effectively can a language model (e.g., DistilBERT) classify fictional text passages by educational reading level?

## Motivation
Traditional readability formulas (i.e., Flesch-Kincaid, SMOG) rely on surface-level features like word and sentence length. However, these metrics don't capture deeper aspects of writing such as:
- vocabulary difficulty
- sentence structure and syntax
- abstract vs. concrete ideas

Transformer models use contextual embeddings and may detect these deeper, subtler patterns more effectively.

## Dataset
Because no suitable public dataset exists, we built our own:

**Fiction Dataset (Training/Validation)**
- Extracted from U.S. school reading lists
- 50 passages per text
- Labels: Elementary, Middle, High
- 5,000+ balanced samples

**Nonfiction Dataset (Out-of-Domain Testing)**
- Nonfiction books, educational articles, biographies
- 50 passages per text
- 2,000+ balanced samples
- Used only for testing generalization

## Models Tested
We compared several pretrained transformer models:
- RoBERTa-large
- DistilBERT
- XLNet-case
- ERNIE 2.0

We chose **DistilBERT** for final training because it provided the best balance of loss, accuracy, and training speed, without overfitting to the training set.

## Classification Approach
1. Fine-tune each model on the labeled fiction dataset
2. Predict: Elementary (0), Middle (1), or High (2) School
3. Test model on held-out fiction test set
4. Evaluate generalization on nonfiction passages
5. Error analysis to understand misclassifications

## Evaluation
We report:
- Accuracy
- F-1 Score
- Precision
- Recall
- Confusion Matrix
- Matthews Correlation Coefficient (MCC)

## Out-of-Domain Analysis
After training on fictional text, the DistilBERT model was tested on nonfiction passages to explore robustness and genre transfer.

## Reproducing the Model
All code for data processing, model preparation, model training, and evaluation is contained in two Jupyter notebooks. To reproduce the results:
1. Clone the repository
```
git clone https://github.com/broooklynp/reading-level-classification.git
```
2. Open the Notebooks

``
notebook.ipynb
``
and
``
analysis.ipynb
``

4. Run All Cells
The notebooks will:
- Load and preprocess both datasets
- Fine-tune each tested model (DistilBERT, RoBERTa, ERNIE, XLNet)
- Generate evaluation metrics
- Run out-of-domain tests
- Error analysis

No additional scripts or setup is needed.
