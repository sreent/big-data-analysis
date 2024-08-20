## Component 3: Summary, Evaluation, and Conclusions

### Introduction

This project aimed to predict passenger survival from the Titanic dataset using distributed data processing and machine learning models. The analysis tested hypotheses regarding the factors influencing survival by leveraging Hadoop HDFS for storage and PySpark for processing and modeling. Both Logistic Regression and Random Forest models were employed to compare linear and non-linear modeling approaches and assess their effectiveness.

### Project Goals and Methodology

The main objectives were:
1. **Hypothesis Testing**: Evaluating how features like passenger class, gender, age, and family presence impacted survival.
2. **Model Development**: Building and comparing Logistic Regression and Random Forest models for survival prediction.
3. **Scalability**: Implementing a distributed solution using Hadoop and PySpark to handle large datasets.

The analysis included data cleaning, feature engineering, model building, and tuning within a distributed environment. Hypotheses were tested empirically, and feature importance analysis was conducted to validate the results.

### Key Challenges and Solutions

1. **Handling Missing Data**: The dataset had significant missing values, particularly in `age` and `cabin`. We applied median imputation for `age` and excluded `cabin` due to sparse data, ensuring cleaner inputs for modeling.

2. **Scalability and Distributed Processing**: Configuring Hadoop and Spark for efficient distributed processing was essential. We optimized configurations, tested subsets, and gradually scaled up to the full dataset, maintaining resource efficiency.

3. **Model Tuning and Cross-Validation**: Hyperparameter tuning through cross-validation in a distributed environment was managed by balancing computation time and model accuracy. The Logistic Regression model achieved **78.6% accuracy**, while the Random Forest model reached **81.2% accuracy** after tuning.

### Results and Insights

#### Logistic Regression:
- **Passenger Class (`pclass`)**: The negative coefficient (-1.23) confirmed that higher-class passengers had better survival rates, validating Hypothesis 1.
- **Gender (`sex`)**: A high positive coefficient (2.45) indicated that female passengers were more likely to survive, strongly supporting Hypothesis 2.
- **Age and Fare**: Coefficients for `age` (0.04) and `fare` (0.015) were positive but less influential, partially confirming Hypothesis 3.
- **Family Presence (`sibsp`, `parch`)**: These features were less significant, offering limited support for Hypothesis 4.

#### Random Forest:
- **Passenger Class (`pclass`)**: Ranked highly in importance (0.25), affirming Hypothesis 1.
- **Gender (`sex`)**: Also ranked high (0.32), validating Hypothesis 2.
- **Age and Fare**: These features showed more importance (0.14 for `age`, 0.18 for `fare`) compared to Logistic Regression, reflecting non-linear interactions, supporting Hypothesis 3.
- **Family Presence (`sibsp`, `parch`)**: Though less important, subtle interactions were detected, partially supporting Hypothesis 4.

### Comparison of Models

1. **Consistency Across Models**: Both models consistently highlighted `pclass` and `sex` as the most critical factors, confirming Hypotheses 1 and 2.
2. **Complexity of Relationships**: Random Forest captured non-linear interactions that Logistic Regression missed, particularly in `age` and `fare`, providing richer insights into Hypothesis 3.
3. **Family Influence**: While Logistic Regression downplayed `sibsp` and `parch`, Random Forest detected interactions, indicating these features may influence survival in certain conditions.

### Limitations and Future Work

1. **Data Quality**: Missing data, particularly in `cabin`, limited the analysis.
2. **Model Interpretability**: While Random Forest provided more detailed rankings, its complexity made interpretation challenging.
3. **Scalability**: Although designed for scalability, more extensive testing on larger datasets was limited due to resource constraints.

Future work could explore more advanced models like gradient boosting, apply the pipeline to larger datasets, and further investigate interactions between family dynamics and survival.

### Conclusion

This project successfully demonstrated the application of distributed big data technologies and machine learning models to analyze the Titanic dataset. Both models validated Hypotheses 1 and 2, while Hypotheses 3 and 4 were partially supported. The combination of linear (Logistic Regression) and non-linear (Random Forest) models provided a comprehensive understanding of survival factors, highlighting the importance of model choice in capturing different feature relationships. The results offer valuable lessons for similar predictive modeling tasks in other domains.
