
# Exploratory Data Analysis - FULL
# Introduction
LendingClub is a peer-to-peer loan platform that connects borrowers and investors, enabling individuals to obtain loans outside traditional banking channels.
# Data used
The data represents both accepted loans and rejected loans.

To reduce the influence of outliers and ensure reliable results, values for each dimension value are included in the analysis only when at least 30 observations are available for that specific dimension value.

For this project, it is essential to understand what each variable represents and when the information was recorded. In credit risk modelling, the timing of data collection is particularly important because only variables known at the time of the loan application can be used to predict default risk. Variables recorded after loan issuance may contain information about the future performance of the loan and can introduce data leakage, leading to overly optimistic model results. Therefore, distinguishing between borrower characteristics available before or at origination and variables generated during the life of the loan is a critical step to ensure a realistic and reliable analysis of default probability.

Detailed explanations of the variables, their type, timing of recording etc. can be found in the [data dictionary](data_dictionary.csv).
# Results
First, we observe that loans appear to be correctly priced: higher interest rates are associated with higher probabilities of default, consistent with risk-based pricing.
![alt text](Images/PD_v_IR_Grade.svg)
## Income
50% of defaults are caused by borrowers earning less than 50,000$ a year, and 90% by those earning less than 115,000$ year.

![alt text](Images/pct_default_v_income.svg)

Income influences probability of default because debt represents a larger financial burden for lower-income borrowers. However, this relationship must be interpreted in context. A borrower with low annual income and a large loan faces significantly higher repayment pressure than a borrower with low income but a small loan amount. Therefore, risk should be assessed using relative measures such as the debt-to-income ratio rather than income alone. 


![alt text](Images/PD_income.svg)

Nonetheless, the relationship between income and default risk still exists. Even when two borrowers have the same debt-to-income ratio, the borrower with the higher income often faces lower risk. This is because essential living expenses do not increase proportionally with income — spending on necessities such as housing, food, and utilities does not scale one-to-one with earnings. Higher-income individuals typically devote a smaller share of their income to essential goods and therefore retain more disposable income after covering basic costs. This additional financial flexibility allows them to better absorb unexpected expenses and maintain loan repayments. As a result, higher income provides a greater financial buffer, reducing the probability of default even when relative leverage is similar.

## FICO

It is also important to note that no loans are issued to borrowers with a FICO score below 600. Additionally, the debt-to-income (DTI) ratio does not appear to significantly influence the interest rate at which loans are priced. This finding is plausible, as higher-income individuals can typically sustain higher levels of debt, since their essential expenses do not increase proportionally with income.

![alt text](Images/avg_ir_v_FICO&income.svg)

FICO scores range from 300 to 850. In the dataset, there are two distinct FICO scores, the one at the date of loan application, and the most recent calculated FICO.

Debt-to-income ratio also affects default probability, as debt burden increases

## Summary table
| Variable | Effect on PD | Interpretation |
|-|-|-|
| FICO | high | higher score → lower risk |
| interest rate | positive | reflects risk pricing |
| DTI | positive | higher leverage increases risk |  
| Annual income | high | higher income decreases PD up to a certain threshold |
# Next step
- Check multi-collinearity