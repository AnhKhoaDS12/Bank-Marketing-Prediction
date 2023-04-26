
# Bank Marketing Prediction




## Relevant Information
+ This dataset is based on "Bank Marketing" UCI dataset (please check the description at: http://archive.ics.uci.edu/ml/datasets/Bank+Marketing).
+ The data is enriched by the addition of five new social and economic features/attributes (national wide indicators from a ~10M population country), published by the Banco de Portugal and publicly available at: https://www.bportugal.pt/estatisticasweb.
+ This dataset is almost identical to the one used in [Moro et al., 2014] (it does not include all attributes due to privacy concerns). 
## Bank client data:
1. age (numeric)
2. job: 12 type of job (categorical: admin., blue-collar,entrepreneur, housemaid, management, retired, self-.employed, services, student, technician, unemployed, unknown).
3. marital: marital status (4 categorical: divorced (divorced means divorced or widowed),married,single,unknown).
4. education (8 categorical: basic.4y, basic.6y, basic.9y, high.school, illiterate, professional.course, university.degree, unknown).
5. default: has credit in default? (3 categorical: no,yes,unknown).
6. housing: has housing loan? (categorical: no,yes,unknown).
7. loan: has personal loan? (categorical: no,yes,unknown).
## Related with the last contact of the current campaign:
8. contact: contact communication type (categorical: cellular, telephone).
9. month: last contact month of year (categorical: jan, feb, mar, ..., nov, dec).
10. day_of_week: last contact day of the week (categorical: mon,tue,wed,thu,fri).
11. duration: last contact duration, in seconds (numeric).
## Other attributes:
12. campaign: number of contacts performed during this campaign and for this client (numeric, includes last contact).
13. pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted).
14. previous: number of contacts performed before this campaign and for this client (numeric).
15. poutcome: outcome of the previous marketing campaign (categorical: failure,nonexistent,success).
## Social and economic context attributes
16. emp.var.rate: employment variation rate - quarterly indicator (numeric).
17. cons.price.idx: consumer price index - monthly indicator (numeric).     
18. cons.conf.idx: consumer confidence index - monthly indicator (numeric). 
19. euribor3m: euribor 3 month rate - daily indicator (numeric).
20. nr.employed: number of employees - quarterly indicator (numeric).
## Output variable (desired target):
21. y - has the client subscribed a term deposit? (binary: yes,no).
+ Missing Attribute Values: There are several missing values in some categorical attributes, all coded with the "unknown" label.
## Model Building Process
1. Input dataset
2. Train (60%) - valid (20%) - test(20%)
3. Drop high correlation in train set.
4. Exploratory Data Analysis (EDA)
+ Target Feature: has the client subscribed a term deposit? (binary: yes,no).
+ Description: which customers will subscribed a term deposit in the this campaign.
+ Drop 'default' columns.
+ 7 numerical features : 3 discrete features , 4 continuous features.
+ 9 categorical features.
+ No missing values
+ No missing values but there are several missing values in some categorical attributes, all coded with the "unknown" label
+ There are 11% target values with 1 (imbalanced train dataset)
+ Normal distribution: cons.conf.idx.
+ Skewness distribution: age,duration,campaign.
+ Visualization
---
+ Retired people or older domestic workers are more likely to participate in term deposits
+ The older married or divorced people are, the more likely they are to join a term deposit
+ Those who have basic education for 4 years, the older they are, the more they will participate in term deposits
+ If the last contact time (in seconds) is more than 300 then that person will definitely join a term deposit
+ The higher the number of contacts made before this campaign, the more likely that customer in this campaign is to join a term deposit.
---
+ Older singles are less likely to participate in term deposits
+ Illiterate older people are less likely to participate in term deposits than younger illiterate people
+ People with credit debt will not participate in term deposits
+ The higher the number of contacts made during this campaign, the less likely it is to join a term deposit.

5. Feature Engineering
+ Replace missing value (unknown values): job (unknown = house maid), education (unknown = university.degree), marital (unknown = single), housing & loan (random sample)
+ Encoding: normal cardinality (>5): 3 (job,education,month),low cardinality (1-5): 6(marital,housing,loan,contact,day_of_week,poutcome). Nomial (job,month,marital,housing,loan,contact,day_of_week,poutcome), ordinal (education).
+ Handling imbalanced dataset: use SMOTETomek (ratio = 1).

6. Model Building
+ We use 7 algorithms (Naive Bayes, decision tree, random forests, K-NN, gradient boosting, XGBoost, LightGBM) for training and predict valid & test set.
+ We choose LightGBM for hyperparameter training.

+ In all cases of participating in term deposits, the model correctly predicted 55% of cases of time deposit transactions (valid set).
+ In all cases actually participating in term deposits the correct prediction model is 61% (valid set).
+ Accuracy: 91%, f1-score: 58% (valid set).


7. Evaluation (test set)
+ In all cases of participating in term deposits, the model correctly predicted 53% of cases of time deposit transactions.
+ In all cases actually participating in term deposits the correct prediction model is 63%.
+ Accuracy: 91%, f1-score: 58%.
=> Model is not overfitting. We still need to improve the recall score of the model as well as the f1 score by other methods of data preprocessing and other algorithms.