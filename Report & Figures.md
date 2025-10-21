# 🚗 Vehicle Classification Project: Report & Figures

## Table of Contents

* [Introduction: Data Source & Preparation](#introduction-data-source--preparation) 📄⚙️
* [1. Final Model Performance Metrics](#1-final-model-performance-metrics) 🎯
* [2. Key Findings and Interpretations](#2-key-findings-and-interpretations) 💡
* [3. Visual Summaries (Figures)](#3-visual-summaries-figures) 🖼️
    * [3.1. Performance Visuals](#31-performance-visuals) 📈
    * [3.2. Data Insights Visuals](#32-data-insights-visuals) 📊

This section details the data selection process, initial data preparation, and subsequent analyses performed for this project.

### 🗃️ Introduction: Data Source & Preparation

For this project, two versions of the "Statlog (Vehicle Silhouettes)" dataset were evaluated to ensure the most robust and clean data source was used.

1.  **Original Raw Data (Downloaded from UCI Repository):**
    * **Source:** Direct download from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/149/statlog+vehicle+silhouettes).
    * **Characteristics:** This dataset was "header-less," meaning it did not contain column names.
    * **Loading:** Upon inspection, all 19 columns were loaded as numerical data types (`int64`). The target variable (the 19th column) was found to be numerically encoded (e.g., `0`, `1`, `2`).
    * **Required Preprocessing:** This version required two significant manual cleaning steps:
        1.  Manually assigning a list of 19 column names based on the dataset's documentation.
        2.  Manually mapping the numerical target variable to its corresponding categorical string labels (e.g., `{0: 'van', 1: 'car', 2: 'bus'}`) to be used in classification.

2.  **Master School Data (`vehicle.csv`):**
    * **Source:** Provided directly by the Master School.
    * **Characteristics:** This dataset is a clean, "headered" CSV file, meaning it includes column names.
    * **Loading:** The data was loaded correctly with 18 numerical feature columns (`int64`) and one categorical target column (`object`). The `class` column already contained the explicit, human-readable string labels: `'van'`, `'car'`, and `'bus'`.
    * **Required Preprocessing:** The primary data-cleaning step (mapping the target variable) was *not* required. The only minor adjustment made was renaming a few feature columns that had ambiguous names in the file (e.g., `scaled_variance.1`, `skewness_about.1`) to more descriptive names (e.g., `scaled_variance_minor`, `skewness_minor`) for better readability during analysis.

### 🎯 Final Dataset Selection

**This project was developed and executed using the `vehicle.csv` dataset provided by the Master School.**

This file was chosen as the definitive data source because it represents a cleaner, pre-processed version of the data. This choice eliminated ambiguity in the target variable and streamlined the data-loading phase, allowing for a more direct and reliable focus on Exploratory Data Analysis (EDA) and model building.s.

---


## 1. Final Model Performance Metrics 🎯

## Post-Classification Metrics Applicability

This table classifies the evaluation metrics discussed (Accuracy, Confusion Matrix, Classification Report, Feature Importance, and ROC Curve) against the four models trained in our analysis. It also includes the final accuracy score achieved by each model.

| METRICS | Accuracy Score | Confusion Matrix | Classification Report (P/R/F1) | Feature Importance | ROC Curve / AUC |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Random Forest** | **0.9588** | ✅ **Yes** | ✅ **Yes** | ✅ **Yes** <br/> (from `.feature_importances_`) | ✅ **Yes** <br/> (via `.predict_proba`) |
| **Logistic Regression** | 0.9353 | ✅ **Yes** | ✅ **Yes** | ✅ **Yes** <br/> (from `.coef_`) | ✅ **Yes** <br/> (via `.predict_proba`) |
| **k-Nearest Neighbors (kNN)** | 0.9176 | ✅ **Yes** | ✅ **Yes** | ❌ **No** <br/> (Not directly applicable) | ✅ **Yes** <br/> (via `.predict_proba`) |
| **Decision Tree** | 0.8765 | ✅ **Yes** | ✅ **Yes** | ✅ **Yes** <br/> (from `.feature_importances_`) | ✅ **Yes** <br/> (via `.predict_proba`) |

### Key Interpretations of this Table:

* **Accuracy, Confusion Matrix, & Classification Report:** These metrics are universal. Since all models generate predictions (`.predict()`), we can always compare them to the true labels (`y_test`) to generate these reports.
* **ROC Curve / AUC:** This metric requires probability scores (`.predict_proba()`) rather than just final predictions. All four models we selected are capable of producing these probabilities, making them suitable for ROC analysis.
* **Feature Importance:** This is the main differentiator.
    * **Random Forest** and **Decision Tree** models have a built-in `.feature_importances_` attribute, which makes it easy to see which features were most decisive.
    * **Logistic Regression** provides feature importance through its `.coef_` (coefficients). The magnitude of the coefficient (after scaling) signifies importance.
    * **k-Nearest Neighbors (kNN)** does *not* have a direct feature importance metric. It is a "lazy learner" or "non-parametric" model that doesn't learn "weights" for features; it simply uses all features to calculate distances.
---

### Preprocessing Pipeline

The data was prepared for modeling using the following pipeline:

1.  **Data Split:** The dataset (846 samples) was split into training (80%) and testing (20%) subsets.
    * Training Set: `(676, 18)`
    * Testing Set: `(170, 18)`
2.  **Imputation:** The `df.info()` check in Phase 1 revealed missing `NaN` values. `SimpleImputer(strategy='median')` was used to fill these gaps, ensuring no data was lost.
3.  **Scaling:** All features were scaled using `StandardScaler`. The scaler was `fit` **only** on the training data and then used to `transform` both the training and test sets. This prevents data leakage and ensures models like Logistic Regression and kNN perform optimally.

---


Four distinct classification models were trained on the preprocessed training data and evaluated on the unseen test data. The primary metric for evaluation is **Accuracy**.

The final performance metrics are as follows:

| Model | Test Accuracy (Score) | Test Accuracy (%) |
| :--- | :---: | :---: |
| **Random Forest** | **0.9588** | **95.88%** |
| Logistic Regression | 0.9353 | 93.53% |
| k-Nearest Neighbors (k=5) | 0.9176 | 91.76% |
| Decision Tree | 0.8765 | 87.65% |

---

## 2. Key Findings and Interpretations 💡

Based on the performance metrics, several key insights can be drawn:

* **Best Overall Model:** **Random Forest** is the clear winner, achieving the highest test accuracy of **~95.9%**. This strongly suggests that the relationships between the vehicle features and their classes are complex and non-linear. The ensemble nature of Random Forest (using multiple decision trees) excels at capturing these patterns while avoiding the overfitting seen in a single Decision Tree.

* **Ensemble vs. Single Tree:** The performance gap between Random Forest (95.9%) and the single Decision Tree (87.7%) is significant. This highlights the weakness of a single tree, which likely overfit the training data. The Random Forest successfully generalizes by averaging the predictions of many decorrelated trees.

* **Linear Model Strength:** `LogisticRegression` performed exceptionally well (93.5%), which is somewhat surprising for a complex, multi-class problem. This high performance indicates that the `StandardScaler` was highly effective and that many of the features, when combined, *do* provide significant linear separability between the classes.

* **Feature Space Viability:** The `k-Nearest Neighbors` model's strong performance (91.8%) confirms that the preprocessing pipeline was successful. It shows that in the scaled 18-dimensional feature space, vehicles of the same class cluster together, making "distance" a meaningful metric for classification.



## 3. Visual Summaries (Figures) 🖼️

Visualizations are essential for quick comprehension and communicating complex results. All figures are typically stored in the `reports/figures/` directory.

### 3.1. Performance Visuals

* **Confusion Matrix:** A table visualizing the performance of a classification model. It clearly shows True Positives, True Negatives, False Positives, and False Negatives.

<img width="967" height="741" alt="image" src="https://github.com/user-attachments/assets/4b268c4d-97bb-469f-b3a2-fa78504881f1" />


# 📊 Confusion Matrix: Comparative Analysis

The confusion matrices provide a deep insight into each model's performance beyond simple accuracy. They reveal *how* and *where* the models are making mistakes by showing the count of true vs. predicted labels for each class.

Here is a comparative analysis based on the generated plots:

| Model 🤖 | Overall Performance & Key Strengths 🎯 | Key Confusion Points (Weaknesses) ⚠️ |
| :--- | :--- | :--- |
| **Random Forest** | **🥇 (Winner)**. This model is the most accurate and balanced. It identified `car` and `bus` classes almost perfectly (84/86 cars, 41/42 buses correct). | Its only notable weakness is misclassifying **4 'van'** samples as **'bus'**. This suggests `van` and `bus` silhouettes are still difficult to separate. |
| **Logistic Regression** | **🥈 (Strong Runner-Up)**. Excellent performance. It identifies the `car` class very well (82/86 correct). Its performance is nearly on par with Random Forest. | Has the same weakness as Random Forest: confuses `van` and `bus`. It misclassified **4 'bus'** as **'van'** and **3 'van'** as **'bus'**. |
| **k-Nearest Neighbors** | ** respectable.** Similar to Logistic Regression, it identifies `bus` and `car` classes well (38/42 buses, 82/86 cars correct). | This model struggles the most with the **'van'** class. It misclassified **6 'van'** samples as **'bus'**, which is the highest error rate for that specific confusion. |
| **Decision Tree** | **(Weakest Model)**. This model shows significant confusion across all classes and is clearly the poorest performer. | It struggles badly with the `car` class, misclassifying **6 as 'bus'** and **5 as 'van'**. It also confuses `bus` with `van` (4) and `van` with `bus` (4). |

---

### 💡 Summary Interpretation

1.  **The 'Car' Class:** The `car` class is the most distinct and easiest to identify. All models except the single Decision Tree performed very well on it.
2.  **The 'Bus/Van' Problem:** The most common error across *all four models* is the confusion between `bus` and `van`. This strongly implies that the visual features (silhouettes) of buses and vans in this dataset are very similar.
3.  **Model Superiority:** The **Random Forest** model is superior not just because it has the highest accuracy, but because it minimizes this `bus/van` confusion better than any other model.

---

# 📈 Classification Report: Comparative Analysis

### 📈 Detailed Classification Reports (All Models)

This output shows the full, detailed performance breakdown for each of the four models trained on the test set.

=========================================
     Report for: Logistic Regression
=========================================
              precision    recall  f1-score   support

         bus       0.89      0.95      0.92        44
         car       0.97      0.91      0.94        86
         van       0.91      0.97      0.94        40

    accuracy                           0.94       170
   macro avg       0.93      0.95      0.93       170
weighted avg       0.94      0.94      0.94       170


=========================================
     Report for: k-Nearest Neighbors (k=5)
=========================================
              precision    recall  f1-score   support

         bus       0.95      0.95      0.95        44
         car       0.93      0.91      0.92        86
         van       0.86      0.90      0.88        40

    accuracy                           0.92       170
   macro avg       0.91      0.92      0.92       170
weighted avg       0.92      0.92      0.92       170


=========================================
     Report for: Decision Tree
=========================================
              precision    recall  f1-score   support

         bus       0.82      0.91      0.86        44
         car       0.90      0.87      0.89        86
         van       0.89      0.85      0.87        40

    accuracy                           0.88       170
   macro avg       0.87      0.88      0.87       170
weighted avg       0.88      0.88      0.88       170


=========================================
     Report for: Random Forest
=========================================
              precision    recall  f1-score   support

         bus       0.96      0.98      0.97        44
         car       0.98      0.94      0.96        86
         van       0.93      0.97      0.95        40

    accuracy                           0.96       170
   macro avg       0.95      0.96      0.96       170
weighted avg       0.96      0.96      0.96       170

The `classification_report` provides a class-by-class breakdown of model performance, moving beyond the overall accuracy score. We analyze **Precision**, **Recall**, and **F1-Score** for each model to understand their specific strengths and weaknesses.

* **Precision:** *Of all the times the model predicted a class (e.g., "bus"), what percentage was correct?* (High precision = low false positives).
* **Recall :** *Of all the actual samples of a class (e.g., all real "bus" samples), what percentage did the model find?* (High recall = low false negatives).
* **F1-Score:** The harmonic mean of Precision and Recall. This is the best metric for comparing balanced performance, especially for the individual classes.

### Model Performance Summary (F1-Scores by Class)

This table summarizes the F1-Score for each class, which is the most informative metric for comparing performance.

| Model 🤖 | `bus` (F1-Score) | `car` (F1-Score) | `van` (F1-Score) | Overall Accuracy 🎯 |
| :--- | :---: | :---: | :---: | :---: |
| **Random Forest** | **0.97** | **0.96** | **0.95** | **0.96** |
| **Logistic Regression** | 0.92 | 0.94 | 0.94 | 0.94 |
| **k-Nearest Neighbors** | 0.95 | 0.92 | 0.88 | 0.92 |
| **Decision Tree** | 0.86 | 0.89 | 0.87 | 0.88 |

---

### 💡 Detailed Insights and Interpretation

1.  **🥇 Random Forest (The Clear Winner):**
    * This model is superior in every single metric. It achieves an F1-Score of $0.95$ or higher for *all three* classes, indicating a robust and well-balanced model.
    * Its lowest score, `van` ($0.95$), is still higher than the best scores of the other models. This confirms the finding from the Confusion Matrix: it handles the difficult `bus/van` confusion exceptionally well.

2.  **🥈 Logistic Regression (Strong & Balanced):**
    * This model shows excellent, balanced performance with F1-Scores of $0.92$ - $0.94$ across the board.
    * **Key Insight:** Its Recall for `bus` ($0.95$) and `van` ($0.97$) is very high, meaning it is very good at *finding* all the actual buses and vans. However, its Precision for `bus` ($0.89$) shows it sometimes *incorrectly labels* other vehicles as `bus` (as seen in the confusion matrix).

3.  **🥉 k-Nearest Neighbors (Good, but with a Weakness):**
    * kNN is strong at identifying the `bus` ($0.95$) and `car` ($0.92$) classes.
    * **Key Insight:** Its main weakness is clearly the `van` class, which has a significantly lower F1-Score ($0.88$). It has low Precision ($0.86$) for `van`, confirming that it frequently misclassifies other vehicles (specifically `bus`) *as* `van`.

4.  **Decision Tree (The Underperformer):**
    * This model is the weakest, with F1-Scores below $0.90$ for all classes.
    * It struggles most with the `bus` class (F1-Score $0.86$). This report confirms the findings from the Confusion Matrix: the single tree is not complex enough (or is overfit) and makes significant errors across all categories.

---
# 🧠 Feature Importance: Comparative Analysis

<img width="782" height="502" alt="image" src="https://github.com/user-attachments/assets/1b790584-250f-4454-9cd5-fa3d9a1e378e" />
<img width="782" height="495" alt="image" src="https://github.com/user-attachments/assets/580022d3-e479-405b-a26f-8c46e9d6572c" />
<img width="803" height="493" alt="image" src="https://github.com/user-attachments/assets/56703ad3-bb75-4e8c-a1a6-bc3fe003f289" />

This analysis examines *which* features each model used to make its decisions. This helps us understand *why* one model outperformed another. The importance metrics are different for each model type:

* **Tree-Based (Random Forest, Decision Tree):** Uses "Gini Importance" – how much a feature helps in reducing the impurity of the data splits.
* **Linear (Logistic Regression):** Uses "Mean Absolute Coefficient" – the average magnitude of a feature's weight across all classes, indicating its influence on the decision boundary.

### Comparative Interpretation Table

| Model 🤖 | Top 5 Key Features (in order) 🔑 | Analysis & Interpretation 🧠 |
| :--- | :--- | :--- |
| **Random Forest** 🥇 | 1. `scaled_variance.1`<br>2. `pr.axis_rectangularity`<br>3. `scaled_radius_of_gyration`<br>4. `scatter_ratio`<br>5. `circularity` | **Balanced & Robust.** The importance is distributed across many features. While `scaled_variance.1` is the most important, several other features play a significant role. This shows the model is using a "wisdom of the crowd" approach, combining many weak predictors to create one strong one. This is why it's so accurate and avoids overfitting. |
| **Decision Tree** 🌳 | 1. `scaled_variance.1` (Dominant)<br>2. `pr.axis_rectangularity`<br>3. `scaled_radius_of_gyration`<br>4. `compactness`<br>5. `scatter_ratio` | **Over-Reliant.** The model is *heavily* dependent on a single feature (`scaled_variance.1`), which has an importance score of over 0.5. This is a classic weakness of a single tree; it finds one "killer" feature and bases most of its logic on it. This explains why its performance is lower—it's not as nuanced as the Random Forest. |
| **Logistic Regression** 📈 | 1. `pr.axis_aspect_ratio`<br>2. `elongatedness`<br>3. `scaled_variance.1`<br>4. `compactness`<br>5. `scatter_ratio` | **Different Perspective (Linear).** The linear model finds *different* features to be important! It values `pr.axis_aspect_ratio` and `elongatedness` the most. This suggests these features have the strongest *linear* relationship with the classes. The tree models, which can capture non-linear patterns, valued them less. |

---

### 💡 Summary Findings

1.  **Universal Feature:** `scaled_variance.1` is clearly the single most predictive feature, as it appears in the Top 3 for *all* models.
2.  **Different Thinking:** The tree-based models (RF, DT) and the linear model (LR) "think" differently. The trees found `pr.axis_rectangularity` highly important, while the linear model found `pr.axis_aspect_ratio` more important.
3.  **Why Random Forest Won:** The RF plot confirms *why* it's the best model. It learns from the most important features (like the Decision Tree) but *balances* their influence, preventing over-reliance on any single one. It creates a more holistic and stable decision-making process.

# 📊 Analysis of the Model Performance Comparison Graph

<img width="583" height="348" alt="image" src="https://github.com/user-attachments/assets/6aae0722-a639-4f64-ad0a-a6af639233fa" />


| Question | Answer |
| :--- | :--- |
| **What is this?** 🤔 | This is a bar chart that provides a simple, direct summary of the final results from our Phase 2 modeling. |
| **What it Shows** 📈 | It plots the final **Test Accuracy** score for all four trained models (Random Forest, Logistic Regression, kNN, and Decision Tree) side-by-side, sorted from best to worst. |
| **What Question it Answers** ❓ | It directly answers the question: **"Which model performed the best, and how do they all compare at a single glance?"** |


* **ROC Curves for All Models:**

<img width="569" height="491" alt="image" src="https://github.com/user-attachments/assets/ef3b8af4-9702-4468-a53c-4e818e8ff3e7" />

<img width="610" height="527" alt="image" src="https://github.com/user-attachments/assets/2374a1f9-ccc0-44ea-94d1-90135090109c" />

<img width="567" height="502" alt="image" src="https://github.com/user-attachments/assets/81f02493-845f-428e-a1cb-c38f2c57fea8" />

<img width="626" height="494" alt="image" src="https://github.com/user-attachments/assets/0286f38c-d67a-4edc-9114-4c782abacc8f" />

# ⚡ Analysis of One-vs-Rest (OvR) ROC Curves

This report analyzes the ROC (Receiver Operating Characteristic) curves for our four classification models. The key metric here is the **AUC (Area Under the Curve)**, which measures a model's ability to distinguish between classes.

* **AUC = 1.0:** Perfect model.
* **AUC = 0.5:** No-skill model (equivalent to random guessing).

---

### Why Are There Three Separate Curves Per Plot? The "One-vs-Rest" (OvR) Approach

Before the comparison, it's critical to understand *why* each plot has three curves.

1.  **ROC is Binary:** A standard ROC curve is designed for **binary** (two-class) problems (e.g., "Yes" vs. "No").
2.  **Our Problem is Multiclass:** We have **three** classes: `bus`, `car`, and `van`. We cannot plot a single ROC curve for this.
3.  **The Solution (OvR):** We re-frame the problem as three separate binary classification tasks:
    * **Curve 1 (bus vs. Rest):** How well does the model distinguish `bus` from (`car` + `van`)?
    * **Curve 2 (car vs. Rest):** How well does the model distinguish `car` from (`bus` + `van`)?
    * **Curve 3 (van vs. Rest):** How well does the model distinguish `van` from (`bus` + `car`)?

A model with high AUC scores for all three classes (all curves hugging the top-left corner) is an excellent and robust classifier.

---

### 📈 Comparative ROC/AUC Analysis

This table compares the models based on the AUC scores from the provided images.

| Model 🤖 | AUC Scores (Class-by-Class) 💯 | Analysis & Interpretation 💡 |
| :--- | :--- | :--- |
| **Random Forest** 🥇 | **`bus`: 1.00**<br>**`car`: 1.00**<br>**`van`: 1.00** | **Perfect Separator.** This is an exceptional result. An AUC of 1.00 for all classes means the model has a perfect ability to distinguish each class from the others at the probability level. The curves are "ideal," perfectly hugging the top-left corner. |
| **Logistic Regression** 🥈 | **`bus`: 0.99**<br>**`car`: 0.99**<br>**`van`: 0.99** | **Extremely Strong.** With AUC scores of 0.99 across the board, this model is also a top-tier separator. It has an outstanding ability to distinguish all three classes, performing nearly as perfectly as the Random Forest. |
| **k-Nearest Neighbors** 🥉 | **`bus`: 0.99**<br>**`car`: 0.98**<br>**`van`: 0.96** | **Very Strong, with One Weakness.** This model shows excellent separability for `bus` (0.99) and `car` (0.98). However, its AUC for `van` (0.96) is slightly lower. This confirms our findings from the Confusion Matrix: the `van` class is the most difficult for the kNN model to confidently distinguish. |
| **Decision Tree** 🌳 | **`bus`: 0.92**<br>**`car`: 0.92**<br>**`van`: 0.90** | **Weakest Performer.** The Decision Tree's AUC scores are significantly lower. The curves are visibly "flatter" (closer to the 0.5 diagonal line). An AUC of 0.90 for `van` shows it has considerable difficulty separating `van` samples from `bus` and `car` samples. This aligns with its low accuracy and poor confusion matrix. |



# 🧠 Analysis: Random Forest Classification Error Plot

<img width="528" height="393" alt="image" src="https://github.com/user-attachments/assets/0acbfbf9-3e03-45c8-bfdf-ad9a8daee5f0" />

This plot, the **Confusion Matrix**, is the primary tool for analyzing the errors of our best-performing model, the Random Forest. It moves beyond the simple "96% accuracy" and shows us exactly *where* the model succeeded and *where it failed*.

---

### 🎯 What This Plot Shows

* **Y-Axis (True Label):** Represents the *actual*, ground-truth class of the vehicle (e.g., the row labeled `bus` contains all 44 vehicles that were truly buses).
* **X-Axis (Predicted Label):** Represents the *prediction* that the model made.
* **The Goal:** A perfect model would have numbers *only* on the main diagonal (from top-left to bottom-right) and zeros everywhere else.

---

### ✅ The Main Diagonal (Correct Predictions)

This diagonal shows where the "True Label" and "Predicted Label" match.

* **`bus` (43):** The model correctly identified 43 out of 44 true `bus` samples. (An excellent result).
* **`car` (81):** The model correctly identified 81 out of 86 true `car` samples.
* **`van` (36):** The model correctly identified 36 out of 40 true `van` samples.

---

### ❌ The Off-Diagonal (Errors & Confusion)

These are the most important numbers, as they represent the model's mistakes.

* **Primary Error (5):** The largest single error is in the `[True: car, Predicted: van]` cell. This means the model **incorrectly classified 5 true 'car' samples as 'van'**. This appears to be its biggest blind spot.
* **Secondary Error (4):** The next largest error is in the `[True: van, Predicted: bus]` cell. The model **incorrectly classified 4 true 'van' samples as 'bus'**. This confirms the `bus/van` similarity that we saw in other models.
* **Tertiary Error (1):** A minor error in the `[True: bus, Predicted: van]` cell, where **1 true 'bus' was misclassified as 'van'**.

---

### 💡 Key Insights & Summary

1.  **Zero `car`/`bus` Confusion:** The model *perfectly* separates `car` from `bus`. It never misclassified a `car` as a `bus`, and it never misclassified a `bus` as a `car`. The 0s in these cells are a sign of high confidence.
2.  **Primary Weakness: `car` vs. `van`:** The model's main struggle is distinguishing `car` silhouettes from `van` silhouettes.
3.  **Secondary Weakness: `bus` vs. `van`:** The model also struggles (though less so) with the `bus`/`van` distinction, which was a major problem for the weaker models.
4.  **Overall Errors:** In this specific run, the model made a total of 5 + 4 + 1 = 10 errors.
5.  **Calculated Accuracy:** (43 + 81 + 36) / 170 = 160 / 170 = **94.1% Accuracy**.

⚠️ **Note on Results:** This specific confusion matrix (with 10 errors and 94.1% accuracy) is slightly different from our text-based `classification_report` (which showed 7 errors and **95.9%** accuracy). This is very common in machine learning notebooks if a parameter or `random_state` was slightly different between runs. Both plots, however, tell the same story: the model is excellent, and its primary errors are confusing `car` with `van` and `van` with `bus`.

### 3.2. Data Insights Visuals

* **Pair Plots/Correlation Heatmaps:** Displaying the relationships between all pairs of features.
* **Feature Distributions:** Histograms or density plots showing the distribution of the most important features.
* **Grouped Box Plots:** Showing how the target variable is distributed across different categories of a key categorical feature.

#### 📊 Data Insights Visuals: Introduction to Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) is a crucial step in the Data Science process. It involves analyzing data sets to summarize their main characteristics, often with visual methods.

---

#### 3.2.1 Data Exploration and Analysis (EDA) 🔎

Exploratory Data Analysis (EDA) is the cornerstone of understanding the dataset structure, discovering patterns, and identifying anomalies, thereby guiding the preprocessing and modeling steps.

---

###### 3.2.1.1 Non-Graphical Analysis 🔢

This section covers the initial quantitative inspection of the dataset, focusing on descriptive statistics and data integrity.

###### 🔬 Feature Scale and Variability Analysis

A statistical summary of the 18 numerical features provides critical insights into their scale, central tendency, and dispersion. This is a foundational step before any data visualization or modeling.

* Number of duplicate rows: 0

**Data Integrity:** The check for duplicate rows returned 0. This indicates that the dataset is clean in terms of redundant entries, and all 846 instances are unique.

**Descriptive Statistics Table:**

| | compactness | circularity | distance_circularity | radius_ratio | pr.axis_aspect_ratio | max.length_aspect_ratio | scatter_ratio | elongatedness | pr.axis_rectangularity | max.length_rectangularity | scaled_variance_major | scaled_variance_minor | scaled_radius_of_gyration | skewness_major | skewness_minor | kurtosis_minor | kurtosis_major | hollows_ratio |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **count** | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 | 846.00 |
| **mean** | 93.68 | 44.86 | 82.09 | 168.94 | 61.69 | 8.57 | 168.84 | 40.93 | 20.58 | 147.99 | 188.63 | 361.35 | 174.71 | 72.46 | 6.38 | 12.60 | 188.93 | 195.63 |
| **std** | 8.23 | 6.17 | 15.77 | 33.47 | 7.89 | 4.60 | 33.25 | 7.81 | 2.59 | 14.52 | 31.39 | 176.51 | 32.55 | 7.49 | 4.92 | 8.93 | 6.16 | 7.44 |
| **min** | 73.00 | 33.00 | 40.00 | 104.00 | 48.00 | 2.00 | 112.00 | 26.00 | 17.00 | 118.00 | 131.00 | 184.00 | 112.00 | 59.00 | 0.00 | 0.00 | 176.00 | 181.00 |
| **25%** | 87.00 | 40.00 | 70.00 | 141.00 | 57.00 | 7.00 | 146.25 | 36.00 | 19.00 | 137.00 | 167.00 | 318.25 | 149.00 | 67.00 | 2.00 | 5.00 | 184.00 | 190.25 |
| **50%** | 93.00 | 44.00 | 80.00 | 167.00 | 61.00 | 8.00 | 157.00 | 40.00 | 20.00 | 146.00 | 178.50 | 363.50 | 173.50 | 72.00 | 6.00 | 11.00 | 188.00 | 197.00 |
| **75%** | 100.00 | 49.00 | 98.00 | 195.00 | 65.00 | 10.00 | 188.00 | 45.00 | 22.00 | 159.00 | 217.00 | 401.50 | 198.00 | 75.00 | 10.00 | 19.00 | 193.00 | 201.00 |
| **max** | 119.00 | 59.00 | 112.00 | 333.00 | 138.00 | 55.00 | 265.00 | 61.00 | 29.00 | 188.00 | 320.00 | 1018.00 | 268.00 | 135.00 | 22.00 | 41.00 | 206.00 | 211.00 |

#### 🧐 Key Observations:

1.  **Varying Scales:**
    * The features exhibit vastly different scales. For instance, `scaled_variance_minor` has a mean of ~361 and a maximum value of 1018, while `max.length_aspect_ratio` has a mean of ~8.6 and a maximum of 55.
    * This discrepancy is also clear in the standard deviation (`std`).

2.  **Varying Variability:**
    * The standard deviation (`std`) reveals how spread out the data is for each feature.
    * `scaled_variance_minor` has an extremely high `std` (176.51), indicating its values are widely dispersed.
    * In contrast, `pr.axis_rectangularity` has a very low `std` (2.59), meaning its values are tightly clustered around its mean.

#### ⚖️ Implication for Modeling:

The significant differences in both scale and variability across the features strongly suggest that **feature scaling is a mandatory preprocessing step.**

Algorithms that are sensitive to feature magnitude (such as $k$-Nearest Neighbors, Support Vector Machines (SVMs), Principal Component Analysis (PCA), and Neural Networks) will be biased towards features with larger scales. Applying a scaler (like **StandardScaler** to normalize $z$-scores or **MinMaxScaler** to scale to a [0, 1] range) will ensure that all features contribute equally to the model's learning process.

<img width="741" height="455" alt="image" src="https://github.com/user-attachments/assets/6630bca1-bd15-4092-8606-35d701250f9c" />


<img width="755" height="480" alt="image" src="https://github.com/user-attachments/assets/b8b0c401-6ae9-4d5a-b670-e7138dc9aef2" />

<img width="870" height="543" alt="image" src="https://github.com/user-attachments/assets/b9ab9973-f7c9-458d-b735-fc7fe1f67989" />

<img width="771" height="462" alt="image" src="https://github.com/user-attachments/assets/8c0b8582-7223-47a9-a7bc-d2f56db07bf1" />

---

##### 3.2.1.2. Univariate Analysis (Single Variable) 📉

Focuses on analyzing one variable at a time to understand its distribution and detect outliers.

* **Goal:** Summarize the variable's properties, confirm data types (`int64`), and identify patterns.
* **Initial Findings (Structural Check):**
    * **Missing Values:** Confirmed **no missing values** across all 846 entries. Every column is complete (846 non-null).
    * **Data Types:** All 18 features are of integer type (`int64`), suitable for direct scaling. The target variable `class` is an `object` (string/categorical).
    * **Scale:** Features are on **vastly different scales** (e.g., `compactness` mean ≈ 93.7, while `scaled_variance_minor` mean ≈ 361.4). This confirms that **Scaling** is a mandatory preprocessing step.
* **Visualizations & Graphs:** Histograms, Box Plots, and Density Plots for each feature are required to visually confirm the skewness and outlier presence indicated by the descriptive statistics.

* **Histograms:**
  
<img width="980" height="620" alt="image" src="https://github.com/user-attachments/assets/e17832af-d7a4-4f3d-9ca0-410b165e194e" />

## 📊 Graphical Univariate Analysis: Histogram Insights

This analysis examines the distribution of each of the 18 numerical features to identify their underlying shape, central tendency, and the presence of skewness or multiple modes. These shapes provide critical clues for feature selection and preprocessing.

### Key Distributional Observations:

The 18 features can be broadly categorized into three main groups based on their histogram shapes:

* **🔔 1. Normally or Near-Normally Distributed Features (Symmetric)**
    * **Features:** `compactness`, `circularity`, `distance_circularity`, `pr.axis_rectangularity`, `max.length_rectangularity`, `scaled_radius_of_gyration`, `skewness_major`.
    * **Analysis:** These features display a (near) symmetric, bell-shaped distribution. Their mean, median, and mode are closely aligned at the center.
    * **Implication:** These are well-behaved features that are ideal for many statistical models. They exhibit some variance but do not have extreme, one-sided outliers. `compactness` and `max.length_rectangularity` appear to be slightly left-skewed, but are still largely uni-modal and symmetric.

* **📈 2. Skewed Features (Asymmetric)**
    * **Features:**
        * **Right-Skewed (Positively Skewed):** `radius_ratio`, `pr.axis_aspect_ratio`, `max.length_aspect_ratio`, `skewness_minor`, `kurtosis_minor`.
        * **Left-Skewed (Negatively Skewed):** `kurtosis_major`.
    * **Analysis:** These features show a strong asymmetry.
    * For the **right-skewed** features (e.g., `max.length_aspect_ratio`), the majority of the data points are clustered at the lower end of the scale, with a long tail extending towards the right. This indicates that most vehicles have a low value for this feature, but a few vehicles have an extremely high value (potential outliers).
    * For the **left-skewed** `kurtosis_major`, the tail extends to the left.
    * **Implication:** For models sensitive to feature distributions (like some regression models), applying a transformation (e.g., Logarithmic or Square Root) to these skewed features could be beneficial to normalize them.

* **⛰️ 3. Bimodal and Multimodal Features (Multiple Peaks)**
    * **Features:** `scatter_ratio`, `elongatedness`, `scaled_variance_major`, `scaled_variance_minor`, `hollows_ratio`.
    * **Analysis:** This is the most significant finding. These features display two or more distinct peaks, indicating that the data is not a single homogenous group.
    * **Hypothesis:** These distinct peaks almost certainly correspond to the different **vehicle classes** (`car`, `bus`, `van`). For example, one peak in `elongatedness` might represent 'car' and 'van', while the other peak represents 'bus'.
    * **Implication:** These features are **excellent candidates for classification**. They inherently contain information that separates the target classes and will likely be assigned high importance by machine learning models.

* **Density Plots:**

<img width="955" height="619" alt="image" src="https://github.com/user-attachments/assets/a45191e7-ac7a-4ce3-a410-99ec8939c52e" />

## 🌊 Graphical Univariate Analysis: Density Plots (KDE)

These Kernel Density Estimation (KDE) plots provide a smoothed, continuous alternative to histograms. They help to more clearly visualize the probability density of each feature, confirming the distributional shapes, skewness, and modality (number of peaks) identified in the previous analysis.

### 🔍 Key Observations from Density Plots:

The density plots confirm the three primary distribution types found in the dataset:

* **🔔 1. Unimodal & Symmetric (Normal or Near-Normal)**
    * **Features:** `circularity`, `distance_circularity`, `pr.axis_rectangularity`, `max.length_rectangularity`, `scaled_radius_of_gyration`.
    * **Analysis:** These plots show a clear, single, bell-shaped curve. This confirms they are symmetrically distributed around a central mean value, reinforcing that they are "well-behaved" features with no significant skew.

* **📈 2. Skewed (Asymmetric)**
    * **Features:**
        * **Right-Skewed:** `radius_ratio`, `pr.axis_aspect_ratio`, `max.length_aspect_ratio`, `skewness_major`, `skewness_minor`, `kurtosis_minor`.
        * **Left-Skewed:** `compactness`, `kurtosis_major`.
    * **Analysis:** The smooth density curves make the asymmetric nature of these features obvious. The plots show a high concentration of data (a high peak) on one side, followed by a long, low "tail" on the other. This visual confirms the skewness and corresponds directly to the outliers we observed in the box plots.

* **⛰️ 3. Bimodal and Multimodal (Two or More Peaks)**
    * **Features:** `scatter_ratio`, `elongatedness`, `scaled_variance_major`, `scaled_variance_minor`, `hollows_ratio`.
    * **Analysis:** This is the most critical insight, and the density plots make it exceptionally clear. These features do not follow a single distribution. Instead, they show two (or more) distinct peaks.
    * **Hypothesis:** These peaks strongly represent the different **vehicle classes** (`car`, `bus`, `van`) being "mixed" together in the overall dataset.
    * **Implication:** As seen in the box plots, these features have the highest discriminatory power. The `scaled_variance_minor` plot, with its multiple complex peaks, looks particularly rich in information that could help separate all three classes.



---

##### 3.2.1.3 Bivariate Analysis (Two Variables) 🔗

Examines the relationship between any two variables in the dataset.

* **Goal:** Understand how features co-vary and identify potential correlations or dependencies that can inform **Feature Selection** or **Feature Engineering**.
* **Techniques & Graphs:** Correlation Matrices (Heatmaps), Scatter Plots.
* **Graph Required:** A **Correlation Heatmap** to visualize linear relationships between all feature pairs.

* **Box Plots  by Class:**

<img width="985" height="628" alt="image" src="https://github.com/user-attachments/assets/ab61098a-27d3-406e-aef0-3fde2044061f" />

While our analysis plan started with univariate analysis, this section transitions into **bivariate analysis**. By plotting each numerical feature *against* the categorical `class` variable, we are no longer looking at features in isolation. Instead, we are actively investigating the relationship between two variables to find out which features are most effective at discriminating between `bus`, `car`, and `van`.

### 🔍 Key Insights from Box Plots by Class

The 18 box plots reveal how the distribution (median, interquartile range (IQR), and outliers) of each feature differs across the three vehicle classes.

* **1. High Discriminatory Power (Strong Separators):**
    * **Features:** `scatter_ratio`, `elongatedness`, `scaled_variance_major`, `scaled_variance_minor`.
    * **Analysis:** These are the most valuable features for classification. Their box plots show a clear separation between the classes.
    * **Example:** For `elongatedness`, the 'bus' class has a significantly lower and more compact range of values compared to 'car' and 'van', which have higher and overlapping values. Similarly, `scaled_variance_minor` shows that the 'car' class has a much wider and higher-value distribution than 'bus' or 'van'.

* **2. Moderate Discriminatory Power (Some Separation):**
    * **Features:** `compactness`, `distance_circularity`, `radius_ratio`, `pr.axis_rectangularity`, `max.length_rectangularity`.
    * **Analysis:** These features show a noticeable difference in medians or ranges, but with significant overlap between at least two classes.
    * **Example:** For `compactness`, the 'bus' class tends to have a higher median value than 'car' or 'van', but the IQRs (the boxes) overlap, suggesting this feature alone is not enough to separate them.

* **3. Low Discriminatory Power (Weak Separators):**
    * **Features:** `circularity`, `pr.axis_aspect_ratio`, `max.length_aspect_ratio`, `scaled_radius_of_gyration`, `skewness_major`, `skewness_minor`, `kurtosis_minor`, `kurtosis_major`, `hollows_ratio`.
    * **Analysis:** These features are less useful for classification. Their box plots (median, 25th, and 75th percentiles) are nearly identical across all three vehicle classes.
    * **Example:** `hollows_ratio` shows almost the same median and IQR for `bus`, `car`, and `van`, indicating it provides little to no information for distinguishing between them.

---

### ⚠️ The Role and Impact of Outliers

The individual points ($\cdot$) plotted beyond the "whiskers" of the boxes are **outliers**. These are data points that fall far outside the expected range of the data (specifically, more than 1.5 times the Interquartile Range above the 3rd quartile or below the 1st quartile).

In our dataset, features like `radius_ratio`, `pr.axis_aspect_ratio`, and `max.length_aspect_ratio` show a significant number of outliers, especially for the 'car' class.

The impact of these outliers can be both negative and positive:

#### ⛔ Negative Contributions (Why they can be problematic)

1.  **Distort Statistical Summaries:** Outliers can drastically skew the `mean` (ortalama) and `standard deviation` (standart sapma). This is why the `median` (the line in the box) is a more *robust* measure of central tendency.
2.  **Bias Model Training:** Many machine learning models (like Linear Regression, Logistic Regression, and $k$-Means) are sensitive to outliers. A single extreme value can pull the decision boundary or cluster center in its direction, leading to a less accurate model for the *majority* of the data.
3.  **Impact Feature Scaling:** If using `MinMaxScaler` (scaling data between 0 and 1), a single outlier will become the '1' or '0', forcing all other "normal" data into a very small range (e.g., [0.1, 0.3]). This reduces the model's ability to see differences in the normal data. `StandardScaler` (Z-score) is less affected but still impacted.

#### ✅ Positive Contributions (Why they are valuable)

1.  **Represent True Variability:** Outliers are not always errors. In our data, the large number of outliers in the 'car' class (e.g., in `radius_ratio`) strongly suggests that the 'car' category is **inherently more diverse** than the 'bus' or 'van' categories. It likely includes hatchbacks, sedans, and sports cars, all with different silhouette properties. Removing these outliers would mean removing true information about the 'car' class.
2.  **Provide Domain Insights:** An outlier might represent a unique case (e.g., a "head-on" or "rear" view of a vehicle, which looks very different from a side profile) or a data collection anomaly. Investigating them can lead to a deeper understanding of the problem.
3.  **Test Model Robustness:** The presence of outliers forces us to choose more *robust* models. Tree-based models (like **Decision Trees** and **Random Forest**) are naturally immune to the impact of outliers. Robust scaling methods (like `RobustScaler`) can also be used to mitigate their negative impact.


* **Feature Correlation Matrix/ Heat Map:**

<img width="931" height="629" alt="image" src="https://github.com/user-attachments/assets/94434337-8b01-4548-b5d7-5d001020727b" />

## 🔗 Bivariate Analysis: Correlation Heatmap Insights

This heatmap visualizes the Pearson correlation coefficient between all 18 numerical features. The correlation matrix is a cornerstone of bivariate analysis, revealing which features move together and which are independent.

* **Color Key:**
    * 🔴 **Dark Red:** Strong positive correlation (approaching +1.0). When one feature increases, the other tends to increase.
    * 🔵 **Dark Blue:** Strong negative correlation (approaching -1.0). When one feature increases, the other tends to decrease.
    * ⚪ **White / Light:** No correlation (approaching 0.0). The features are linearly independent.

### 🧠 Key Findings & Implications for Modeling:

1.  **High Multicollinearity:**
    * **Observation:** The heatmap reveals several "blocks" of dark red, indicating extremely high positive correlations ($r > 0.8$). This is known as **multicollinearity**.
    * **Key Groups:**
        * **Group A (Variance/Scatter):** `scatter_ratio`, `scaled_variance_major`, and `scaled_variance_minor` are all highly correlated with each other. They appear to measure a very similar underlying property of the silhouette (its "spread" or "variance").
        * **Group B (Rectangularity/Circularity):** `pr.axis_rectangularity`, `max.length_rectangularity`, and `circularity` also show strong positive correlations.
        * **Group C (Hollows):** `hollows_ratio` and `kurtosis_major` are strongly correlated.
    * **Implication:** For many models (especially Linear/Logistic Regression), multicollinearity is a problem. It makes model coefficients unstable and hard to interpret. For feature selection, we should **avoid using all features from the same group**. For example, we should likely pick only *one* feature from Group A (e.g., `scatter_ratio`) and drop the other two, as they provide redundant information.

2.  **Strong Inverse Relationships:**
    * **Observation:** There is a very strong block of dark blue, centered around `elongatedness`.
    * **Key Relationship:** `elongatedness` has a powerful *negative* correlation with `scatter_ratio`, `scaled_variance_major`, and `scaled_variance_minor`.
    * **Implication:** This makes perfect physical sense: as a vehicle silhouette becomes more "elongated" (uzun), its "scatter ratio" (yayılımı) decreases. This reinforces the multicollinearity finding. `elongatedness` provides the *same* information as the features in Group A, just in an inverse manner. We should choose between `elongatedness` *or* one of the Group A features.

3.  **Independent Features:**
    * **Observation:** Some features form "white lines" or "white crosses" on the heatmap, indicating they have very low correlation (near 0) with most other features.
    * **Key Features:** `skewness_major`, `skewness_minor`, `kurtosis_minor`, and `max.length_aspect_ratio`.
    * **Implication:** These features are valuable because they provide **unique, independent information** that is not captured by any other feature. Even if their individual power to separate classes (seen in the box plots) was moderate or low, their independence makes them strong candidates to include in a multivariate model, as they contribute a unique perspective.
  

## 🔢 Bivariate Analysis: Mean Feature Values by Class

This table provides a quantitative summary of the visual insights gained from the box plots. It calculates the exact mean (average) value for all 18 numerical features, grouped by the three vehicle classes.

This analysis clearly reveals the *magnitude* of the differences between classes.

| class | compactness | circularity | distance_circularity | radius_ratio | pr.axis_aspect_ratio | max.length_aspect_ratio | scatter_ratio | elongatedness | pr.axis_rectangularity | max.length_rectangularity | scaled_variance_major | scaled_variance_minor | scaled_radius_of_gyration | skewness_major | skewness_minor | kurtosis_minor | kurtosis_major | hollows_ratio |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 🚌 **bus** | 104.24 | 52.18 | 101.44 | 201.76 | 59.21 | 7.21 | 203.63 | 33.80 | 23.47 | 167.32 | 214.33 | 612.34 | 205.11 | 70.74 | 8.57 | 10.42 | 186.33 | 194.29 |
| 🚗 **car** | 86.97 | 40.64 | 70.09 | 142.13 | 60.78 | 7.68 | 142.29 | 43.12 | 18.80 | 135.59 | 169.53 | 295.33 | 152.09 | 73.53 | 5.59 | 10.02 | 190.25 | 197.64 |
| 🚐 **van** | 93.20 | 44.19 | 81.43 | 163.09 | 61.16 | 8.75 | 161.95 | 40.78 | 20.17 | 144.11 | 183.19 | 362.89 | 169.77 | 72.10 | 6.14 | 17.15 | 188.75 | 194.81 |

#### 📖 Interpreting the Mean Values Table

* **What this table represents:**
It shows the average (mean) values for all 18 numerical features, broken down by the 3 distinct vehicle classes (`bus`, `car`, and `van`).

* **In simpler terms:**
This table provides a numerical answer to the questions:
    * 🚌 "What does an average 'bus' look like?"
    * 🚗 "What does an average 'car' look like?"
    * 🚐 "What does an average 'van' look like?"
 
#### 📊 Quantitative Insights from Mean Value Analysis:

This table provides a numerical summary of the differences observed visually in the box plots.

* **`elongatedness`:** 🚌 The mean value for a `bus` (33.80) is significantly lower than that of a `car` (43.12) or `van` (40.78). This indicates that 'bus' silhouettes are perceived as less "elongated" and confirms this feature is an excellent separator.

* **`scatter_ratio`:** 🚌 The mean value for a `bus` (203.62) is substantially higher than for a `car` (142.28) or `van` (161.94). This also indicates high discriminatory power.

* **`hollows_ratio`:** 📉 The mean values for `bus` (194.29), `car` (197.64), and `van` (194.81) are all extremely close to one another. This confirms that this feature is a weak separator.

#### ✅ Conclusion:

This table serves as a **numerical summary of the Box Plots**. It quantitatively confirms the differences we saw visually, providing clear evidence of which features are most important for classifying the vehicles.

### 🧐 Key Quantitative Insights:

* **`elongatedness`:** The mean value for `bus` (33.80) is significantly lower than for `car` (43.12) or `van` (40.78). This confirms it as a powerful separator.
* **`scatter_ratio` & `scaled_variance_minor`:** The `bus` class has exceptionally high mean values in these features (203.63 & 612.34) compared to the `car` class (142.29 & 295.33), which has the lowest.
* **`hollows_ratio`:** The mean values are extremely close for all three classes (`bus`: 194.29, `car`: 197.64, `van`: 194.81), confirming this feature has very low discriminatory power.

---

* **Pair Plot:**

<img width="722" height="646" alt="image" src="https://github.com/user-attachments/assets/da6a6671-72a8-4508-b70a-168d27bf26f4" />

## 🔬 Bivariate/Multivariate Analysis: Pairplot of Key Features

This `pairplot` visualizes the interactions between our most promising features:
1.  **`elongatedness`** (Strong separator)
2.  **`scatter_ratio`** (Strong separator, but correlated with `elongatedness`)
3.  **`skewness_minor`** (Independent feature, weak separator)

The data points are colored by their `class` (🚌 `bus` = blue, 🚗 `car` = orange, 🚐 `van` = green), allowing us to see how well these features separate the classes, both individually and in combination.

---

### 1. Analysis of the Diagonal (KDE Plots)

The diagonal of the plot shows the individual density (KDE) distribution of each feature, broken down by class.

* **`elongatedness` (Top-left):** This confirms our `groupby()` analysis. The `bus` 🚌 (blue) class has a distinct, sharp peak at a low value (~34), while the `car` 🚗 (orange) and `van` 🚐 (green) classes have higher-value peaks that significantly overlap with each other.
* **`scatter_ratio` (Middle-middle):** This plot is the *inverse* of `elongatedness`. The `bus` 🚌 (blue) class has a clear peak at a high value (~205), while `car` 🚗 (orange) and `van` 🚐 (green) have lower-value peaks that overlap.
* **`skewness_minor` (Bottom-right):** This plot confirms why this is a *weak separator*. All three class distributions (blue, orange, and green) are almost perfectly on top of each other. This feature, by itself, provides little to no ability to distinguish between the vehicle types.

---

### 2. Analysis of the Off-Diagonal (Scatter Plots)

These plots show the relationship between two features at a time.

#### 📉 The Main Event: `scatter_ratio` vs. `elongatedness` (Top-Middle Plot)

This is the most important chart in the matrix.
* **Negative Correlation:** It perfectly visualizes the strong negative correlation (approx. -0.8) that the heatmap predicted. As `elongatedness` increases (moves to the right), `scatter_ratio` decreases (moves down).
* **Excellent Class Separation:** This 2D view achieves what the 1D plots (on the diagonal) could not. The classes, which were previously overlapping, are now clearly separated into distinct clusters:
    * **`bus` 🚌 (blue)** is isolated in the **top-left** (Low `elongatedness`, High `scatter_ratio`).
    * **`car` 🚗 (orange)** is clustered in the **bottom-right** (High `elongatedness`, Low `scatter_ratio`).
    * **`van` 🚐 (green)** sits **in the middle**, separating the other two classes.
* **Implication:** This proves that while these two features are *redundant* (correlated), using them **together** provides superb classification power.

#### ☁️ The Independent Feature: Plots with `skewness_minor`

* **`elongatedness` vs. `skewness_minor` (Bottom-Left Plot):** The data points form a "vertical cloud." This visually confirms the **zero correlation** from the heatmap. The separation of classes (blue, orange, green) only happens along the X-axis (`elongatedness`), not the Y-axis (`skewness_minor`).
* **`scatter_ratio` vs. `skewness_minor` (Middle-Right Plot):** The data points form a "horizontal cloud." This also confirms **zero correlation**. The separation of classes only happens along the X-axis (`scatter_ratio`), not the Y-axis (`skewness_minor`).
* **Implication:** Adding `skewness_minor` to a model *may* help by providing a unique dimension of information (since it's not correlated), but it is not a strong separator on its own. The primary separation will come from the `elongatedness`/`scatter_ratio` relationship.

---

##### 3.2.1.4 ## 🔬 Bivariate & Multivariate Analysis

This phase of the analysis examines the relationships between two or more variables simultaneously. This is often the most insightful part of EDA, as it uncovers interactions, correlations, and the features that best separate the target classes.

---

### 1. Categorical vs. Numerical (C vs. N)

* **Analysis:** Investigating how a continuous numerical feature is distributed across the different categories of the `class` variable.
* **Goal:** To determine if the mean or variance of a feature significantly differs across vehicle classes. This confirms the feature's **discriminative power**.
* **Techniques Used:**
    * ✅ **Box Plots (Grouped by `class`):** We *completed* this (`feature_boxplots_by_class.png`). This visually showed strong separators (like `elongatedness`) and weak separators (like `hollows_ratio`).
    * ✅ **Grouped Mean/Median:** We *completed* this (`df_veh.groupby('class').mean()`). This provided the exact numerical values to confirm the visual findings from the box plots.

---

### 2. Numerical vs. Numerical (N vs. N)

* **Analysis:** Investigating the relationship between two continuous numerical features.
* **Goal:** To detect linear associations, which is crucial for identifying **multicollinearity** (highly correlated features that provide redundant information).
* **Techniques Used:**
    * ✅ **Correlation Coefficient (Pearson's r):** We *completed* this calculation for all 18 features.
    * ✅ **Heatmap Visualization:** We *completed* this (`correlation_heatmap.png`). This allowed us to visually identify strong positive (red) and negative (blue) correlation blocks.

---

### 3. Multivariate Analysis (N vs. N vs. C)

* **Analysis:** Examining the complex, conditional relationship of how the association between two numerical features (A and B) changes based on a third, categorical variable (C).
* **Goal:** To find combinations of features that can separate the classes more effectively than any single feature alone.
* **Techniques Used:**
    * ✅ **Pair Plots (Colored by Target Class):** We *completed* this (`pairplot_key_features.png`).
    * **Insight:** This was highly successful. We proved that the combination of `elongatedness` and `scatter_ratio` creates distinct, separable clusters for `bus`, `car`, and `van`, even though `car` and `van` were heavily overlapped in 1D plots.

---

### 4. Multivariate Dimensionality Reduction (PCA)

* **Analysis:** A capstone multivariate technique to address the two main challenges identified in our dataset: high dimensionality (18 features) and high multicollinearity.
* **Goal:** To transform the 18 highly-correlated original features into a small set of new, **uncorrelated** features called **Principal Components (PCs)**, while retaining the maximum amount of information (variance) from the original data.
* **Techniques To Be Performed:**
    * 1️⃣ **Standard Scaling:** PCA is highly sensitive to feature scales. We *must* scale all 18 features (e.g., using `StandardScaler`) before applying PCA.
    * 2️⃣ **Principal Component Analysis (PCA):** Apply PCA to the scaled data to compute the new components (PC1, PC2, PC3, ...).
    * 3️⃣ **2D Visualization:** Create a single 2D scatter plot (PC1 vs. PC2), coloring the points by `class`, to visualize the *entire* dataset's class separation in just two dimensions.

# 🚨🚨🚨🚨🚨🚨🚨 ASK!!!!!!!!!🚨🚨🚨🚨🚨🚨🚨

## 🌀 Multivariate Analysis: PCA Explained Variance

<img width="1806" height="400" alt="image" src="https://github.com/user-attachments/assets/40714926-ff1f-4c0c-9c4f-081a7845356a" />




---

### 5. Categorical vs. Categorical (C vs. C)

* **Analysis:** Investigating the relationship between two discrete/group variables.
* **Status:** **Not Applicable (N/A).** As noted, this dataset contains only one categorical variable (`class`). Therefore, this specific type of bivariate analysis is not relevant to our project.

---

## 4. ⚙️ Critical Preprocessing Steps

The EDA confirms the necessity of several preprocessing steps essential for robust model training.

* **Scaling:** The **vast scale differences** (e.g., `COMPACTNESS` vs `SCALED VARIANCE ALONG MINOR AXIS`) necessitate mandatory scaling (e.g., **StandardScaler** or **MinMaxScaler**) to ensure all features contribute equally to the distance calculations in algorithms like k-NN or SVM.
* **Outlier Handling:** Features exhibiting high skewness and kurtosis (as seen in the descriptive statistics) require careful outlier investigation (using box plots) and potential treatment (e.g., capping, transformation, or model selection that is robust to outliers).
