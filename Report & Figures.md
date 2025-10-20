## 📊 Report & Figures

This section details the data selection process, initial data preparation, and subsequent analyses performed for this project.

### 🗃️ Data Source & Preparation

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
