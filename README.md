# Bank Customer Churn Prediction

Predicting which credit card customers will close their accounts, so a bank can reach out before they leave.

**Tools:** R · tidyverse · caret · leaps · randomForest · e1071 · class · gbm · pROC

## The question
Can we tell from a customer's account activity whether they are likely to leave (attrite) or stay?

## Data
- `customer_data.csv`: 10,127 bank customers, with 20 columns on demographics (age, gender, education, income), relationship with the bank (months on book, number of products, contacts) and card activity (credit limit, revolving balance, transaction amounts and counts).
- About 16% of the customers left (1,627 attrited vs. 8,500 existing), so the classes are imbalanced.
- `Data_Dictionary.pdf` explains every column.

## Approach
1. **Cleaning and exploration:** checked for missing values, looked at a correlation heat map, and removed `Avg_Open_To_Buy` because it overlaps heavily with the other credit variables.
2. **Feature selection:** used best-subset selection (lowest BIC), checked multicollinearity with VIF, and compared the result with random forest feature importance.
3. **Models:** trained on a 50/50 train/test split and compared:
   - Logistic regression (three predictor sets)
   - Naive Bayes
   - k-nearest neighbors (k = 10, scaled data)
   - Random forest
   - Gradient boosting
4. **Evaluation:** confusion matrices, accuracy, sensitivity, specificity, ROC curves and AUC.

## Results
- The strongest predictors of leaving were **total transaction amount**, **change in transaction count (Q4 vs. Q1)**, **revolving balance**, **change in transaction amount** and **number of bank products held**. Customers who use their card less are more likely to leave.
- Naive Bayes reached about **88.6% test accuracy**, and k-nearest neighbors reached about **89.9%**, both above the 84% you'd get by always predicting "stays."
- The models were very good at recognizing customers who stay, with 95–97% sensitivity. They caught fewer of the customers who left, about 40–50%. That's the part to improve, for example with class weights or a different decision threshold.

## Files
| File | What it is |
|---|---|
| `Project 3rd trial best subset.Rmd` | Full analysis in R Markdown |
| `customer_data.csv` | Dataset |
| `Data_Dictionary.pdf` | Column descriptions |

## How to run
Open `Project 3rd trial best subset.Rmd` in RStudio. Change the `read.csv(...)` path near the top so it points to `customer_data.csv`, then click **Knit** or run the chunks in order.

---
*Created by Ertugrul Turkseven for DSE6111 Predictive Modeling, M.S. in Data Science, Merrimack College.*
