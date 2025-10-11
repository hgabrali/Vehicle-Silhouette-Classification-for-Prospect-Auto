# 🚗 Vehicle Silhouette Classification for Prospect Auto
## 🎯 Project Goal
The primary goal of this project is to develop and evaluate a robust multiclass classification model capable of accurately distinguishing between three distinct vehicle types—Bus, Van, and Car—based solely on their two-dimensional geometric silhouettes. This model will be used by "Prospect Auto" repair shops to automate initial vehicle identification.

# 📋 Data Description
The dataset utilizes 2D geometric features extracted from vehicle silhouettes viewed from various angles. All features are continuous and numerical.

## Feature Type	Value Range	Details
* Input Features	18 numerical columns (e.g., compactness, circularity, hollows_ratio).	These describe the shape of the vehicle silhouette; understanding their exact calculation is not required.
*Target Variable (class)	Categorical (3 values).	bus (double decker), van (Cheverolet), or car (Saab 9000/Opel Manta).

### Export to Sheets
**Key Challenge:** While the Bus and Van are expected to be easily distinguishable, the model must handle the challenge of separating the two similar Car models.

# 🛠️ Project Steps and Methodology
This project follows a standard supervised machine learning workflow, focusing on strong evaluation metrics due to the multiclass nature of the problem.

## Phase 1: Setup and Exploration
**Import & Load Data:** Import necessary Python libraries (Pandas, NumPy, Matplotlib, Scikit-learn) and load the vehicle silhouette dataset.

**Exploratory Data Analysis (EDA):** Conduct comprehensive visual and numerical analysis:

* Check for missing values, unique values, and data types.

* Analyze the distribution of the target variable (class) to check for class imbalance.

* Visualize feature distributions (histograms) and relationships between features and the target class.

## Phase 2: Data Preprocessing and Modeling
**Data Preparation:** Prepare the data for modeling:

* Separate features (X) from the target (y).

* Split the dataset into Training and Testing subsets.

* Apply Feature Scaling (e.g., StandardScaler) as all features are numerical.

* Supervised Classification: Train multiple classification models suitable for multiclass problems (e.g., Logistic Regression, kNN, Decision Trees, Random Forest).

## Phase 3: Evaluation and Conclusion
**Metric Selection:** Select a robust set of metrics for multiclass classification:

* Accuracy (Overall performance).

* Confusion Matrix (To see confusion between specific classes, particularly the two 'car' types).

* Precision, Recall, and F1 Score (Averaged across classes, e.g., 'macro' or 'weighted' average, to handle potential imbalance).

**Model Evaluation:** Evaluate all trained models using the selected metrics on the Test Set.

**Conclusion:** Based on the results (e.g., high F1 Score and low confusion between 'car' and other types), conclude whether the model meets "Prospect Auto's" needs for vehicle differentiation.

* Which model performed best? Can the model reliably distinguish between the "car" class and the other two?

## 💻 Where to Work
This project is best executed in a flexible environment like Google Colab or a Jupyter Notebook.
