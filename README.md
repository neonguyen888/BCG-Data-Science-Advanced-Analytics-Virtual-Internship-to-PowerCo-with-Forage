# Customer Churn Prediction for PowerCo · BCG Data Science Virtual Experience (Forage)

![Data Science   Advanced Analytics VEP](https://user-images.githubusercontent.com/82594129/225690586-ef6095dc-a2e4-4835-8061-6707adf54c08.png)

![Python](https://img.shields.io/badge/Python-3670A0?style=flat&logo=python&logoColor=ffdd54)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikitlearn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)

An end-to-end churn analysis for PowerCo, a European gas and electricity utility, completed as part of Boston Consulting Group's Data Science & Advanced Analytics virtual experience on Forage ([completion certificate](https://forage-uploads-prod.s3.amazonaws.com/completion-certificates/BCG/Tcz8gTtprzAS4xSoK_BCG_bySFBp5SzDx3hQ7qt_1683187050646_completion_certificate.pdf)).

**Business question:** are SME customers leaving because of price changes, and would a 20% discount for high-risk customers pay off?

## Key results

- **14,606 customers** analysed, with client data joined to 12 months of energy pricing data. **9.7% churned.**
- Price sensitivity showed only a **weak correlation with churn**. Consumption, margins and tenure mattered more.
- The baseline Random Forest reached **90.5% accuracy** but caught only **6% of churners**. Accuracy is misleading when 90% of customers stay.
- Weighting the minority class and tuning the decision threshold on training data raised **churn recall from 6% to 28%** (about 4.6x more at-risk customers caught).
- The **discount analysis** found that offering 20% off to customers with predicted churn probability ≥ 0.5 gives the largest revenue gain on the test set (about $2,930).

## What I did

| Step | Work | Deliverable |
|---|---|---|
| 1. Business understanding | Framed the price-sensitivity hypothesis as a data science problem and outlined the data and models needed to test it, written as an email to the Associate Director | [Hypothesis email (PDF)](Task%201%20-%20Business%20Understanding%20%26%20Hypothesis%20Framing/Business%20Understanding%20%26%20Hypothesis%20Framing%20-%20BCG.pdf) |
| 2. Exploratory data analysis | Cleaned and explored client and pricing data: data types, distributions, skewness and outliers, churn rate by segment, price changes over time | [EDA notebook](Task%202%20-%20Exploratory%20Data%20Analysis/Exploratory%20Data%20Analysis%20(Task%202).ipynb) · [EDA summary (PDF)](Task%202%20-%20Exploratory%20Data%20Analysis/EDA%20Summary.pdf) |
| 3. Feature engineering & modelling | Built price-difference features (e.g. December vs. January off-peak price), tenure and contract-timing features, and log transforms for skewed data. Trained and evaluated Random Forest models and estimated the impact of the discount | [Modelling notebook](Task%203%20-%20Feature%20Engineering%20%26%20Modelling/feature_engineering.ipynb) |
| 4. Findings & recommendations | Summarised the results for the Head of the SME division in a one-page executive summary | [Executive summary (PDF)](Task%204%20-%20Findings%20%26%20Recommendations/Executive%20Summary.pdf) |

## Model performance

Evaluated on a 25% hold-out test set (3,652 customers):

| Metric | Baseline Random Forest (threshold 0.5) | Balanced Random Forest (tuned threshold 0.36) |
|---|---|---|
| Accuracy | 90.5% | 85.2% |
| Precision (churn) | 0.88 | 0.27 |
| Recall (churn) | 0.06 | 0.28 |
| F1 (churn) | 0.11 | 0.28 |
| ROC AUC | 0.67 | 0.66 |

5-fold cross-validation accuracy of the baseline model: 90.8%.

**Why recall matters here:** missing a customer who is about to leave costs more than offering a discount to someone who would have stayed. So I focused on catching more churners rather than on headline accuracy. The threshold was chosen from out-of-fold predictions on the training set, and the test set was used only once at the end.

**Top churn drivers** (Random Forest feature importance): 12-month electricity consumption, net and gross margins on power subscriptions, forecasted meter rent, and how long the customer has been active.

**Limitations and next steps:** price features alone are a weak signal. Better predictions would need data such as competitor prices, customer service interactions and complaints, and a clearer definition of zero-price records.

## Repository structure

```
├── Task 1 - Business Understanding & Hypothesis Framing/   # hypothesis email (PDF + DOCX)
├── Task 2 - Exploratory Data Analysis/                      # EDA notebook, raw data, EDA summary
├── Task 3 - Feature Engineering & Modelling/                # features, models, discount analysis
└── Task 4 - Findings & Recommendations/                     # executive summary
```

## How to run

1. Install the libraries: `pip install pandas numpy matplotlib seaborn scikit-learn`
2. Run `Task 2 - Exploratory Data Analysis/Exploratory Data Analysis (Task 2).ipynb`. It reads the raw data from `Dataset/` and saves `clean_eda_data.csv`.
3. Run `Task 3 - Feature Engineering & Modelling/feature_engineering.ipynb` to build features, train the models and run the discount analysis.

Tested with Python 3.13, pandas 3.0 and scikit-learn 1.9. Both notebooks are saved with their outputs, so all charts can be viewed directly on GitHub.

---

*The PowerCo scenario and datasets were provided by BCG and Forage for educational purposes.*
