<h1>Diabetes Prediction System</h1>

_Diabetes is a chronic disease where the pancreas either does not produce insulin or the body is not able to effectively use the insulin, causing dangerously high levels of blood glucose. Without treatment, acute diabetes can lead to death. Even with management, diabetes takes a toll over time on the person's nervous system, blood vessels, and eyesight. [[1]](https://www.who.int/news-room/fact-sheets/detail/diabetes) Type 1 diabetes typically has early age onset and the cause is currently unknown. Type 2 diabetes and Gestational diabetes, however, have known risk factors that be tracked such as smoking, obesity, phyisical inactivity, A1C, high blood pressure, and high cholesterol. [[2]](https://www.cdc.gov/diabetes/php/data-research/index.html) Monitoring the risk factors can help catch diabetes in the early stage or in some cases even mitigate the risk for people who are pre-diabetic. Today, approximately 8.7 million adults in the United States meet the criteria and are like diabetic, yet are undiagnosed and not receiving treatment. The goal here is to create a model that effectively predicts diabetes can be valuable and in doing so, improve outcomes and quality of life for the undiagnosed population._

<h2>1. Data</h2>

The dataset used is originally from the National Institute of Diabetes & Digestive & Kidney Disease. The objective when they collected this data was to predict based on diagnostic measurements whether a patient has diabetes.

* [Kaggle Website Source](https://www.kaggle.com/datasets/mathchi/diabetes-data-set)
* [Kaggle Dataset](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/data/diabetes.csv)

<h2>2. Data Cleaning</h2>

[Data Cleaning Report](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/Capstone%202%20Diabetes%20Project.ipynb)

* **Problem 1:** Inconsistencies in completeness of data entry. **Solution:** Null values were filled in with the mean or median, as appropriate for the various independent variables.
* **Problem 2:** Outliers were present throughout the independent variable values. **Solution:** Initial visualizations were done with histograms in order to get a sense of how far the distribution might be from normal. Outliers were later explored further using boxplots, then severe outliers were trimmed from the data.

![Boxplot](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/images/OutliersinBoxplot.png)

<h2>3. EDA</h2>

[EDA Report](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/Sarah.Berkin--EDA-Capstone%202%20Diabetes%20Project.ipynb)

* A heatmap was generated to visualize correlations between the variables

![Heatmap](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/images/CorrelationHeatmap.png)

* The 3 independent variables which had the lowest p-value from the Pearson Correlation Coefficient test were 1) Glucose, 2) Insulin, and 3) BMI

**Glucose P-value**

![Glucose P-value](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/images/Glucose%20Pearson%20Coefficient.png)

**Insulin P-value**

![Insulin P-value](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/images/Insulin%20Pearson%20Coefficient.png)

**BMI P-value**

![BMI P-value](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/images/BMI%20Pearson%20Coefficient.png)

<h2>4. Pre-Processing</h2>

[Pre-Processing Report](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/Sarah.Berkin--PreProcessing.Revised-Capstone%202%20Diabetes%20Project.ipynb)

* **Problem:** Out of the 768 people in the original sample, only 268 of them have diabetes. If the expressions of the dependent variable are not balanced in the dataset, it would be tough to get any model to accurately predict the outcome because the baseline would already be leaning towards a negative outcome. **Solution:** I created dummy variables in order to balance the dataset.

<h2>5. Modeling</h2>

_I used [scikit-learn](https://scikit-learn.org/stable/) for training my recommendation system. Based on the fact that my dependent variable, whether or not a person has diabetes, is a binary Yes/No, I determined that the 2 algorithms which made the most sense are 1) Logistic Regression, and 2) Support Vector Machine (SVM)._

**A.** [Modeling Report with Train Test Split](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/Sarah.Berkin--Modeling.Revised-Capstone%202%20Diabetes%20Project.ipynb)

I first ran each algorithm by performing a train test split on the data to create training and testing clusters of the data. 

* **Mean cross-validation & standard deviation when using Train Test Split**

* ![CV](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/images/CVscoresw-TTS.png)

* **Accuracy & ROC-AUC CV with Train Test Split**

* ![Modeling Report with TTS](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/images/modelresultswithTTS.png)

-------

**B.** [Modeling Report with K Fold CV](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/S.Berkin--KFold-Capstone%202%20Diabetes%20Project.ipynb)

I next ran the same 2 algorithms with K Fold cross validation to create clusters instead of train test split.

* **Mean cross-validation & standard deviation when using K Fold CV**

* ![CV](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/images/CVwithKFold.png)

* **Accuracy & ROC-AUC CV with K Fold CV**

* ![Modeling Report with K Fold Cross-Validation](https://github.com/sarahberkin/Capstone-Two-Sarah-Berkin/blob/main/images/modelresultsKFold.png)

--------

**Key Takeaways:**
* Mean cross-validation scores are slightly higher when using Train Test Split vs K Fold CV
* Accuracy is higher across the board when using Train Test Split vs K Fold CV
* ROC-AUC CV scores are just slightly higher when using Train Test Split vs K Fold CV
* If using Train Test Split, the SVM model shows slightly higher accuracy and ROC-AUC CV scores
* If using K Fold CV, the Logistic Regression model shows slightly higher accuracy and ROC-AUC CV scores

**Winning Model:**
* For the sake of erring on the more conservative side, I will choose the Logistic Regression model using K Fold CV. K Fold CV helps guard against overfitting and makes sure the entire dataset is used for training and testing while validating unseen data.

<h2>Future Improvements</h2>

* In the future, I would love to expand this data set either by gathering new data in a similar manner or by merging it with similar existing ones. I believe the results would only be strengthened by having more data points to work off of.
* I would also love to focus on the population of people who have diabetes to get more data directly from them. It could strengthen the results to have a more naturally balanced data set rather than needing to rely so heavily on dummy variables to balance the Yes / No ratio.
