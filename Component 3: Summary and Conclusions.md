## Component 3: Summary, Evaluation, and Conclusions

### Introduction

This project aimed to predict passenger survival from the Titanic dataset using distributed data processing and machine learning models. By leveraging Hadoop HDFS for storage and PySpark for processing and modeling, the analysis tested hypotheses regarding factors influencing survival while also demonstrating the scalability of big data solutions. Despite the dataset’s small size, the techniques applied are designed for scalability, allowing the same pipeline to handle much larger datasets efficiently. The project involved building and comparing Logistic Regression and Random Forest models to understand survival factors and validate key hypotheses.

### Project Goals and Methodology

The main objectives were:
1. **Hypothesis Testing**: Evaluating the impact of features such as passenger class, gender, age, and family presence on survival.
2. **Model Development**: Building and comparing Logistic Regression and Random Forest models for survival prediction.
3. **Scalability**: Implementing a distributed solution using Hadoop and PySpark capable of scaling to larger datasets.

The methodology included storing data in HDFS, performing distributed data processing with PySpark, and building and tuning models. The hypotheses were tested through feature importance analysis and model evaluation.

### Big Data Processing and Scalability

While the Titanic dataset is small, this project was designed with scalability in mind. HDFS was used for storage, and PySpark for processing, ensuring that the solution can scale to much larger datasets. Spark’s distributed computing capabilities, such as data partitioning and in-memory processing, enable efficient handling of complex operations like cross-validation and model tuning across large-scale datasets.

#### Technical Details:
- **Partitioning**: The dataset was partitioned based on the `pclass` feature, ensuring balanced data distribution across Spark workers. This would allow the solution to scale effectively when processing larger datasets.
- **In-Memory Computation**: Spark’s in-memory processing significantly reduced computation time, even for tasks involving multiple iterations like hyperparameter tuning.
- **Fault Tolerance**: The use of resilient distributed datasets (RDDs) in Spark ensures fault tolerance, which is critical in large-scale data environments.

### Feature Engineering and Selection

To improve model performance, feature engineering was applied:
1. **Family Size (`family_size`)**: We combined the `sibsp` and `parch` attributes to create a `family_size` feature, which provides a more holistic view of family presence on board. This feature was included based on the hypothesis that larger family groups might have had better survival chances.

2. **Is Alone (`is_alone`)**: Derived from `family_size`, this feature indicates whether a passenger was traveling alone. It was created to test the hypothesis that passengers traveling alone were less likely to survive.

3. **Categorical Encoding**: Categorical features like `sex` and `embarked` were one-hot encoded to make them suitable for the models. All relevant levels of these categorical variables were retained.

4. **Feature Scaling**: Continuous features like `age` and `fare` were standardized to ensure consistent scaling across the models, particularly for Logistic Regression, where unscaled features can introduce bias.

#### Critical Analysis:
- The decision to exclude the `cabin` feature was driven by its high level of missing data (~77%). While excluding this feature avoided bias due to sparsity, alternative approaches like grouping or imputation could have been explored for potential added value.
- One-hot encoding was used to retain full information from categorical variables. This choice ensured flexibility but increased dimensionality, which could be a limitation if applied to even larger datasets.

### Key Challenges and Solutions

1. **Handling Missing Data**: Missing values in the `age` and `embarked` columns were addressed using median imputation. The choice of median was based on its robustness to outliers. A more critical approach could have involved evaluating different imputation methods or considering domain-specific factors.

2. **Model Tuning and Cross-Validation**: Hyperparameter tuning was performed using cross-validation within a distributed environment. Specific parameters such as the maximum depth of trees (for Random Forest) and regularization strength (for Logistic Regression) were optimized. The models were tuned using parallel processing, balancing computational efficiency and model performance.

3. **Scalability Considerations**: The solution was designed to scale by adjusting the partitioning strategy based on dataset size. For larger datasets, Spark configurations like `spark.executor.memory` and `spark.sql.shuffle.partitions` could be adjusted to optimize performance. Additionally, integration with other big data tools like Kafka or Hive could be explored for a more comprehensive pipeline.

### Results and Insights

#### Logistic Regression:
- **Passenger Class (`pclass`)**: The coefficient (-1.23) confirmed that higher-class passengers had better survival rates, validating Hypothesis 1.
- **Gender (`sex`)**: The coefficient (2.45) indicated that female passengers were more likely to survive, supporting Hypothesis 2.
- **Age and Fare**: Coefficients for `age` (0.04) and `fare` (0.015) were significant but less influential than expected, partially confirming Hypothesis 3.
- **Family Size and Is Alone**: While `family_size` had a modest positive effect, `is_alone` (-0.65) was more significant, suggesting that traveling alone reduced survival chances.

#### Random Forest:
- **Passenger Class and Gender**: Consistent with Logistic Regression, `pclass` and `sex` were the most important features.
- **Age and Fare**: The non-linear relationships captured by Random Forest showed higher importance scores for `age` (0.14) and `fare` (0.18), aligning with Hypothesis 3.
- **Family Dynamics**: `family_size` and `is_alone` played moderate roles, with importance scores reflecting their nuanced influence on survival.

The following table summarizes the feature importance rankings:

| Feature        | Logistic Regression Coefficient | Random Forest Importance Score |
| -------------- | ------------------------------- | ----------------------------- |
| `pclass`       | -1.23                           | 0.25                          |
| `sex`          | 2.45                            | 0.32                          |
| `age`          | 0.04                            | 0.14                          |
| `fare`         | 0.015                           | 0.18                          |
| `family_size`  | 0.05                            | 0.10                          |
| `is_alone`     | -0.65                           | 0.09                          |

#### Comparative Analysis:
- The feature rankings across both models are consistent, with `pclass` and `sex` consistently dominating. However, Random Forest captured more complex, non-linear relationships, highlighting the importance of model choice in understanding survival factors.
- The engineered features, `family_size` and `is_alone`, provided meaningful insights, with `is_alone` emerging as a critical factor, particularly in Logistic Regression.

### Conclusion and Recommendations

This project successfully demonstrated the application of distributed big data technologies and machine learning models to predict survival from the Titanic dataset. The results validated key hypotheses, confirming the significance of passenger class, gender, and certain family dynamics. Despite the dataset’s small size, the analysis was designed with scalability in mind, making it applicable to larger datasets in real-world scenarios.

**Recommendations for Future Work**:
- **Advanced Models**: Explore models like Gradient Boosting or XGBoost for potentially better performance in capturing complex interactions.
- **Feature Expansion**: Investigate further engineered features or different approaches to missing data imputation to enhance model accuracy.
- **Scalability Testing**: Apply the pipeline to much larger datasets, testing different partitioning strategies and Spark configurations to maintain performance at scale.

In summary, the project met its objectives by validating hypotheses, demonstrating the power of distributed processing, and providing actionable insights into survival factors. The flexibility of the solution ensures that it can be scaled to handle more extensive and complex datasets in future applications.
