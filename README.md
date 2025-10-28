⸻


# 🏠 House Prices Correlation with Crime Rate and School Quality

**Department of Computer Science – Georgia State University**  
**Team Members:** Tom Dibble Dempsey, Cryon Trazona, Angel Nivar, Jack Coleman, Omar Majitov (Team Lead), Sanjib K C  
**Date:** May 3, 2025  

---

## 📘 Project Overview
This study investigates how **school quality** and **crime rates** influence **housing prices** across Atlanta ZIP codes.  
Using a combination of **statistical analysis**, **machine learning**, and **spatial visualization**, the project explores whether safety and education can predict housing market patterns.

The research integrates datasets from:
- **National Center for Education Statistics (NCES)** and six Georgia education databases  
- **Atlanta Police Department (APD)** open crime data  
- **Zillow Real Estate** datasets for housing price trends  

---

## 🎯 Objectives
1. Quantify relationships among **crime rates, school quality, and housing prices**.  
2. Identify correlations and nonlinear interactions between social factors and property values.  
3. Develop **predictive models** to estimate housing prices based on neighborhood attributes.  
4. Visualize results through geographic and statistical representations for urban analysis.

---

## 🧩 Methodology

### **1. Data Collection and Cleaning**
- Collected data from NCES, APD, and Zillow.
- Merged and geocoded records at the **ZIP code level**.
- Cleaned over **50,000 records**, handled missing data, normalized variables, and removed outliers (±3 SD).
- Used `StandardScaler` and one-hot encoding for preprocessing.

### **2. Statistical & Correlation Analysis**
- Performed **Pearson** and **Spearman** correlation tests to assess linear and non-linear relationships.
- Conducted **Exploratory Data Analysis (EDA)** using boxplots, histograms, and KDE visualizations.
- Created spatial maps with **GeoPandas** to visualize ZIP-level differences.

### **3. Machine Learning Modeling**
Implemented multiple algorithms for regression and classification:

| Model | Purpose | F1-Score | Notes |
|-------|----------|----------|-------|
| Random Forest | Nonlinear feature modeling | **0.95** | Best overall accuracy |
| K-Nearest Neighbors (KNN) | Local pattern detection | 0.90 | Tuned with k=4 |
| Neural Network | High-dimensional modeling | 0.80 | Required more tuning |
| Logistic Regression | Baseline model | 0.70 | Limited by linearity |

- **Dimensionality Reduction:** PCA and t-SNE visualized feature separability.  
- **Feature Selection:** Forward and backward selection via `SequentialFeatureSelector`.

### **4. Evaluation**
- Used **k-fold cross-validation** for reliability.  
- Analyzed **ROC curves**, **AUC scores**, and **feature importances**.  
- Built choropleth maps and spatial clusters to show high-value vs low-value ZIP codes.

---

## 🧠 Key Findings
- **School quality** strongly correlates with higher housing prices (γ ≈ 0.72).  
- **Crime rate** shows a mild **negative correlation (−0.38)** with price levels.  
- Safe areas with top-tier schools have housing prices **4.7× higher** than low-performing areas.  
- **Random Forest** proved most effective, achieving **~95% F1-score** in classifying above/below-median ZIP codes.  
- Non-linear relationships dominate, suggesting the need for advanced feature engineering.

---

## 💻 Technical Stack

| Category | Tools / Libraries |
|-----------|------------------|
| **Language** | Python 3.10 |
| **Data Handling** | pandas, NumPy |
| **Modeling** | scikit-learn |
| **Spatial Analysis** | GeoPandas |
| **Visualization** | Matplotlib, Seaborn |
| **Environment** | Jupyter Notebook, VS Code |
| **Version Control** | GitHub |

---

## 🧩 Repository Structure

├── data/
│   ├── crime_data.csv
│   ├── school_data.csv
│   ├── zillow_prices.csv
│   └── zipcodes.csv
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_EDA_visualizations.ipynb
│   ├── 03_modeling.ipynb
│   └── 04_results_and_discussion.ipynb
├── src/
│   ├── data_processing.py
│   ├── feature_selection.py
│   ├── model_training.py
│   └── visualization_utils.py
├── results/
│   ├── figures/
│   ├── model_metrics.csv
│   └── atlanta_maps/
└── README.md

---

## 🧭 How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/house-price-correlation.git
   cd house-price-correlation

	2.	Create and activate a virtual environment

python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows


	3.	Install dependencies

pip install -r requirements.txt


	4.	Run notebooks or scripts

jupyter notebook notebooks/01_data_cleaning.ipynb



⸻

📈 Results Visualization
	•	Choropleth maps display ZIP-code clustering of crime, school scores, and price distributions.
	•	ROC/AUC graphs illustrate model performance across classifiers.
	•	PCA/t-SNE visualizations confirm weak cluster separability, highlighting the non-linear nature of the data.

⸻

🔍 Future Work
	•	Integrate demographic, transit, and infrastructure datasets for finer prediction.
	•	Increase spatial granularity from ZIP codes to school zones.
	•	Explore temporal modeling to track housing trends over time.
	•	Investigate causal relationships between property taxes, school funding, and home prices.

⸻

🧑‍💼 Leadership Role – Omar Majitov
	•	Role: Team Lead & Lead Data Analyst
	•	Managed project scope, code integration, and team coordination through GitHub.
	•	Led the house price correlation and regression modeling module.
	•	Directed communication, reporting, and data integrity across all contributors.

⸻

📜 Citation

If you use this project in your research, please cite:

Majitov, O., Dempsey, T., Trazona, C., Nivar, A., Coleman, J., & K C, S. (2025). 
House Prices Correlation with Crime Rate and School Quality. Department of Computer Science, Georgia State University.


⸻

🪪 License

This project is released under the MIT License.
See the LICENSE file for details.

⸻