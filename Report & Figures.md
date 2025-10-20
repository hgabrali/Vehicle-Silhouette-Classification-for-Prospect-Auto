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
