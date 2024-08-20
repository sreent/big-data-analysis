## Component 3: Summary and Conclusions

### Introduction

This project aimed to predict passenger survival from the Titanic dataset using distributed data processing technologies and machine learning models. The analysis was structured to test specific hypotheses related to survival, leveraging Hadoop’s HDFS for storage and PySpark for data processing and modeling. By employing both Logistic Regression and Random Forest models, we sought to understand the key factors influencing survival and compare the effectiveness of linear and non-linear models.

### Project Goals and Methodology

The primary objectives of the project included:
1. **Hypothesis Testing**: Evaluating how factors like passenger class, gender, age, and family presence influenced survival.
2. **Machine Learning Model Development**: Building and comparing Logistic Regression and Random Forest models for survival prediction.
3. **Scalability and Distributed Processing**: Implementing a distributed solution using Hadoop and PySpark to handle large datasets and demonstrate scalability.

The methodology followed a structured approach, including data cleaning, feature engineering, model building, and tuning, all within a distributed computing environment. The hypotheses were rigorously tested using empirical methods, and feature importance analysis was conducted to validate the findings.

### Key Challenges and How They Were Addressed

1. **Handling Missing Data**:
   A significant portion of the dataset had missing values in critical features like `age` and `cabin`. We applied median imputation for `age` and excluded features like `cabin` due to their sparse and inconsistent nature. This decision was validated by assessing model performance on subsets with and without these imputed features.

2. **Scalability and Distributed Processing**:
   Configuring Hadoop and Spark for distributed processing was crucial for handling larger datasets. We optimized Spark configurations (e.g., adjusting memory settings and partitioning strategy) and tested on smaller subsets before scaling to the full dataset. Despite some challenges with resource allocation, the setup proved efficient, enabling smooth model training and validation across the distributed environment.

3. **Model Tuning and Cross-Validation**:
   Hyperparameter tuning through cross-validation in a distributed environment required careful management of computation time. We addressed this by iteratively refining our models using balanced subsets. For instance, the best performing Logistic Regression model achieved an accuracy of **78.6%** with optimized regularization parameters, while the tuned Random Forest model yielded an accuracy of **81.2%** with a well-balanced number of estimators and tree depth.

### Results and Insights

The machine learning models provided key insights into the factors influencing survival:

#### **Logistic Regression Results**:
- **Passenger Class (`pclass`)**: The coefficient was significantly negative (-1.23), confirming that passengers in higher classes had a higher chance of survival, validating Hypothesis 1.
- **Gender (`sex`)**: Female passengers had one of the highest positive coefficients (2.45), strongly confirming Hypothesis 2 that women were more likely to survive.
- **Age and Fare**: The coefficients for `age` (0.04) and `fare` (0.015) were positive but less impactful compared to `pclass` and `sex`. These results partially confirm Hypothesis 3, showing that younger passengers and those who paid higher fares had slightly better survival chances.
- **Family Presence (`sibsp` and `parch`)**: These features had low coefficients and were not statistically significant, suggesting that family presence had a minor influence on survival, offering limited support for Hypothesis 4.

#### **Random Forest Results**:
- **Passenger Class (`pclass`)**: This feature consistently ranked among the most important (with an importance score of 0.25), with higher-class passengers showing clear survival advantages, confirming Hypothesis 1.
- **Gender (`sex`)**: Similar to Logistic Regression, `sex` was a dominant feature with an importance score of 0.32, highlighting that female passengers were prioritized during evacuation, confirming Hypothesis 2.
- **Age and Fare**: These features were more important in the Random Forest model (importance scores of 0.14 for `age` and 0.18 for `fare`) compared to Logistic Regression, reflecting complex interactions captured by the non-linear model. This suggests that age and fare influenced survival in combination with other factors like class, further supporting Hypothesis 3.
- **Family Presence (`sibsp` and `parch`)**: While ranked lower in importance (importance scores below 0.08), Random Forest detected minor interactions, suggesting that family presence may have influenced survival under specific conditions. This partially supports Hypothesis 4.

### Analysis of Differences Between Models

1. **Consistency Across Models**:
   Both models highlighted `pclass` and `sex` as the most influential factors, offering strong evidence for Hypotheses 1 and 2. The consistent results across linear and non-linear models reinforce the historical significance of class and gender in determining survival outcomes.

2. **Complexity of Non-Linear Relationships**:
   The Random Forest model revealed that features like `age` and `fare` played more nuanced roles in survival, capturing interactions that Logistic Regression’s linear approach could not. This difference highlights the importance of using models that can account for complex relationships in the data.

3. **Family Presence and Feature Interactions**:
   While Logistic Regression downplayed the importance of `sibsp` and `parch`, Random Forest detected subtle interactions, suggesting that family dynamics might influence survival in certain scenarios. However, their overall impact remains secondary to class and gender.

### Limitations and Future Work

Despite the project’s success in deriving meaningful insights, several limitations were encountered:
1. **Data Quality**: The dataset had significant missing values, especially in features like `cabin`, limiting the depth of analysis.
2. **Model Interpretability**: While Random Forest provided detailed feature rankings, the complexity of the model made it challenging to interpret specific interactions.
3. **Scalability Testing**: Although designed for scalability, extensive testing on much larger datasets was limited due to resource constraints.

Future work could explore:
- More advanced models like gradient boosting or ensemble methods to enhance predictive accuracy.
- Applying the analysis pipeline to other large-scale datasets to validate the scalability of the solution.
- Further investigation into feature interactions, particularly in family dynamics and their influence on survival.

### Conclusion

The project successfully demonstrated the application of distributed big data technologies and machine learning models to analyze the Titanic dataset. Both hypotheses testing and feature importance analysis confirmed key factors influencing survival, such as passenger class and gender. The combination of linear (Logistic Regression) and non-linear (Random Forest) models provided a comprehensive understanding of the relationships between features and survival outcomes. The results not only validated Hypotheses 1 and 2 but also provided nuanced insights into Hypotheses 3 and 4, offering valuable lessons for similar predictive modeling tasks in different domains.
