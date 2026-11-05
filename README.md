# BCG Data Science Advanced Analytics Virtual Internship to PowerCo with Forage

   ![Data Science   Advanced Analytics VEP](https://user-images.githubusercontent.com/82594129/225690586-ef6095dc-a2e4-4835-8061-6707adf54c08.png)

Completed with a certificate of completion from BCG and Forage.
---
## Task 1 
### Business Understanding & Hypothesis Framing

**Problem:**

PowerCo is a major gas and electricity utility that supplies to corporate, SME (Small & Medium Enterprise), and residential customers. The power-liberalization of the energy market in Europe has led to significant customer churn, especially in the SME segment. They have partnered with BCG to help diagnose the source of churning SME customers.

A fair hypothesis is that price changes affect customer churn. Therefore, it is helpful to know which customers are more (or less) likely to churn at their current price, for which a good predictive model could be useful.

Moreover, for those customers that are at risk of churning, a discount might incentivize them to stay with our client. The head of the SME division is considering a 20% discount that is considered large enough to dissuade almost anyone from churning (especially those for whom price is the primary concern).

The Associate Director (AD) held an initial team meeting to discuss various hypotheses, including churn due to price sensitivity. After discussion with your team, you have been asked to go deeper on the hypothesis that the churn is driven by the customers’ price sensitivities. 

Your AD wants an email with your thoughts on how the team should go about testing this hypothesis.

The client plans to use the predictive model on the 1st working day of every month to indicate to which customers the 20% discount should be offered.

**Task:**
 
Formulate the hypothesis as a data science problem and lay out the major steps needed to test this hypothesis. Communicate your thoughts and findings in an email to your AD, focusing on the data that you would need from the client and the analytical models you would use to test such a hypothesis.


---
## Task 2
### Exploratory Data Analysis

The BCG project team thinks that building a churn model to understand whether price sensitivity is the largest driver of churn has potential. The client has sent over some data and the AD wants you to perform some exploratory data analysis.

The data that was sent over includes:

* Historical customer data: Customer data such as usage, sign up date, forecasted usage etc
* Historical pricing data: variable and fixed pricing data etc
* Churn indicator: whether each customer has churned or not

**Sub-Task 1:**

Perform some exploratory data analysis. Look into the data types, data statistics, specific parameters, and variable distributions. This first subtask is for you to gain a holistic understanding of the dataset. 

**Sub-Task 2:**

Verify the hypothesis of price sensitivity being to some extent correlated with churn. It is up to you to define price sensitivity and calculate it.

**Sub-Task 3:**

Prepare a half-page summary or slide of key findings and add some suggestions for data augmentation – which other sources of data should the client provide you with and which open source datasets might be useful


---
## Task 3
### Feature Engineering & Modelling

The team now has a good understanding of the data and feels confident to use the data to further understand the business problem. The team now needs to brainstorm and build out features to uncover signals in the data that could inform the churn model.

Feature engineering is one of the keys to unlocking predictive insight through mathematical modeling. Based on the data that is available and was cleaned, identify what you think could be drivers of churn for our client and build those features to later use in your model.

First focus on building on top of the feature that your colleague has already investigated: “the difference between off-peak prices in December and January the preceding year”. After this, if you have time, feel free to get creative with making any other features that you feel are worthwhile.

Once you have a set of features, you must train a Random Forest classifier to predict customer churn and evaluate the performance of the model with suitable evaluation metrics. Be rigorous with your approach and give full justification for any decisions made by yourself as the intern data scientist. 

Recall that the hypotheses under consideration is that churn is driven by the customers’ price sensitivities and that it would be possible to predict customers likely to churn using a predictive model.

If you’re eager to go the extra mile for the client, when you have a trained predictive model, remember to investigate the client’s proposed discounting strategy, with the head of the SME division suggesting that offering customers at high propensity to churn a 20% discount might be effective.

Build your models and test them while keeping in mind you would need data to prove/disprove the hypotheses, as well as to test the effect of a 20% discount on customers at high propensity to churn.

**Sub-Task 1:**

This feature is “the difference between off-peak prices in December and January the preceding year”. 

**Sub-Task 2:**

Train a Random Forest classifier and to evaluate the results in an appropriate manner. We would also like you to document the advantages and disadvantages of using a Random Forest for this use case. 

Ensure you’re able to explain the performance of your model, where did the model underperform?
Why did you choose the evaluation metrics that you used? Please elaborate on your choices.
Document the advantages and disadvantages of using the Random Forest for this use case.
Do you think that the model performance is satisfactory? Give justification for your answer.


---
## Task 4
### Findings & Recommendations

Develop an abstract slide synthesizing all the findings from the project so far, keeping in mind that this will be for the key stakeholders meeting which the Head of the SME division, as well as other various stakeholders, will be attending which including:

* What is the most important number or metric to share with the client?
* What impact would the model have on the client’s bottom line?


---
## Results (Task 3 model)

Evaluated on a 25% hold-out test set (3,652 customers, about 10% churn):

| Metric | Baseline Random Forest (threshold 0.5) | Balanced Random Forest (tuned threshold 0.36) |
|---|---|---|
| Accuracy | 90.5% | 85.2% |
| Precision (churn) | 0.88 | 0.27 |
| Recall (churn) | 0.06 | 0.28 |
| F1 (churn) | 0.11 | 0.28 |
| ROC AUC | 0.67 | 0.66 |

5-fold cross-validation accuracy of the baseline model: 90.8%.

**What this means:** because only about 10% of customers churn, the baseline looks accurate but catches only 6% of churners. Weighting the minority class and choosing the threshold from training data (out-of-fold predictions, never the test set) raises recall to 28%, about 4.6x more churners caught, at the cost of more false alarms. Price features alone are a weak predictor of churn, so the next step would be adding non-price data such as customer service history.

**Discount analysis:** offering the 20% discount to customers with a predicted churn probability of 0.5 or above gives the largest revenue gain on the test set (about $2,930).

## How to run

1. Install: `pip install pandas numpy matplotlib seaborn scikit-learn`
2. Run `Task 2 - Exploratory Data Analysis/Exploratory Data Analysis (Task 2).ipynb`. It reads the raw data from `Dataset/` and saves `clean_eda_data.csv`.
3. Run `Task 3 - Feature Engineering & Modelling/feature_engineering.ipynb` to build features, train the model, and run the discount analysis.

Tested with Python 3.13, pandas 3.0, and scikit-learn 1.9.
