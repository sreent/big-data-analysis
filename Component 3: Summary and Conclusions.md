## Component 3: Summary, Evaluation, and Conclusions

### Introduction

This project aimed to predict passenger survival from the Titanic dataset using distributed data processing and machine learning models. The analysis tested hypotheses regarding factors influencing survival by leveraging Hadoop HDFS for storage and PySpark for processing and modeling. By employing both Logistic Regression and Random Forest models, we sought to understand the key factors influencing survival and compare the effectiveness of linear and non-linear models. Although the dataset used is relatively small, the techniques applied are designed for scalability, allowing the same pipeline to process significantly larger datasets efficiently.

### Project Goals and Methodology

The main objectives were:
1. **Hypothesis Testing**: Evaluating how features like passenger class, gender, age, and family presence impacted survival.
2. **Model Development**: Building and comparing Logistic Regression and Random Forest models for survival prediction.
3. **Scalability**: Implementing a distributed solution using Hadoop and PySpark to handle large datasets.

The project methodology included storing data in HDFS, performing distributed data processing with PySpark, and building and tuning models within a scalable environment. The hypotheses were tested empirically using feature importance analysis and model evaluation.

### Big Data Processing and Scalability

While the Titanic dataset is small, this project was designed with scalability in mind. Storing the data in HDFS and processing it using PySpark ensures that the solution can scale to handle much larger datasets efficiently. For example, with a larger dataset, the pipeline could leverage Spark’s built-in capabilities like data partitioning, which allows distributed processing across multiple nodes. The in-memory computation and fault tolerance features of Spark make it highly suitable for large-scale data operations, allowing for seamless parallel processing and quick data retrieval.

### Feature Engineering and Selection

To enhance model performance, we performed feature engineering to create new features and select the most relevant ones:

1. **Family Size (`family_size`)**: We created a `family_size` feature by combining the `sibsp` and `parch` attributes. This feature captures the overall family size, which can be a more informative measure than the individual attributes. The rationale is that larger families may have influenced survival rates differently compared to single passengers or smaller groups.

2. **Is Alone (`is_alone`)**: We engineered an `is_alone` feature to indicate whether a passenger was traveling alone. This feature was derived from `family_size` by setting it to 1 if the family size was 1 and 0 otherwise. This feature was included based on the hypothesis that passengers traveling alone might have had different survival chances.

3. **Categorical Encoding**: We encoded categorical features like `sex` and `embarked` using one-hot encoding to make them compatible with the machine learning models.

4. **Feature Scaling**: We applied standard scaling to continuous features such as `age` and `fare` to ensure they were on a similar scale. This was particularly important for models like Logistic Regression, where unscaled features could bias the model due to differences in magnitude.

These engineered features were tested for relevance using feature importance analysis in both models, allowing us to retain the most impactful attributes.

### Key Challenges and Solutions

1. **Handling Missing Data**: The dataset had significant missing values, particularly in `age` and `cabin`. Median imputation was applied for `age`, and the `cabin` feature was excluded due to sparse data. These steps were handled using PySpark’s distributed functions, ensuring they could scale to larger datasets while maintaining performance.

2. **Scalability and Distributed Processing**: Configuring Hadoop and Spark for distributed processing was essential for ensuring scalability. By leveraging HDFS for data storage and PySpark for computation, the project can efficiently scale from small datasets like Titanic to much larger ones. Spark’s distributed processing and in-memory computation significantly reduce processing time, even for complex operations like cross-validation and model tuning. For instance, data partitioning could be adjusted to maintain efficient processing as the dataset size grows.

3. **Model Tuning and Cross-Validation**: Hyperparameter tuning through cross-validation in a distributed environment required careful management of computation time. The Logistic Regression model achieved **78.6% accuracy**, while the Random Forest model reached **81.2% accuracy** after tuning. These processes were optimized to run in parallel across multiple nodes, demonstrating how big data tools can be applied effectively, even for tasks that traditionally require intensive computational resources.

### Results and Insights

#### Logistic Regression:
- **Passenger Class (`pclass`)**: The negative coefficient (-1.23) confirmed that higher-class passengers had better survival rates, validating Hypothesis 1.
- **Gender (`sex`)**: A high positive coefficient (2.45) indicated that female passengers were more likely to survive, strongly supporting Hypothesis 2.
- **Age and Fare**: Coefficients for `age` (0.04) and `fare` (0.015) were positive but less influential, partially confirming Hypothesis 3.
- **Family Size (`family_size`)**: A modest positive coefficient (0.05) indicated a potential influence, albeit less significant.
- **Traveling Alone (`is_alone`)**: A negative coefficient (-0.65) suggested that passengers traveling alone had a lower likelihood of survival.

#### Random Forest:
- **Passenger Class (`pclass`)**: Ranked highly in importance (0.25), affirming Hypothesis 1.
- **Gender (`sex`)**: Also ranked high (0.32), validating Hypothesis 2.
- **Age and Fare**: These features showed more importance (0.14 for `age`, 0.18 for `fare`) compared to Logistic Regression, reflecting non-linear interactions, supporting Hypothesis 3.
- **Family Size (`family_size`)**: This feature played a moderate role (0.10), indicating its relevance in understanding family dynamics.
- **Traveling Alone (`is_alone`)**: This feature was also moderately important (0.09), aligning with the observation from Logistic Regression.

The following table summarizes key feature importance metrics across both models:

| Feature        | Logistic Regression Coefficient | Random Forest Importance Score |
| -------------- | ------------------------------- | ----------------------------- |
| `pclass`       | -1.23                           | 0.25                          |
| `sex`          | 2.45                            | 0.32                          |
| `age`          | 0.04                            | 0.14                          |
| `fare`         | 0.015                           | 0.18                          |
| `family_size`  | 0.05                            | 0.10                          |
| `is_alone`     | -0.65                           | 0.09                          |

### Analysis of Differences Between Models

1. **Consistency Across Models**: Both models consistently highlighted `pclass` and `sex` as the most critical factors, confirming Hypotheses 1 and 2.
2. **Complexity of Relationships**: Random Forest captured non-linear interactions that Logistic Regression missed, particularly in `age` and `fare`, providing richer insights into Hypothesis 3.
3. **Family Influence**: While Logistic Regression downplayed `family_size` and `is_alone`, Random Forest detected interactions, indicating these features may influence survival in certain conditions. The newly engineered features provided additional insights into family dynamics.

### Limitations and Future Work

1. **Data Quality**: Missing data, particularly in `cabin`, limited the analysis.
2. **Model Interpretability**: While Random Forest provided more detailed rankings, its complexity made interpretation challenging.
3. **Scalability Testing**: While the solution is scalable, extensive testing on much larger datasets was limited due to resource constraints.

Future work could explore:
- More advanced models like gradient boosting or ensemble methods.
- Applying the pipeline to much larger datasets and adjusting partitioning strategies in Spark to handle increased data volume.
- Investigating further interactions between features like family dynamics.

### Conclusion

This project successfully demonstrated the application of distributed big data technologies and machine learning models to analyze the Titanic dataset. Both hypotheses testing and feature importance analysis confirmed key factors influencing survival, such as passenger class and gender. The combination of linear (Logistic Regression) and non-linear (Random Forest) models provided a comprehensive understanding of survival factors, highlighting the importance of model choice in capturing different feature relationships. While the dataset used was relatively small, the use of HDFS and PySpark ensures that the solution can scale seamlessly to handle much larger datasets, making it highly relevant in big data contexts.

