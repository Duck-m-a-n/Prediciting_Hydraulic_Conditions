# Hydraulic Systems Monitoring by Stacking RandomForest 🌲🔧
## Stephen Duckers, Data Project Club - May 2023
Connect with me on [LinkedIn](https://www.linkedin.com/in/stephen-jake-duckers/)

### Dataset:
[UCI Condition monitoring of hydraulic systems Data Set](https://archive.ics.uci.edu/ml/datasets/condition+monitoring+of+hydraulic+systems)

### Objective 🎯
The aim of this project is to predict the stability of a hydraulic system along with identifying the causes of degradation. The conditions of various hydraulic system components - cooler_condition, valve_condition, internal_pump_leakage, and hydraulic_accumulator are treated as multi-class classification problems, while the system's overall stability prediction is a binary classification task.

### Approach 🧠
A RandomForestClassifier model is developed for each degradation state, which are then combined with sensor data to predict the system's stability. The primary evaluation metric used is `recall_weighted` in order to prioritize false negatives - when the system is mistakenly classified as stable when it isn't. Using the "weighted" averaging scheme, greater importance is attributed to minority classes, ensuring a more balanced evaluation of model performance amidst class imbalance.

### Insights and Recommendations 📊🔍
* **Valve Condition:** A key determinant of system stability. For optimal stability, the valve_condition should operate at 100%. Regular inspections and maintenance should be conducted to ensure this.
* **System Efficiency Sensor (SE):** SE serves as an excellent indicator of system stability. An alert system can be beneficial to notify the team when readings drop below certain levels, indicating potential stability issues.
* **Internal Pump Leakage:** It significantly affects system stability. Monitoring and timely mitigation of any internal pump leakages are crucial for system stability.
* **Cooler Condition:** It doesn't majorly impact the system's stability. This insight can help prioritize maintenance tasks, allowing more focus on valve condition and internal pump leakages.

EnergyMobil should primarily focus on monitoring valve condition and internal pump leakage, as sub-optimal values in these areas are more likely to lead to system instability.

### Exploratory Data Analysis 📊
The EDA process included:
* Histograms for data distribution checking (independent variables)
* Boxplots for outlier detection
* Line graphs for degradation states over time
* Pairplot to illustrate sensor data relationships
* Countplots for class distributions
* Correlation matrix to compare sensor and degradation states correlation
* Feature importance on all degradation states and features to find important sensors using RandomForestClassifier
* Spearman rank test for feature importance with stable flag and sensor data (does not assume linear relationship or normally distributed data)
* Chi-squared test to see importance of conditions with stable flag

### Machine Learning Model 🤖
For the model:
* `QuantileTransformer` was used for a non-linear transformation of the data based on their ranks, preserving the order of values while potentially redistributing outliers in the transformed space.
* `SMOTE` was utilized to handle class imbalance for degradation states (except cooler_condition) and stable_flag.
* Degradation states were one-hot encoded for evaluating the final model.

### Future Work 💡
* Feature selection for improved performance and interpretability
* More extensive hyperparameter tuning, as the recall score for the valve condition decreased by 10% when tuned, indicating model overfitting.
* Utilization of `OrdinalEncoder` for degradation conditions instead of `OneHotEncoder`, given the ordinal nature of the classes.
* Exploration of dimensionality reduction techniques like T-SNE and UMAP to capture local structures and nonlinear patterns better, as PCA was unable to adequately separate the stable_flag conditions.

Check out the Jupyter notebook for detailed code and explanations. If you find this project useful
