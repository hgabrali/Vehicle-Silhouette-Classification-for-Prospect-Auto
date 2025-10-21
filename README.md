# 🚗 Vehicle Silhouette Classification for Prospect Auto
### 🎯 Project Goal 
The primary goal of this project is to develop and evaluate a robust multiclass classification model capable of accurately distinguishing between three distinct vehicle types—Bus, Van, and Car—based solely on their two-dimensional geometric silhouettes. This model will be used by "Prospect Auto" repair shops to automate initial vehicle identification.

## 🚗 Vehicle Classification Project: Report & Figures

### Table of Contents

* [Introduction: Data Source & Preparation](#introduction-data-source--preparation) 📄⚙️
* [1. Final Model Performance Metrics](#1-final-model-performance-metrics) 🎯
* [2. Key Findings and Interpretations](#2-key-findings-and-interpretations) 💡
* [3. Visual Summaries (Figures)](#3-visual-summaries-figures) 🖼️
    * [3.1. Performance Visuals](#31-performance-visuals) 📈
    * [3.2. Data Insights Visuals](#32-data-insights-visuals) 📊
* [Vehicle Classification: Final Analysis Report](https://github.com/hgabrali/Vehicle-Silhouette-Classification-for-Prospect-Auto/blob/main/01_Final%20Analysis%20Report.md)

## 🚀 Technical Context
 
This repository hosts a practical implementation project within the **Master School Supervised Learning curriculum**. The focus is on applying a structured machine learning pipeline to a real-world multiclass classification problem.

---

| Aspect | Description ||
| :--- | :--- | :--- |
| **Learning Module** | **Supervised Learning** | 🧠🎓 |
| **Core Task** | **Multiclass Classification** | 🏷️🎯 |
| **Key Methodologies** | Exploratory Data Analysis (EDA), Feature Scaling, Model Training (e.g., Logistic Regression, Random Forest), Multiclass Metric Evaluation (Confusion Matrix, Macro/Weighted F1 Score). | ⚙️📈 |

## 📋 Data Description

The dataset utilizes **2D geometric features** extracted from vehicle silhouettes viewed from various angles. All features are continuous and numerical.

[Statlog (Vehicle Silhouettes)](https://archive.ics.uci.edu/dataset/149/statlog+vehicle+silhouettes)

---

| Feature Type | Value Range | Details ||
| :--- | :--- | :--- | :--- |
| **Input Features** | 18 numerical columns (e.g., `compactness`, `circularity`, `hollows_ratio`). | These describe the shape of the vehicle silhouette; understanding their exact calculation is **not required**. | 📐🔢 |
| **Target Variable** (`class`) | Categorical (3 values). | `bus` (double decker), `van` (Cheverolet), or `car` (Saab 9000/Opel Manta). | 🎯🚗 |

### Export to Sheets
**Key Challenge:** While the Bus and Van are expected to be easily distinguishable, the model must handle the challenge of separating the two similar Car models.

## 🚀 Project Steps and Methodology

This project follows a standard supervised machine learning workflow, focusing on strong evaluation metrics due to the multiclass nature of the problem.

---

### Phase 1: Setup and Exploration

1.  **Import & Load Data:** Import necessary Python libraries (Pandas, NumPy, Matplotlib, Scikit-learn) and load the vehicle silhouette dataset. 💾
2.  **Exploratory Data Analysis (EDA):** Conduct comprehensive visual and numerical analysis: 🔎
    * Check for missing values, unique values, and data types.
    * Analyze the distribution of the target variable (`class`) to check for **class imbalance**.
    * Visualize feature distributions (histograms) and relationships between features and the target class.

### Phase 2: Data Preprocessing and Modeling 

1.  **Data Preparation:** Prepare the data for modeling: ⚙️
    * Separate features ($\mathbf{X}$) from the target ($\mathbf{y}$).
    * Split the dataset into **Training** and **Testing** subsets.
    * Apply **Feature Scaling** (e.g., `StandardScaler`) as all features are numerical.
2.  **Supervised Classification:** Train multiple classification models suitable for multiclass problems (e.g., Logistic Regression, kNN, Decision Trees, Random Forest). 🧠

### Phase 3: Evaluation and Conclusion

1.  **Metric Selection:** Select a robust set of metrics for multiclass classification: 📏
    * **Accuracy** (Overall performance).
    * **Confusion Matrix** (To see confusion between specific classes, particularly the two 'car' types).
    * **Precision, Recall, and F1 Score** (Averaged across classes, e.g., 'macro' or 'weighted' average, to handle potential imbalance).
2.  **Model Evaluation:** Evaluate all trained models using the selected metrics on the **Test Set**. 📈
3.  **Conclusion:** Based on the results (e.g., high F1 Score and low confusion between 'car' and other types), conclude whether the model meets "Prospect Auto's" needs for vehicle differentiation. 🎯
    * Which model performed best? Can the model reliably distinguish between the "car" class and the other two?

### 💻 Where to Work
This project is best executed in a flexible environment like Google Colab or a Jupyter Notebook.

# 📚 Resources

* [EDA](https://github.com/hgabrali/EDA)
* [PCA](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html)
* [Masterschool-Math-Foundation](https://github.com/hgabrali/Masterschool-Math-Foundation)
* [Machine-Learning](https://github.com/hgabrali/Machine-Learning)
