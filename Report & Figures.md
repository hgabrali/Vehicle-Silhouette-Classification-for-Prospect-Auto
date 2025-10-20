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

### 📊 Data Insights Visuals: Introduction to Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) is a crucial step in the Data Science process. It involves analyzing data sets to summarize their main characteristics, often with visual methods.

---

#### 3.2.1. Non-Graphical Analysis 🔢

This involves calculating summary statistics for the dataset without relying on plots or charts. It provides a numerical summary of the data's central tendency, dispersion, and shape.

| Metric Type | Examples | Purpose |
| :--- | :--- | :--- |
| **Central Tendency** | Mean, Median, Mode | Finding the "typical" value. |
| **Dispersion** | Range, Variance, Standard Deviation, IQR | Measuring the spread of data. |
| **Shape** | Skewness, Kurtosis | Describing the symmetry and peakedness of the distribution. |
| **Frequency Tables** | Counts, Percentages | Summary for categorical variables. |

#### 3.2.2. Univariate Analysis (Single Variable) 📉

Focuses on analyzing one variable at a time to understand its distribution and detect outliers.

* **Goal:** Summarize the variable's properties and identify patterns.
* **Visualizations:** Histograms, Box Plots, Density Plots.
* **Use Case:** Identifying if a numerical feature is normally distributed or if a categorical feature is heavily imbalanced.

#### 3.2.3. Bivariate Analysis (Two Variables) 🔗

Examines the relationship between any two variables in the dataset.

* **Goal:** Understand how variables co-vary and identify potential correlations or dependencies.
* **Techniques:** Correlation Matrices, Scatter Plots, Grouped Box Plots.

#### 3.2.4. Multivariate Analysis (Multiple Variables) 🌐

Examines the relationships among three or more variables simultaneously. This is often the most insightful part of EDA as real-world phenomena involve complex interactions.

* **Goal:** Explore complex interactions, hidden patterns, and conditional relationships (e.g., how the relationship between A and B changes based on C).
* **Techniques:** Pair Plots, Bubble Charts, Heatmaps (with a third variable encoded by color/size).

#### 3.2.4.1. Numerical vs Numerical (N vs N)

Analyzing the relationship between two continuous variables.

* **Visualizations:** Scatter Plots, Line Plots (time series).
* **Metrics:** Pearson's r (Correlation Coefficient), Covariance.
* **Insight:** Detecting linear or non-linear associations, which is crucial for regression modeling.

#### 3.2.4.2. Categorical vs Categorical (C vs C)

Analyzing the relationship between two discrete/group variables.

* **Visualizations:** Stacked Bar Charts, Grouped Bar Charts, Mosaic Plots.
* **Metrics:** Chi-Square Test, Contingency Tables, Cramer's V.
* **Insight:** Testing for statistical independence between categories.

#### 3.2.4.3. Categorical vs Numerical (C vs N)

Analyzing how a continuous variable is distributed across different categories of a discrete variable.

* **Visualizations:** Box Plots (Grouped by Category), Violin Plots.
* **Metrics:** ANOVA (Analysis of Variance), T-tests, Grouped Mean/Median.
* **Insight:** Determining if the mean or variance of the numerical variable significantly differs across the categories.
