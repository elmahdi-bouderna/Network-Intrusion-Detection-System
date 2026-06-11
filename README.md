# Deep Learning-Based Network Intrusion Detection System (NIDS)

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![LaTeX](https://img.shields.io/badge/LaTeX-Document-green.svg)](https://www.latex-project.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the code, data preprocessing notebooks, and the final LaTeX report for the **Deep Learning Network Intrusion Detection System (NIDS)** mini-project. The project evaluates classical machine learning models, deep learning architectures (1D CNN, BiLSTM, MLP), and hybrid ensemble techniques on two benchmark datasets: **NSL-KDD** and **CSE-CIC-IDS2018**.

---

## 👥 Authors & Supervision

* **Students:**
  * **EL MAHDI BOUDERNA**
  * **Yassine Mounabih**
  * **Yassine EL Hattab**
* **Supervisor:** **Prof. Youness Abouqora**
* **Institution:** École Nationale des Sciences Appliquées -- El Jadida (ENSA El Jadida), Université Chouaib Doukkali
* **Program:** Master in Data Science and Artificial Intelligence (SDIA)
* **Module:** Deep Learning

---

## 📂 Repository Structure

```directory
├── Network Intrusion Detection NSL-KDD.ipynb                        # Data preprocessing, training, and evaluation on NSL-KDD
├── Network Intrusion Detection CSE-CIC-IDS2018-00-Cleaning.ipynb   # Cleaning, filtering, and balancing the CSE-CIC-IDS2018 dataset
├── README.md                                                        # Repository documentation
└── Report/                                                          # LaTeX report source files
    ├── main.tex                                                     # Main LaTeX document
    ├── main.pdf                                                     # Compiled French report (25 pages)
    ├── ucd.png & ensa.png                                           # Institution logos for the cover page
    └── figures/                                                     # Output plots, confusion matrices, and diagrams
```

---

## 🔬 Project Overview & Methodology

The objective of this project is to implement a robust and adaptive NIDS capable of identifying network anomalies and cyber-attacks.

### 1. Data Preprocessing & Cleaning
- **NSL-KDD:** Class mapping (binary classification), label/one-hot encoding of categorical variables (`protocol_type`, `service`, `flag`), standard scaling, and sequence reshaping for deep learning inputs.
- **CSE-CIC-IDS2018:** Concatening parquet partitions, removing invalid entries (NaNs/Infs), downsampling to 1,000,000 records, filtering rare classes to form a structured **10-class** problem, and applying stratified train/val/test splits.

### 2. Evaluated Models
* **Classical ML:** Random Forest, Decision Tree, Support Vector Machine (SVM), K-Nearest Neighbors (KNN), Logistic Regression, Naive Bayes, AdaBoost, Gradient Boosting, LightGBM, and XGBoost.
* **Deep Learning:**
  * **1D CNN:** Designed to capture local spatial correlations across network statistics.
  * **BiLSTM:** Leverages bi-directional sequence context (evaluated and compared against feed-forward networks).
  * **MLP:** A deep feed-forward network serving as a fast, parameter-efficient baseline.
* **Ensemble Hybrids:**
  * **Soft-Voting Ensemble (XGBoost + RF + MLP):** Leverages decision boundaries of different model families.
  * **Feature Stacking (XGBoost + CNN):** Combines CNN features with tree-based prediction probabilities.

---

## 📈 Key Results

Detailed metrics and confusion matrices can be found in the [Report/main.pdf](file:///c:/Users/hp/Desktop/IDS%20PRO/Report/main.pdf).

### NSL-KDD (Binary Classification)
| Model / Ensemble | Accuracy | F1-Score | Recall (Attack) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| **XGBoost + RF + MLP (Soft Voting, $\tau = 0.25$)** | **90.2%** | **0.892** | **85.3%** | **Best performance; limits false negatives** |
| Gradient Boosting | 80.6% | 0.800 | 68.2% | High precision, conservative recall |
| 1D CNN | 79.8% | 0.785 | 70.1% | Evaluated with tuned decision threshold |
| BiLSTM | 79.9% | 0.782 | 68.9% | Computationally heavy compared to CNN |

### CSE-CIC-IDS2018 (10-Class Classification)
* **1D CNN (Keras-Tuned):** Reached **97.98%** accuracy on the test set.
* **MLP:** Reached **97.97%** accuracy, completing training in only **~1s/epoch** (preferred choice for production deployment due to efficiency).
* **BiLSTM:** Underperformed at **67.17%**, confirming that sequence-based models mismatch tabular flow-level network statistics where time ordering is not present.
* **Infiltration Attack Challenge:** Remained the most difficult attack category to detect (F1 0.08–0.17) due to its stealth profile mimicking benign network traffic.

---

## 🚀 Getting Started

### Prerequisites

You will need the following libraries installed:
```bash
pip install numpy pandas scikit-learn tensorflow xgboost lightgbm jupyter matplotlib seaborn
```

### Running the Notebooks
1. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
2. Run `Network Intrusion Detection CSE-CIC-IDS2018-00-Cleaning.ipynb` to download, clean, and export the preprocessed 10-class subset of CSE-CIC-IDS2018.
3. Run `Network Intrusion Detection NSL-KDD.ipynb` to train and evaluate all baseline ML, deep learning models, and hybrid ensembles on NSL-KDD.

### Compiling the Report
The final report is written in LaTeX. To compile it yourself:
```bash
cd Report
pdflatex main.tex
pdflatex main.tex
```

---

## 📝 License
This project is licensed under the MIT License - see the LICENSE file for details.
