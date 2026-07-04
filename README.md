# Criteo Click-Through Rate Prediction

An end-to-end implementation of a **Hybrid Gradient Boosted Decision Tree (GBDT) + Logistic Regression (LR)** click-through rate (CTR) prediction model inspired by Facebook's paper **"Practical Lessons from Predicting Clicks on Ads at Facebook"**.

The project reproduces several key ideas from the paper, including feature transformation using tree leaf indices, negative downsampling, and probability recalibration, using the **CriteoPrivateAd** dataset.

---

## Project Overview

Online advertising platforms must estimate the probability that a user clicks on an advertisement (CTR). Accurate CTR prediction directly impacts ad ranking, bidding strategies, and revenue.

This project builds a production-style CTR prediction pipeline consisting of:

- LightGBM for learning non-linear feature interactions
- Tree leaf extraction as learned categorical features
- One-hot encoding of leaf indices
- Logistic Regression as the final probabilistic classifier
- Negative downsampling for efficient training
- Probability recalibration after downsampling
- Evaluation using AUC and Log Loss

---

## Model Pipeline

```
Raw Features
      │
      ▼
 LightGBM (GBDT)
      │
      ▼
 Leaf Indices
      │
      ▼
 One-Hot Encoding
      │
      ▼
 Logistic Regression
      │
      ▼
 CTR Probability
```

---

## Dataset

This project uses the **CriteoPrivateAd** dataset.

Dataset download instructions can be found in:

```
data/README.md
```

The dataset is **not included** in this repository because of its size.

---

## Experiments

The notebook evaluates the effect of **negative downsampling** on prediction quality and training time.

| Sampling Rate | Train Size | AUC | Log Loss | Training Time |
|--------------:|-----------:|----:|---------:|--------------:|
| 1.00 | 1,600,000 | 0.7376 | 0.1300 | 58.5 s |
| 0.50 | 825,825 | 0.7375 | 0.1301 | 34.1 s |
| 0.25 | 438,738 | 0.7366 | 0.1303 | 23.3 s |
| 0.10 | 206,485 | 0.7335 | 0.1308 | 13.6 s |

### Key Findings

- Hybrid GBDT + Logistic Regression effectively models non-linear feature interactions.
- Moderate negative downsampling significantly reduces training time with minimal impact on predictive performance.
- Probability recalibration restores calibrated CTR estimates after downsampling.
- AUC remains relatively stable until aggressive downsampling is applied.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- LightGBM
- Matplotlib
- Jupyter Notebook

---

## Repository Structure

```
.
├── notebooks/
│   └── Criteo_CTR_Prediction.ipynb
│
├── data/
│   └── README.md
│
├── README.md
└── .gitignore
```

---

## Future Improvements

- Hyperparameter optimization
- Comparison with standalone Logistic Regression and LightGBM models
- Online learning experiments
- Feature importance analysis
- Cross-validation
- Model deployment using FastAPI

---

## References

1. He, X., Pan, J., Jin, O., Xu, T., Liu, B., Xu, T., Shi, Y., Atallah, A., Herbrich, R., Bowers, S., & Quiñonero Candela, J. (2014).

**Practical Lessons from Predicting Clicks on Ads at Facebook**

https://dl.acm.org/doi/10.1145/2648584.2648589

2. Criteo

**CriteoPrivateAd Dataset**

https://huggingface.co/datasets/criteo/CriteoPrivateAd
