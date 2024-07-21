## Component 1: Topic Proposal

### Introduction
In this project, we aim to analyze the Titanic dataset to build and evaluate machine learning models that predict passenger survival. The Titanic dataset contains detailed information about the passengers on the Titanic, such as their age, sex, ticket class, and fare. Our goal is to leverage distributed data processing and machine learning techniques to understand the factors that influenced survival and to build predictive models. Understanding these factors can provide insights into historical survival patterns and improve current practices in areas such as safety protocols and emergency response strategies. This analysis can also serve as a benchmark for similar predictive modeling tasks in different domains.

### Data
The Titanic dataset from OpenML will be used for this project. This dataset is widely used for binary classification problems and contains 1,309 records with 14 attributes. Key attributes include:
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
We will test the following hypotheses based on initial data insights and prior research:
1. **Hypothesis 1:** Passenger class (pclass) significantly affects the likelihood of survival. Prior research indicates that higher-class passengers had better access to lifeboats.
2. **Hypothesis 2:** Female passengers had a higher survival rate compared to male passengers. Historical accounts suggest that women and children were given priority during evacuation.
3. **Hypothesis 3:** Age and fare are significant predictors of survival. Younger passengers and those who paid higher fares may have had better chances of survival.
4. **Hypothesis 4:** The presence of siblings/spouses (sibsp) and parents/children (parch) aboard influences survival rates. Family members may have helped each other during the evacuation.

### Planned Analysis
Our analysis will involve the following steps:

1. **Set Up the Hadoop Environment:**
   - Configure the Hadoop environment to enable interaction with HDFS.

2. **Download and Save the Dataset:**
   - Use sklearn to fetch the Titanic dataset.
   - Save the dataset locally as a CSV file.

3. **Create a Folder in HDFS and Copy the CSV File:**
   - Create a folder in HDFS for the CSV file.
   - Copy the CSV file from the local system to HDFS.

4. **Set Up the Spark Environment:**
   - Initialize SparkSession for data processing and machine learning tasks.

5. **Reading Data from HDFS:**
   - Read the Titanic dataset from HDFS into a Spark DataFrame.

6. **Data Cleaning:**
   - Clean and preprocess the data to handle missing values and incorrect data types. For example, impute missing ages and categorize cabin data.
   - Summarize and visualize missing values to guide the cleaning process.

7. **Exploratory Data Analysis (EDA):**
   - Perform EDA to understand the distribution and relationships between features. This includes visualizations like histograms, box plots, and pair plots.
   - Highlight key findings and patterns observed during EDA.

8. **Feature Engineering and Scaling:**
   - Engineer relevant features using existing attributes (e.g., combining `sibsp` and `parch` into a single family size feature).
   - Standardize the features to ensure they are on a similar scale.
   - Justify the choice of features and transformations applied.

9. **Data Splitting:**
   - Split the data into training and test sets.

10. **Building and Tuning Multiple Machine Learning Models:**
    - Build and tune Logistic Regression, Decision Tree, and Random Forest models using PySpark.
    - Use cross-validation to optimize hyperparameters.
    - Document the process and rationale for hyperparameter selection.

11. **Summarize and Conclude the Analysis:**
    - Compare model accuracies and summarize the results.
    - Analyze feature importances and coefficients to understand the impact of each feature on survival.
    - Use the feature importance scores to validate the hypotheses:
      - For Hypothesis 1: Significant coefficients or high importance scores for `pclass`.
      - For Hypothesis 2: Significant coefficients or high importance scores for `sex`.
      - For Hypothesis 3: Significant coefficients or high importance scores for `age` and `fare`.
      - For Hypothesis 4: Significant coefficients or high importance scores for `sibsp` and `parch`.
    - Discuss potential implications of the findings and any limitations encountered.

### Technologies
The following technologies will be used to carry out the analysis:
- **Data Storage:** Hadoop HDFS for storing the dataset.
- **Data Processing and Machine Learning:** Apache Spark and

 Spark MLlib for data processing and building machine learning models.
- **Programming Language:** PySpark for coding and implementing the analysis.

### Relevance
The Titanic dataset provides a classic example for binary classification problems, allowing us to apply and demonstrate distributed data processing and machine learning techniques effectively. The project will be relevant for understanding the impact of different features on survival and building predictive models that can be applied to similar classification problems. By understanding these factors, we can improve current practices in related fields such as safety protocols and emergency response strategies.

### Exploratory and Summary Results
Initial exploration of the dataset shows that the survival rate is influenced by multiple factors such as passenger class, sex, and age. Summary statistics and visualizations will be provided to illustrate these relationships and to guide further analysis. For example, initial histograms and pair plots indicate that first-class passengers and female passengers had higher survival rates.

### References
- OpenML: Titanic Dataset [https://www.openml.org/d/40945]
- PySpark Documentation [https://spark.apache.org/docs/latest/api/python/index.html]
- Hadoop HDFS Documentation [https://hadoop.apache.org/docs/r3.3.0/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html]
