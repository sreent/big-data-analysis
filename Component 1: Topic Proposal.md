## Component 1: Topic Proposal

### Introduction
In this project, we aim to analyze the Titanic dataset to build and evaluate machine learning models that predict passenger survival. The dataset contains detailed information about the passengers, such as age, sex, ticket class, and fare. Our goal is to leverage distributed data processing and machine learning techniques to identify key factors influencing survival and build predictive models. The analysis offers insights into historical survival patterns and can inform modern practices in areas such as safety protocols and emergency response strategies. Additionally, the project demonstrates scalable data processing methodologies applicable to other domains, making it relevant for diverse risk assessment applications.

### Data
The Titanic dataset from OpenML will be used for this project. This dataset, widely used for binary classification problems, contains 1,309 records with 14 attributes. Key attributes include:

- `pclass`: Passenger class (1 = 1st class, 2 = 2nd class, 3 = 3rd class)
- `survived`: Survival (0 = No, 1 = Yes)
- `name`: Name of the passenger
- `sex`: Sex of the passenger
- `age`: Age of the passenger
- `sibsp`: Number of siblings/spouses aboard the Titanic
- `parch`: Number of parents/children aboard the Titanic
- `ticket`: Ticket number
- `fare`: Passenger fare
- `cabin`: Cabin number
- `embarked`: Port of Embarkation (C = Cherbourg; Q = Queenstown; S = Southampton)
- `boat`: Lifeboat number
- `body`: Body identification number
- `home.dest`: Home/Destination

### Hypotheses
We will test the following hypotheses based on initial data insights and historical records:

1. **Hypothesis 1:** Passenger class (pclass) significantly affects the likelihood of survival.
   - **Justification:** Historical accounts indicate that higher-class passengers had better access to lifeboats, leading to higher survival rates among first-class passengers.

2. **Hypothesis 2:** Female passengers had a higher survival rate compared to male passengers.
   - **Justification:** The principle of "women and children first" during evacuations suggests that female passengers were prioritized.

3. **Hypothesis 3:** Age and fare are significant predictors of survival.
   - **Justification:** Younger passengers might have been more agile during evacuation, and higher fares likely correlate with better accommodations closer to lifeboats.

4. **Hypothesis 4:** The presence of siblings/spouses (sibsp) and parents/children (parch) aboard influences survival rates.
   - **Justification:** Family members may have supported each other during the evacuation, improving their chances of survival.

These hypotheses will be tested by evaluating feature importance and model coefficients from our machine learning models.

### Planned Analysis

Our analysis will involve the following steps:

1. **Set Up the Hadoop Environment:**
   - Configure the Hadoop environment to interact with HDFS.
   - **Rationale:** Setting up Hadoop is essential for managing large datasets and leveraging distributed processing for efficient data handling.

2. **Download and Save the Dataset:**
   - Use `sklearn` to fetch the Titanic dataset.
   - Save the dataset locally as a CSV file.
   - **Rationale:** Fetching and saving the dataset ensures a stable and consistent data source for analysis.

3. **Create a Folder in HDFS and Copy the CSV File:**
   - Create a folder in HDFS for the CSV file.
   - Copy the CSV file from the local system to HDFS.
   - **Rationale:** Storing the data in HDFS allows us to utilize Hadoop's distributed storage, which is crucial for large-scale data processing.

4. **Set Up the Spark Environment:**
   - Initialize `SparkSession` for data processing and machine learning tasks.
   - **Rationale:** `SparkSession` is the entry point to using Spark functionalities, necessary for performing operations on data stored in HDFS.

5. **Reading Data from HDFS:**
   - Read the Titanic dataset from HDFS into a Spark DataFrame.
   - **Rationale:** Loading the data into a Spark DataFrame allows us to leverage Spark's distributed computing capabilities for efficient data processing.

6. **Data Cleaning:**
   - Clean and preprocess the data to handle missing values and incorrect data types. Key steps include:
     - Imputing missing ages using median values or predictive models.
     - Categorizing cabin data by deck or proximity to lifeboats.
   - Summarize and visualize missing values to guide the cleaning process.
   - **Rationale:** Proper data cleaning ensures the accuracy of the analysis and the validity of the results. Visualization helps identify patterns in missing data that could inform the imputation strategy.

7. **Exploratory Data Analysis (EDA):**
   - Perform EDA to understand the distribution and relationships between features using visualizations like histograms, box plots, and pair plots.
   - Highlight key findings and patterns observed during EDA.
   - **Rationale:** EDA helps identify trends, patterns, and anomalies in the data, guiding feature engineering and model development.

8. **Feature Engineering and Scaling:**
   - Engineer relevant features using existing attributes:
     - For example, combining `sibsp` and `parch` into a single family size feature to capture the effect of family size on survival.
   - Standardize the features to ensure they are on a similar scale.
   - **Rationale:** Feature engineering enhances model performance by creating more informative features, while scaling ensures models treat each feature fairly during training.

9. **Data Splitting:**
   - Split the data into training and test sets.
   - **Rationale:** Splitting the data allows for model training on one subset while preserving another for unbiased evaluation, reducing the risk of overfitting.

10. **Building and Tuning Multiple Machine Learning Models:**
    - Build and tune Logistic Regression, Decision Tree, and Random Forest models using PySpark.
    - Use cross-validation to optimize hyperparameters.
    - **Rationale:** Cross-validation provides a robust method for model evaluation and hyperparameter tuning, ensuring that the models generalize well to unseen data.

11. **Summarize and Conclude the Analysis:**
    - Compare model accuracies and summarize the results.
    - Analyze feature importances and coefficients to understand the impact of each feature on survival.
    - Validate the hypotheses using feature importance scores:
      - For Hypothesis 1: Significant coefficients or high importance scores for `pclass`.
      - For Hypothesis 2: Significant coefficients or high importance scores for `sex`.
      - For Hypothesis 3: Significant coefficients or high importance scores for `age` and `fare`.
      - For Hypothesis 4: Significant coefficients or high importance scores for `sibsp` and `parch`.
    - Discuss potential implications of the findings, including how they might inform current safety protocols, and any limitations encountered, such as potential biases in the dataset or the models.
    - **Rationale:** This step synthesizes the entire analysis, linking the results back to the original hypotheses and discussing their broader implications.

### Technologies

The following technologies will be used to carry out the analysis:
- **Data Storage:** Hadoop HDFS for storing the dataset.
- **Data Processing and Machine Learning:** Apache Spark and Spark MLlib for data processing and building machine learning models.
- **Programming Language:** PySpark for coding and implementing the analysis.

**Rationale:** These technologies are chosen for their ability to handle large datasets and perform distributed computing, which is essential for the scale and complexity of this analysis.

### Relevance

The Titanic dataset provides a classic example for binary classification problems, allowing us to apply and demonstrate distributed data processing and machine learning techniques effectively. The project is relevant for understanding the impact of different features on survival and building predictive models that can be applied to similar classification problems. By understanding these factors, we can improve current practices in related fields such as safety protocols and emergency response strategies. This analysis also has broader implications for any situation where survival predictions could be critical, such as in disaster response or healthcare.

### Exploratory and Summary Results

Initial exploration of the dataset shows that the survival rate is influenced by multiple factors such as passenger class, sex, and age. Summary statistics and visualizations will illustrate these relationships and guide further analysis. For example, initial histograms and pair plots indicate that first-class passengers and female passengers had higher survival rates. These insights will guide the feature engineering and model-building process, ensuring that the most relevant features are used in the predictive models.

### Conclusion and Limitations

The proposed analysis will provide a comprehensive understanding of the factors influencing survival on the Titanic, validated through rigorous machine learning models. However, the analysis may be limited by the quality and completeness of the data, as well as the assumptions made during data cleaning and feature engineering. Additionally, the models' performance is contingent on the availability of sufficient computational resources, given the scale of distributed processing required. Future work could extend this analysis to other datasets or explore more complex models such as ensemble methods or deep learning.

### References

- OpenML: Titanic Dataset [https://www.openml.org/d/40945]
- PySpark Documentation [https://spark.apache.org/docs/latest/api/python/index.html]
- Hadoop HDFS Documentation [https://hadoop.apache.org/docs/r3.3.0/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html]
