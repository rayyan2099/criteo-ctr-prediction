# Dataset

This project uses the **CriteoPrivateAd** dataset released by Criteo.

**Dataset:** :contentReference[oaicite:0]{index=0}

## Description

CriteoPrivateAd is a large-scale, anonymized real-world online advertising dataset designed for research on click-through rate (CTR) prediction and privacy-preserving advertising systems. It contains production-derived bidding logs with engineered features suitable for training machine learning models under realistic advertising constraints. :contentReference[oaicite:1]{index=1}

## Download

You can download the dataset directly from the Hugging Face dataset page:

```bash
git lfs install
git clone https://huggingface.co/datasets/criteo/CriteoPrivateAd
```

Alternatively, use the Hugging Face Python library:

```python
from datasets import load_dataset

dataset = load_dataset("criteo/CriteoPrivateAd")
```

## Placement

After downloading, place the dataset files inside the `data/` directory (or update the notebook paths accordingly).

Example:

```
data/
├── train.parquet
├── validation.parquet
├── test.parquet
└── README.md
```

> **Note:** The dataset is **not included** in this repository because of its size. Please download it directly from the official Hugging Face repository.

## Citation

If you use this dataset in your work, please cite:

> Sebbar et al. *CriteoPrivateAd: A Real-World Bidding Dataset to Design Private Advertising Systems*, 2025. :contentReference[oaicite:2]{index=2}