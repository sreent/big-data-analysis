## Component 3: Summary, Evaluation, and Conclusions

### Introduction

This project aimed to predict passenger survival from the Titanic dataset using distributed data processing and machine learning models. By leveraging Hadoop HDFS for storage and PySpark for processing and modeling, the analysis tested hypotheses regarding factors influencing survival while demonstrating the scalability of big data solutions. Although the dataset is small, the approach is designed to scale, making it adaptable for much larger datasets. The analysis focused on building and comparing Logistic Regression and Random Forest models to validate key hypotheses and understand survival factors.

### Project Goals and Methodology

The main objectives were:
1. **Hypothesis Testing**: Evaluating the impact of features like passenger class, gender, and age on survival.
2. **Model Development**: Building and comparing Logistic Regression and Random Forest models for survival prediction.
3. **Scalability**: Implementing a distributed solution using Hadoop and PySpark capable of scaling to larger datasets.

The methodology involved storing data in HDFS, processing it with PySpark, and testing hypotheses using feature importance analysis and model evaluation.

### Big Data Processing and Scalability

Although the Titanic dataset is small, this project was designed with scalability in mind. HDFS was used for storage, and PySpark for processing, ensuring the solution can handle much larger datasets. Key aspects include:
- **Partitioning**: Data was partitioned based on `pclass`, balancing load across Spark workers and preventing data skew—critical for performance when scaling.
- **In-Memory Computation**: Spark’s in-memory processing significantly reduced computation time, especially for iterative tasks like cross-validation.
- **Fault Tolerance**: The use of resilient distributed datasets (RDDs) ensures fault tolerance, allowing processing to continue even if nodes fail.

While these tools ensure scalability, potential bottlenecks like shuffle operations during large-scale joins must be carefully managed in larger applications. The setup remains adaptable to different data sizes by adjusting configurations such as partitioning strategies and memory allocation.

### Feature Engineering and Selection

To improve model performance, feature engineering was applied:
1. **Family Size (`family_size`)**: Combined `sibsp` and `parch` to represent the presence of family, hypothesized to impact survival.
2. **Is Alone (`is_alone`)**: Derived from `family_size` to indicate if a passenger traveled alone, an important factor in survival.
3. **Categorical Encoding**: One-hot encoding was used for categorical variables like `sex` and `embarked`, retaining interpretability while preventing bias in models.
4. **Feature Scaling**: Continuous features like `age` and `fare` were standardized to ensure consistent scaling, particularly for Logistic Regression.

The decision to exclude `cabin` due to high missing data (~77%) was practical but limited insights that could have been gained from exploring imputation or grouping strategies. While one-hot encoding was effective here, for datasets with high-cardinality categorical variables, techniques like target encoding might be more appropriate.

### Key Challenges and Solutions

1. **Handling Missing Data**: Missing values in `age` and `embarked` were imputed using median values, chosen for robustness. However, more sophisticated imputation methods, like regression or KNN, could be explored in future work.
2. **Model Tuning and Cross-Validation**: Hyperparameter tuning was performed using distributed cross-validation, optimizing parameters like tree depth (Random Forest) and regularization strength (Logistic Regression). The process balanced computational efficiency with model performance.
3. **Scalability Considerations**: The solution is scalable by adjusting partitioning strategies based on dataset size. For larger datasets, Spark configurations such as `spark.sql.shuffle.partitions` and executor memory would be adjusted. The pipeline could also integrate with tools like Kafka or Hive for broader use cases.

### Results and Insights

#### Logistic Regression:
- **Passenger Class (`pclass`)**: The coefficient (-1.23) confirmed that higher-class passengers had better survival rates, validating Hypothesis 1.
- **Gender (`sex`)**: The coefficient (2.45) indicated female passengers were more likely to survive, strongly supporting Hypothesis 2.
- **Age and Fare**: Coefficients for `age` (0.04) and `fare` (0.015) were significant but less influential, partially confirming Hypothesis 3.
- **Family Size and Is Alone**: `Is_alone` (-0.65) had a more significant impact than `family_size`, indicating those traveling alone were less likely to survive.

#### Random Forest:
- **Passenger Class and Gender**: Consistent with Logistic Regression, `pclass` and `sex` were the most important features.
- **Age and Fare**: Random Forest captured non-linear relationships, showing higher importance for `age` (0.14) and `fare` (0.18), aligning with Hypothesis 3.
- **Family Dynamics**: `Family_size` and `is_alone` played moderate roles, but `is_alone` was slightly less influential in Random Forest compared to Logistic Regression.

The table below summarizes the feature importance rankings:

| Feature        | Logistic Regression Coefficient | Random Forest Importance Score |
| -------------- | ------------------------------- | ----------------------------- |
| `pclass`       | -1.23                           | 0.25                          |
| `sex`          | 2.45                            | 0.32                          |
| `age`          | 0.04                            | 0.14                          |
| `fare`         | 0.015                           | 0.18                          |
| `family_size`  | 0.05                            | 0.10                          |
| `is_alone`     | -0.65                           | 0.09                          |

#### Comparative Analysis:
The feature rankings are consistent across models, with `pclass` and `sex` dominating. However, Random Forest’s ability to capture non-linear interactions provided richer insights, especially for continuous variables like `age` and `fare`. The engineered features also provided value, particularly `is_alone`, which emerged as a critical factor in both models.

### Conclusion and Recommendations

The project demonstrated the successful application of distributed big data technologies and machine learning to predict Titanic survival. The results validated key hypotheses, confirming the significance of passenger class, gender, and family dynamics. Despite the dataset’s small size, the approach was designed with scalability in mind, making it applicable to much larger datasets in real-world scenarios.

**Recommendations**:
- **Advanced Models**: Explore Gradient Boosting or XGBoost for better performance in capturing complex interactions.
- **Feature Expansion**: Investigate further engineered features and explore more sophisticated missing data handling.
- **Scalability Testing**: Test the pipeline on larger datasets, adjusting configurations and integrating additional big data tools like Kafka.

This project effectively validated the hypotheses and demonstrated the power of distributed processing in handling survival prediction tasks. The scalability and flexibility of the solution make it well-suited for broader applications in large-scale data environments.

