# Propensity-Capstone-Project
## _Propensity Model to Identify How Likely Certain Target Groups Customers Respond To The Marketing Campaign_

# Objective
This project is aimed at building a propensity model to identify potential customers for an insurance company to develop a tool to optimize their marketing efforts.

# Description
Propensity modeling is a method that aims to forecast the chance that individuals, leads, and customers will engage in specific actions. This method uses statistical analysis which takes into account all the independent and confounding factors that impact customer behavior.

# Data
The insurance company has provided a historical data set (train.csv). The company has also provided you with a list of potential customers to whom to market (test.csv). From this list of potential customers, we need to determine yes/no whether we wish to market to them.

#### Input Variables:
custAge, profession, marital, schooling, default, housing, loan, contact, month, day_of_week, campaign, pdays, previous, poutcome, emp.var.rate, cons.price.idx, cons.conf.idx, euribor3m, nr.employed, pmonths, pastEmail

#### Output Variables:
responded

# Steps involved in building the model and identify target customers
### Started with importing necessary libraries
- Basic libraries like pandas, numpy, matplotlib, seaborn and warnings
- Z-score for outlier treament
- Preprocessing Libraries, Models , Evaluation Metrics
- Hyperparameter Tuning Libraries and Cross Validation Libraries
### Train Dataset Details
- Total number of rows in data: 8240
- Total number of columns: 24
### Deleting Unwanted rows and columns 
- Dropped last 2 rows as they are sum and average of profit column.
- Drooped id and profit columns as they are not necessary as of now.
### Exploratory Data Analysis
- Data info to know about data types and null values.
- Data describe to get a overview of Descriptive Statistics of numerical columns.
- ### Duplicate values
   - As the dataset is having 36 duplicated rows dropped all duplicate rows.
- ### Null Values
   - To find the null values used isnull() and ploted bar chart.
   - To handle null values , filled all null values using Forwardfill.
- ### Outliers
   - Before finding outliers replaced '999' value in pdays and pmonths columns to -1 to identify never contacted as '999' can be treated as outlier and effect the analysis.
   - To view the outliers used boxplot to visualize the outlier values.
   - Used Z-scores to find the rows with outlier values from custAge, campaign, pdays and pastEmail columns.
   - Handled outliers by removing the outlier rows and saved all remaining rows as cleaned_data.
- ### Data visualization
    - Before visualizing and analyzing the data seperated the categorical and numerical columns.
    - Visualized the data based on target column 'responded' in plots per below:
    - Plot 1: Distribution of customer age who responded for marketing and not responded.
    - Plot 2: Response based on Profession of the customer.
    - Plot 3: Response of customer who have housing loan or not.
    - Plot 4: Histplot for Marital Status.
    - Plot 5: Pairplot to understand the distribution between numerical columns.
    - Plot 6: Distribution of categorical columns using countplot.
    - Plot 7: Distribution of numerical columns using Boxplot.
    - Plot 8: Voilin Plot to display the density of each value in each numerical columns.
    - Plot 9: Distribution on Outcome with responded column
    - Plot 10: Plot for Response Based on Previous Contact Month
    - Plot 11: Response Based on Contact Type
    - Plot 12: Distribution of employee variance rate on target column
    - Plot 13: Distribution on No. of Employees
    - Plot 14: Response on No. of times contacted
    - Plot 15: Countplot to find out how balanced the data is in target column.
### Feature Engineering  
-  #### Encoding
  -  Encoded all categorical columns using Label Encoder.
-  #### Scaling
  -  Scaled all numerical columns using Standard Scaler
### Split Train and Test Data
  - Defined X with all columns except target column and y with target column
  - Did train and test split on data using train test split library.  - 
- #### Sampling Trainig Dataset
    - As the dataset is highly imbalanced on target column we need perform any sampling technique.
    - Using RandomUnderSampler undersampled the training dataset.
    - Using SMOTE oversampled the undersampeld training dataset.
### Model Selection
- As the output variable is a classification output we can perform multiple classification Models.
- Models opted are
  - Logistic Regression
  - Desicion Tree Classifier
  - Random Forest Classifier
  - Gradient Boosting Classifier
  - Support Vector Classifier
  - KNeighbours Classifier
  - XG Boosting Classifier
  - Neural Network Classifier
### Model Training and Testing
- Trained all models with the resampled training data.
- Made predictions with test data.
### Model Evaluation
- Evaluated all models performance using evaluation metrics like :
  - Accuracy Score
  - ROC AUC Score
  - Classification Report.
  - Confusion Matrix
  - ROC Curve plot
### Best Model Evaluation
- Using a forloop determined best model with minimun threshold of 0.80.
- XG Boosting Classifier Model turned out to BEST MODEL with highest Accuracy of 0.90.
### Hyperparameter Tuning
- Performed RandomSearch CV with XG Boosting Classifier model as it was best from all trained classification models.
- Trained the grid search with original training dataset.
- With best estimator from Grid Search CV predicted the test datset achieved an accuracy increase to 0.91 for best estimator of XG Boosting Classifier.
- So, the model performance increased by hyperparameter tuning.
### Cross Validation
- Cross validated the model evaluation using 5 folds and achived an accuracy of 0.90%
- The best estimator achieved an accuracy of approximately 91.3%, which is consistent with the cross-validation accuracy of 90.3%. This suggests that the chosen hyperparameters provide a stable and reliable model with minimal variance across different folds.
### Feature Importance
- Feature importances indicate the contribution of each feature to the model's predictions.A higher importance value suggests a stronger influence on the model's decision-making.
- Features with the highest importance:
   - 'nr.employed' (30.01%) and 'emp.var.rate' (12.62%) significantly impact the model, indicating that economic factors play a crucial role in predicting the outcome.
### Predictions on Unseen Data
- As provided with test.csv file and asked to predict and add a column in that set to identify the potential customer to go with marketing followed below steps;
  - Read test.csv file.
  - Handled null values.
  - Repalced 999 with -1 in pdays and pmonths columns.
  - Seperated categorical columns and numerical columns.
  - Encoded categorical columns.
  - Scaled numerical columns.
  - And predicted Marketing Decision as 1(yes) or 0 (No) using Best model from hyperparameter tuning.
  - Created a column Marketing Decision using predictions.

**_As the test data is encoded and scaled we cannot get exact idea from these rows, to get exact list of Customers that can be contacted for marketing, read the test.csv again into candidates and added the predictions into Marketing Decision Column and displayed all potential customers rows.Exported the potential customers list to new excel file marketing_list._**



## Difficulties Faced
- Couldn't select exact plot to understand the analysis so tried to create all types of plots.
- As the dataset is having very high null values, finding better imputing method took time.
- As the dataset is highly imbalanced finding suitable sampling technique is a bit hard, found undersample could help better for high imbalance so used oversampling over undersampling.


# Conclusion:
- **The hyperparameter tuning process using RandomizedSearchCV significantly improved the XGBoost classifier's performance, resulting in a model with an accuracy of approximately 91.4%.** 
- **Cross-validation results further validate the model's consistency.**
- **Feature importance analysis highlighted the critical role of economic factors, specifically 'nr.employed' and 'emp.var.rate.'**

***Overall, the tuned XGBoost model showcases robustness, but continuous monitoring and potential adjustments are crucial for adapting to evolving data patterns and improving predictive capabilities.The Propensity project for predicting potential customers has been an exciting journey in harnessing the power of data for effective marketing. With advanced algorithms and insightful analysis, I've crafted a tool that identifies potential customers.The potential customer list, combined with strategic insights, positions us for a targeted and impactful marketing campaign that aligns with the preferences and behaviors of our customers.***



##                                                             _**Thank you!**_

