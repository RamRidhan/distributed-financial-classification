# Distributed Financial Classification Using Fundamental and Macroeconomic Data

## Overview
This project builds a **distributed machine learning pipeline** to classify **S&P 500 stocks** into benchmark-relative performance categories using a combination of **firm-level fundamentals** and **macroeconomic indicators**.

The core focus is on **scalability, robustness, and interpretability** when working with **large, high-dimensional financial datasets**.  
The pipeline is implemented using **Apache Spark on Google Cloud Dataproc**, enabling efficient preprocessing and model training on **146,000+ observations**.

---

## Problem Statement
Classifying stock performance using financial and macroeconomic data is challenging due to:

- Large data volume and heterogeneous feature sets  
- Strong class imbalance across performance categories  
- Non-linear relationships between variables  
- Practical limitations of single-node computation  

This project addresses these challenges by combining **distributed computing** with **modern ML techniques**, while maintaining **transparent, reproducible workflows** suitable for real-world analysis.

---

## Data
The dataset integrates two complementary sources:

**Firm-level fundamentals**
- Liquidity, leverage, profitability, and valuation ratios  

**Macroeconomic indicators**
- Growth, inflation, labour market, and interest-rate signals  

**Scale**
- ~146,000 observations  
- 42 continuous input features  
- Monthly and quarterly frequencies  
- Coverage: **2009–2024**

📎 **Public dataset (Kaggle):**  
https://www.kaggle.com/datasets/laxmansudhan25002/st446-macroeconomic-and-fundamental-data/data

---

## Target Variable
Stocks are classified into **five benchmark-relative performance categories** based on returns relative to the S&P 500:

- Strong underperformance  
- Slight underperformance  
- Neutral performance  
- Slight outperformance  
- Strong outperformance  

This **multi-class formulation** captures more nuanced performance differences than binary labels and aligns closely with **portfolio attribution and risk analysis**.

---

## Methodology

### Distributed Architecture
- **Apache Spark** on **Google Cloud Dataproc**
- Multi-node clusters for parallel preprocessing and training
- Spark DataFrames used end-to-end to avoid memory bottlenecks

### Data Engineering
- API-based extraction of macroeconomic indicators  
- Distributed joins and schema validation  
- Missing-value handling and feature pruning  
- Unified dataset construction in Spark  

### Modeling
Eight supervised models were implemented and evaluated:

- **Classical baselines:** Logistic Regression, Decision Tree, Random Forest  
- **Gradient-based models:** GBTClassifier, XGBoost, LightGBM  
- **Automated modeling:** H2O AutoML  
- **Ensemble:** F1-weighted model fusion  

Class imbalance was addressed using **oversampling** where appropriate.

---

## Evaluation
Models were evaluated using:

- Accuracy, Precision, Recall, F1-score  
- Confusion matrices  
- Resource metrics (training time, CPU, memory usage)  
- **SHAP analysis** for model interpretability  

---

## Key Results
- **H2O AutoML** achieved the strongest overall performance (**F1 ≈ 0.89**)  
- **LightGBM** delivered the best accuracy-efficiency trade-off, training in **~35 seconds** on a 3-node cluster  
- Increasing cluster size reduced training time by **up to 18%**  
- SHAP analysis highlighted **macroeconomic variables** (e.g. CPI, interest rates) as key drivers alongside firm fundamentals  

These results demonstrate how **distributed computing enables scalable, interpretable financial classification** without sacrificing analytical rigor.

---

## Limitations
- Class imbalance remains challenging despite oversampling  
- AutoML models are resource-intensive in distributed environments  
- Results focus on S&P 500 stocks and may not directly generalise to smaller or international markets  

---

## Future Work
- More efficient handling of class imbalance at scale  
- Improved temporal alignment between macro and firm-level data  
- Exploration of lighter-weight ensemble strategies for near real-time use  

---

## Notes
This repository contains a **cleaned and independent version** of work originally developed as part of a collaborative academic project.

All **code, structure, and documentation** have been adapted for **clarity, reproducibility, and professional use**.
