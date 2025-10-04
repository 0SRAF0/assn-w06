# Customer Churn Prediction Analysis Report

## Introduction

This project tackles customer churn prediction for a telecom company. The goal is to figure out which customers are about to leave so the company can do something about it before they're gone. I used a Random Forest classifier on the Telco Customer Churn dataset with 7,043 customers and built a RandomForest model that predicts churn with decent accuracy.


## Methodology

### Data Preprocessing

The dataset had 21 features including demographics, services, contract info, and billing data. The baseline churn rate was 26.5%, so roughly 1 in 4 customers left.

First issue I hit was TotalCharges being stored as text instead of numbers, which caused 11 missing values. I converted it to numeric and filled the gaps with the median. I also dropped customerID since it's just an identifier and doesn't help predict anything.

For the categorical variables (gender, Contract type, PaymentMethod, etc.), I used one-hot encoding to convert them to binary columns. This turned 15 text columns into numeric features, expanding from 20 to 30 total features. I used `drop_first=True` to avoid redundancy.

### Model Training

I went with Random Forest because it handles mixed data types well and gives you feature importance for free. The model has 100 trees with max depth of 15. I split the data 80/20 for train/test (5,634 training samples, 1,409 test samples) and used stratification to keep the same churn rate in both sets.

Each tree in the forest trains on a random subset of customers and features, then they all vote on the final prediction. If 60+ trees say a customer will churn, the model predicts churn.

---

## Results

### Performance Metrics

The model hit 79.28% accuracy with an AUC of 0.831. Breaking down the metrics:

- **Accuracy: 79.28%** - Got about 4 out of 5 predictions right
- **Precision: 63.23%** - When it says someone will churn, it's right 63% of the time
- **Recall: 52.41%** - Only catches about half of the people who actually churn
- **F1-Score: 57.31%** - Balanced metric between precision and recall
- **AUC: 0.831** - Strong ability to separate churners from non-churners

### Confusion Matrix Breakdown

| | Predicted No Churn | Predicted Churn |
|---|---|---|
| **Actual No Churn** | 921 | 114 |
| **Actual Churn** | 178 | 196 |

The 178 false negatives are the real problem here. Those are customers the model said would stay but actually left. That's missed revenue and missed chances to retain them. The 114 false positives are less critical - yeah, we'd waste some retention budget on people who weren't going to leave anyway, but that's cheaper than losing a customer entirely.

The recall being only 52% means we're missing almost half the churners. Depending on how much retention costs versus customer lifetime value, it might make sense to lower the prediction threshold to catch more at-risk customers, even if it means more false alarms.

---

## Feature Importance

The top predictors are mostly financial:

1. **TotalCharges (18.5%)** - How much they've spent over their lifetime
2. **tenure (17.6%)** - How long they've been a customer
3. **MonthlyCharges (15.9%)** - Current monthly bill
4. **InternetService_Fiber optic (4.3%)** - Having fiber internet
5. **PaymentMethod_Electronic check (4.1%)** - Paying via electronic check

These three financial features alone account for over 50% of what the model uses to make decisions. The tenure result makes sense - new customers are riskier. What's interesting is that fiber optic internet and electronic check payments both correlate with higher churn. Either there's a service quality issue with fiber, or the payment method creates friction that annoys people.

Contract type also matters (two-year contracts reduce churn), but demographics like gender and senior citizen status barely register.

---

## Business Recommendations

### Short-term Actions

**Focus on new customers.** The first year is critical. Tenure is the second most important feature, so implementing better onboarding for customers in their first 6-12 months could help. Regular check-ins, exclusive new customer perks, or dedicated account managers might work.

**Look into fiber optic service.** If fiber customers are churning more, something's wrong. Either the service quality isn't matching the price, competitors have better fiber offerings, or the value proposition isn't clear. This needs investigation.

**Fix the electronic check experience.** People using electronic checks churn more. Maybe the process is tedious.Incentivizing automatic payment methods could help.

**Price sensitivity for high spenders.** Customers with both high monthly charges and high total charges are at risk. These are valuable customers who might be shopping around.

### Future Improvements

The model works but could be better. Some ideas:

- Retrain quarterly with fresh data to avoid drift
- Try different hyperparameters (max_depth, number of trees)
- Get feedback from the retention team on whether the predictions are actionable

---

## Conclusion

The Random Forest model predicts churn reasonably well (79% accuracy, 0.831 AUC) and identifies the key risk factors: new customers with high charges are the biggest flight risk. The main weakness is the 52% recall, we're missing half the churners. By targeting new customers, investigating fiber service issues, and addressing payment friction, the company should be able to reduce churn. The model provides a solid foundation for a retention strategy, but catching more at-risk customers (even with more false alarms) would probably be worth it from a revenue perspective.