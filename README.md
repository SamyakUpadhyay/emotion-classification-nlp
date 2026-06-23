# Emotion Classification Using NLP

A machine learning project that classifies emotions in text using Natural Language Processing. Built with a Support Vector Machine (LinearSVC) and compared against a Naive Bayes baseline, covering the full ML pipeline from raw text preprocessing to detailed error analysis and visualisation.

SDG 10 (Reduced Inequalities): Emotion-aware NLP tools can help surface under-represented voices, improve access to mental health support, and reduce communication barriers for marginalised groups.

---

## Project Overview

This notebook takes sentences written in natural language and predicts which of six emotions they express: anger, fear, joy, love, sadness, surprise.

- Primary model: LinearSVC (Support Vector Machine)
- Baseline model: Multinomial Naive Bayes
- Dataset: [Emotions Dataset for NLP](https://www.kaggle.com/datasets/praveengovi/emotions-dataset-for-nlp) by Praveengovi (Kaggle, 2020)
- Environment: Google Colab (Python 3)

---

## Repository Structure

```
Emotion_Classification_Using_NLP.ipynb
README.md
outputs/
    class_distribution.png
    hyperparameter_sensitivity.png
    learning_curve.png
    confusion_matrix.png
    confusion_matrix_enhanced.png
    per_class_metrics.png
    roc_curves.png
    top_features.png
    wordcloud_per_emotion.png
    model_comparison.png
    model_comparison_dashboard.png
    error_analysis.png
    results_summary.csv
```

---

## Pipeline

```
Raw Text -> Preprocessing -> TF-IDF Vectorisation -> Model Training -> Evaluation -> Visualisation
```

1. Install and import dependencies (NLTK, scikit-learn, matplotlib, seaborn)
2. Upload the dataset (3 split files: train.txt, val.txt, test.txt)
3. Combine and clean the dataset, removing duplicates and stripping whitespace
4. Visualise class distribution
5. Preprocess text: lowercase, remove punctuation, tokenise, remove stopwords, lemmatise
6. Split into 80% train / 20% test with stratification
7. Extract TF-IDF features (up to 30,000 unigrams and bigrams)
8. Hyperparameter sensitivity test comparing C = 0.1, 1.0, 10.0
9. Train LinearSVC with class_weight=balanced and C=1.0
10. Generate learning curve (training vs. validation F1 across 10 sizes)
11. Train Naive Bayes baseline
12. Evaluate both models on 4 metrics
13. Generate 9 visualisation figures and a full error analysis
14. Test on unseen example sentences

---

## Results

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|
| LinearSVC (SVM) | ~90% | ~90% | ~90% | ~90% |
| Naive Bayes (baseline) | ~87% | ~88% | ~87% | ~87% |

> Exact values are printed when you run the notebook. SVM outperforms Naive Bayes across all metrics, with the largest gains on minority classes (surprise, love) because of class_weight=balanced.

---

## Visualisations

The notebook generates 9 figures saved as high-resolution PNG files:

- Class distribution (bar and pie)
- Hyperparameter sensitivity (C value vs F1)
- Learning curve (training vs. validation score)
- Confusion matrices: raw and normalised, SVM and Naive Bayes
- Per-class precision, recall and F1
- ROC curves, one per emotion class with AUC scores
- Top 12 most important words per emotion class
- Word clouds per emotion class
- Full model comparison dashboard
- Error analysis: misclassification rate and confidence distribution

---

## How to Run

### Google Colab (recommended)

1. Open the notebook in [Google Colab](https://colab.research.google.com/)
2. Download the dataset from Kaggle: [Emotions Dataset for NLP](https://www.kaggle.com/datasets/praveengovi/emotions-dataset-for-nlp)
3. Run all cells in order. The notebook will prompt you to upload train.txt, val.txt and test.txt
4. Output files will be downloaded automatically at the end

### Local Jupyter

The notebook uses google.colab.files for uploading and downloading. When running locally, skip Step 3 and Step 21, and place your dataset files in a ./dataset/ folder before running Step 4.

```bash
pip install nltk scikit-learn pandas numpy matplotlib seaborn wordcloud
jupyter notebook Emotion_Classification_Using_NLP.ipynb
```

---

## Dependencies

| Library | Purpose |
|---|---|
| nltk | Tokenisation, stopwords, lemmatisation |
| scikit-learn | TF-IDF, LinearSVC, Naive Bayes, evaluation metrics |
| pandas / numpy | Data manipulation |
| matplotlib / seaborn | Visualisations |
| wordcloud | Word cloud generation |

All dependencies are installed automatically in the first cell when running on Colab.

---

## Key Design Decisions

- Stratified split: ensures every emotion class is proportionally represented in both train and test sets
- TF-IDF with bigrams: captures two-word phrases like "not happy" that single words miss
- class_weight=balanced: corrects for the imbalanced dataset where joy and sadness dominate and surprise makes up only 2-3%
- C = 1.0: chosen by testing three values and selecting the one with the best F1 score
- Calibrated SVM: wrapped in CalibratedClassifierCV to produce probability scores for ROC curves and confidence analysis

---

## Dataset

Emotions Dataset for NLP by Praveengovi (Kaggle, 2020).
Three files (train.txt, val.txt, test.txt) with semicolon-separated text and label columns.
Six emotion classes: anger, fear, joy, love, sadness, surprise.
Combined size: around 20,000 labelled sentences.

---

## Author

[Samyak Upadhyay github.com/SamyakUpadhyay, www.linkedin.com/in/samyak-upadhyay]
