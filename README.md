# OilyGiant — Oil Well Selection with Risk Analysis 🛢️📊

This project selects the **best region** to develop **200 new oil wells** under strict business constraints.
We train a **Linear Regression** model to predict reserve volume (`product`), then use **bootstrapping** to estimate profit uncertainty and the **risk of loss**.

---

## Goal 🎯

Choose the region that:
- Keeps **loss probability < 2.5%** ✅
- Maximizes **expected profit** 💰

---

## Business assumptions 💵

- Total budget: **$100,000,000**
- Wells to develop: **200**
- Exploration points per region: **500**
- Revenue per unit of `product`: **$4,500**
- Minimum production threshold (break-even): **111.1 units** *(derived in the notebook)*

---

## Approach 🧩

1) **Modeling**
- Train a **Linear Regression** model per region to predict `product`.

2) **Well selection**
- For each region, take the **top 200 predicted wells** out of 500 exploration points.

3) **Profit calculation**
- Compute profit from the selected wells using the business constants.

4) **Bootstrapping (risk) 🎲**
- Repeat the selection/profit process many times (resampling) to estimate:
  - Average profit
  - Confidence interval (2.5% / 97.5% quantiles)
  - Probability of loss

---

## Model performance (validation) 🧪

| Region | RMSE | R² |
|---|---:|---:|
| geo_data_0 | 37.6834 | 0.2738 |
| geo_data_1 | 0.8923 | 0.9996 |
| geo_data_2 | 40.1525 | 0.2023 |


> Region `geo_data_1` shows dramatically lower RMSE and very high R² compared to the others.

---

## Profit & risk results (bootstrapping) 📈

| Region | Avg profit (USD) | 2.5% quantile | 97.5% quantile | Loss probability | ROI | Effective ROI |
|---|---:|---:|---:|---:|---:|---:|
| geo_data_0 | $4,089,561.93 | $-963,570.86 | $9,616,291.73 | 5.20% | 4.09% | 3.88% |
| geo_data_1 | $4,714,887.65 | $523,824.95 | $9,114,850.35 | 1.20% | 4.71% | 4.66% |
| geo_data_2 | $4,209,020.14 | $-1,403,231.64 | $9,343,215.56 | 7.40% | 4.21% | 3.90% |


✅ **Recommended region:** `geo_data_1`  
- Avg profit: **$4,714,887.65**
- Loss probability: **1.20%** *(meets the <2.5% requirement)*

---

## Tech stack 🛠️
- Python
- pandas, NumPy
- scikit-learn
- matplotlib

---

## How to run ▶️

1) Install dependencies:
```bash
pip install -r requirements.txt
```
