# 📈 Report & Figures

This section is dedicated to presenting the final results, key findings, and performance evaluation of the project. A well-structured reporting section ensures transparency and easy verification of the model's success.

---

## 1. Final Model Performance Metrics

A clear summary of how the chosen model performs on unseen data (test set or cross-validation).

| Metric | Purpose | Typical Use Case |
| :--- | :--- | :--- |
| **Accuracy** | Overall correctness of classification. | General classification tasks. |
| **Precision** | Out of all positive predictions, how many were correct? | Minimizing False Positives (e.g., Spam detection). |
| **Recall (Sensitivity)** | Out of all actual positives, how many were correctly identified? | Minimizing False Negatives (e.g., Disease prediction). |
| **F1-Score** | Harmonic mean of Precision and Recall. | When an equal balance between P & R is needed. |
| **ROC AUC** | Area under the Receiver Operating Characteristic curve. | Evaluating the model's ability to distinguish between classes. |
| **R² (Coefficient of Determination)** | Proportion of the variance in the dependent variable that is predictable from the independent variables. | Regression tasks. |
| **RMSE/MAE** | Root Mean Square Error / Mean Absolute Error. | Measuring the magnitude of prediction errors in regression. |

## 2. Key Findings and Interpretations 🧠

Beyond raw numbers, this covers the insights derived from the model and the data itself.

* **Feature Importance:** Which input variables (features) had the greatest impact on the prediction?
* **Model Limitations:** What are the scenarios where the model performs poorly? (e.g., highly skewed data, rare events).
* **Business Impact:** How does the model's performance translate into practical value (e.g., cost savings, revenue increase)?

## 3. Visual Summaries (Figures) 🖼️

Visualizations are essential for quick comprehension and communicating complex results. All figures are typically stored in the `reports/figures/` directory.

### 3.1. Performance Visuals

* **Confusion Matrix:** A table visualizing the performance of a classification model. It clearly shows True Positives, True Negatives, False Positives, and False Negatives.
* **ROC Curve:** Graphically represents the trade-off between the True Positive Rate and the False Positive Rate at various threshold settings.
* **Residuals Plot (for Regression):** Used to check the homoscedasticity and normality assumptions of the regression model errors.

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

This involves calculating summary statistics for the dataset without relying on plots or charts, providing a numerical summary of the data's central tendency, dispersion, and shape.

| Metric Type | Examples | Purpose | Initial Observation (Based on `df.describe().T`) |
| :--- | :--- | :--- | :--- |
| **Central Tendency** | Mean, Median (`50%`) | Finding the "typical" value. | **PR.AXIS ASPECT RATIO** (Mean $\approx$ 61, Median = 61) shows symmetry. **SCALED VARIANCE ALONG MINOR AXIS** (Mean $\approx$ 439, Median = 363) suggests **right skewness**. |
| **Dispersion** | Range, Std. Deviation | Measuring the spread of data. | **SCALED VARIANCE ALONG MINOR AXIS** ($\text{Std} \approx 176$) has the highest variability, confirming the vast scale differences. |
| **Shape** | Skewness, Kurtosis | Describing the symmetry and peakedness of the distribution. | Several features like `SKEWNESS ABOUT MAJOR AXIS` and `KURTOSIS ABOUT MINOR AXIS` show values far from zero, confirming **non-Normal distributions** and the presence of **outliers/heavy tails**. |
| **Frequency Tables** | Counts, Percentages | Summary for categorical variables. | The **Target Class Distribution** shows 4 major classes (`saab`, `bus`, `opel`, `van`) with balanced counts ($\approx 200$), and **one highly imbalanced class** (`204`) with only 1 instance. |

---

##### 3.2.1.2. Univariate Analysis (Single Variable) 📉

Focuses on analyzing one variable at a time to understand its distribution and detect outliers.

* **Goal:** Summarize the variable's properties, confirm data types (`int64` and `float64`), and identify patterns.
* **Initial Findings (Structural Check):**
    * **Missing Values:** Confirmed **no missing values** across all 846 entries (except for one entry in `COMPACTNESS` from the `df.info()` output, which is negligible for 846 rows and all other columns being 846 non-null).
    * **Data Types:** Most features are of integer type, suitable for direct scaling. The target variable `class` is an `object` (string/categorical).
    * **Scale:** Features are on **vastly different scales** (e.g., `COMPACTNESS` mean $\approx 93$, `SCALED VARIANCE ALONG MINOR AXIS` mean $\approx 439$). This necessitates the **Scaling** step in preprocessing.
* **Visualizations & Graphs:** Histograms, Box Plots, and Density Plots for each feature to confirm the skewness and outlier presence indicated by the descriptive statistics.

---

##### 3.2.1.3 Bivariate Analysis (Two Variables) 🔗

Examines the relationship between any two variables in the dataset.

* **Goal:** Understand how features co-vary and identify potential correlations or dependencies that can inform **Feature Selection** or **Feature Engineering**.
* **Techniques & Graphs:** Correlation Matrices (Heatmaps), Scatter Plots.
* **Graph Required:** A **Correlation Heatmap** to visualize linear relationships between all feature pairs.

---

##### 3.2.1.4 Multivariate Analysis (Multiple Variables) 🌐

Examines the relationships among three or more variables simultaneously. This is often the most insightful part of EDA as real-world phenomena involve complex interactions.

* **Goal:** Explore complex interactions, hidden patterns, and conditional relationships (e.g., how the relationship between feature A and feature B changes based on the vehicle `class`).
* **Techniques & Graphs:** Pair Plots (Colored by Target Class), Bubble Charts.

##### 3.2.1.4.1. Numerical vs Numerical (N vs N)

Analyzing the relationship between two continuous variables.

* **Visualizations & Graphs:** Scatter Plots, Pair Plots.
* **Metrics:** Pearson's $r$ (Correlation Coefficient), Covariance.
* **Insight:** Detecting linear or non-linear associations, which is crucial for regression modeling (if the target were continuous) and identifying **multicollinearity** (highly correlated features that may destabilize some ML models).

##### 3.2.1.4.1.2. Categorical vs Categorical (C vs C)

Analyzing the relationship between two discrete/group variables. (In this dataset, only one categorical variable, the `class`, is present, limiting this direct analysis).

* **Visualizations & Graphs:** Stacked Bar Charts, Grouped Bar Charts.
* **Metrics:** Chi-Square Test, Contingency Tables, Cramer's $V$.
* **Insight:** Testing for statistical independence between categories.

#####  3.2.1.4.3. Categorical vs Numerical (C vs N)

Analyzing how a continuous variable is distributed across different categories of the discrete `class` variable.

* **Visualizations & Graphs:** Box Plots (Grouped by Vehicle Class), Violin Plots.
* **Metrics:** ANOVA (Analysis of Variance), T-tests, Grouped Mean/Median.
* **Insight:** Determining if the **mean or variance of a feature significantly differs across vehicle classes**. This confirms the feature's **discriminative power** for the classification task.

---

## 4. ⚙️ Critical Preprocessing Steps

The EDA confirms the necessity of several preprocessing steps essential for robust model training.

* **Scaling:** The **vast scale differences** (e.g., `COMPACTNESS` vs `SCALED VARIANCE ALONG MINOR AXIS`) necessitate mandatory scaling (e.g., **StandardScaler** or **MinMaxScaler**) to ensure all features contribute equally to the distance calculations in algorithms like k-NN or SVM.
* **Outlier Handling:** Features exhibiting high skewness and kurtosis (as seen in the descriptive statistics) require careful outlier investigation (using box plots) and potential treatment (e.g., capping, transformation, or model selection that is robust to outliers).
