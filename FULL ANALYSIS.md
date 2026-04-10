
# Exploratory Data Analysis - FULL
# Introduction
LendingClub is a peer-to-peer loan platform that connects borrowers and investors, enabling individuals to obtain loans outside traditional banking channels.
# Data used
The data represents both accepted loans and rejected loans.

To reduce the influence of outliers and ensure reliable results, values for each dimension value are included in the analysis only when at least 30 observations are available for that specific dimension value.

For this project, it is essential to understand what each variable represents and when the information was recorded. In credit risk modelling, the timing of data collection is particularly important because only variables known at the time of the loan application can be used to predict default risk. Variables recorded after loan issuance may contain information about the future performance of the loan and can introduce data leakage, leading to overly optimistic model results. Therefore, distinguishing between borrower characteristics available before or at origination and variables generated during the life of the loan is a critical step to ensure a realistic and reliable analysis of default probability.
| data_type   | variable                      | description                  | timing          | pd_model_usage |
|-------------|-------------------------------|------------------------------|-----------------|----------------|
| numeric     | loan_amnt                     | Requested loan amount        | pre_application | safe           |
| numeric     | funded_amnt                   | Funded amount                | origination     | safe           |
| numeric     | funded_amnt_inv               | Funded by investors          | origination     | safe           |
| numeric     | term                          | Loan duration months         | origination     | safe           |
| numeric     | int_rate                      | Interest rate                | origination     | caution        |
| numeric     | installment                   | Monthly payment              | origination     | safe           |
| categorical | grade                         | LC credit grade              | origination     | caution        |
| categorical | sub_grade                     | LC subgrade                  | origination     | caution        |
| numeric     | annual_inc                    | Annual income                | pre_application | safe           |
| numeric     | annual_inc_joint              | Joint income                 | pre_application | safe           |
| categorical | emp_length                    | Employment length            | pre_application | safe           |
| categorical | emp_title                     | Employment title             | pre_application | safe           |
| categorical | home_ownership                | Housing status               | pre_application | safe           |
| categorical | verification_status           | Income verification          | origination     | safe           |
| categorical | verification_status_joint     | Joint verification           | origination     | safe           |
| categorical | purpose                       | Loan purpose                 | pre_application | safe           |
| categorical | title                         | Loan title                   | pre_application | safe           |
| numeric     | fico_range_low                | FICO lower                   | pre_application | safe           |
| numeric     | fico_range_high               | FICO upper                   | pre_application | safe           |
| numeric     | last_fico_range_low           | Last FICO lower              | post_loan       | avoid          |
| numeric     | last_fico_range_high          | Last FICO upper              | post_loan       | avoid          |
| numeric     | dti                           | Debt to income ratio         | pre_application | safe           |
| numeric     | dti_joint                     | Joint DTI                    | pre_application | safe           |
| numeric     | open_acc                      | Open credit lines            | pre_application | safe           |
| numeric     | total_acc                     | Total accounts               | pre_application | safe           |
| numeric     | revol_bal                     | Revolving balance            | pre_application | safe           |
| numeric     | revol_util                    | Revolving utilization        | pre_application | safe           |
| numeric     | delinq_2yrs                   | Delinquencies 2 years        | pre_application | safe           |
| numeric     | inq_last_6mths                | Inquiries 6 months           | pre_application | safe           |
| numeric     | open_acc_6m                   | Accounts opened 6 months     | pre_application | safe           |
| numeric     | open_acc_12m                  | Accounts opened 12 months    | pre_application | safe           |
| numeric     | open_acc_24m                  | Accounts opened 24 months    | pre_application | safe           |
| numeric     | acc_open_past_24mths          | Accounts opened 24 months    | pre_application | safe           |
| numeric     | num_rev_accts_opened_last_12m | Revolving opened 12m         | pre_application | safe           |
| numeric     | num_il_tl_12m                 | Installment opened 12m       | pre_application | safe           |
| numeric     | mths_since_recent_inq         | Months since inquiry         | pre_application | safe           |
| numeric     | tot_cur_bal                   | Total current balance        | pre_application | safe           |
| numeric     | tot_coll_amt                  | Total collections            | pre_application | safe           |
| numeric     | total_bal_ex_mort             | Balance excl mortgage        | pre_application | safe           |
| numeric     | total_bc_limit                | Credit card limit            | pre_application | safe           |
| numeric     | bc_util                       | Credit card utilization      | pre_application | safe           |
| numeric     | bc_open_to_buy                | Unused card limit            | pre_application | safe           |
| numeric     | percent_bc_gt_75              | Cards >75% utilization       | pre_application | safe           |
| numeric     | total_rev_hi_lim              | Revolving credit limit       | pre_application | safe           |
| numeric     | avg_cur_bal                   | Average balance              | pre_application | safe           |
| numeric     | num_bc_tl                     | Number bankcard accounts     | pre_application | safe           |
| numeric     | num_actv_bc_tl                | Active bankcard accounts     | pre_application | safe           |
| numeric     | num_actv_rev_tl               | Active revolving accounts    | pre_application | safe           |
| numeric     | num_op_rev_tl                 | Open revolving accounts      | pre_application | safe           |
| numeric     | num_rev_tl_bal_gt_0           | Revolving balance >0         | pre_application | safe           |
| numeric     | num_sats                      | Number satisfactory accounts | pre_application | safe           |
| numeric     | num_tl_30dpd                  | Accounts 30dpd               | pre_application | safe           |
| numeric     | num_tl_90g_dpd_24m            | 90dpd last 24m               | pre_application | safe           |
| numeric     | num_tl_op_past_12m            | Accounts opened 12m          | pre_application | safe           |
| numeric     | num_tl_closed_24m             | Closed accounts 24m          | pre_application | safe           |
| numeric     | num_il_tl                     | Installment accounts         | pre_application | safe           |
| numeric     | il_util                       | Installment utilization      | pre_application | safe           |
| numeric     | total_il_high_credit_limit    | Installment credit limit     | pre_application | safe           |
| numeric     | max_bal_bc                    | Max balance credit card      | pre_application | safe           |
| numeric     | all_util                      | Balance to credit ratio      | pre_application | safe           |
| numeric     | inq_fi                        | Finance inquiries            | pre_application | safe           |
| numeric     | inq_last_12m                  | Inquiries 12m                | pre_application | safe           |
| numeric     | total_cu_tl                   | Total credit lines           | pre_application | safe           |
| numeric     | num_accts_ever_120_pd         | Accounts 120dpd ever         | pre_application | safe           |
| numeric     | chargeoff_within_12_mths      | Chargeoffs 12m               | pre_application | safe           |
| numeric     | collections_12_mths_ex_med    | Collections 12m              | pre_application | safe           |
| numeric     | tax_liens                     | Tax liens                    | pre_application | safe           |
| numeric     | pub_rec                       | Public records               | pre_application | safe           |
| numeric     | pub_rec_bankruptcies          | Bankruptcies                 | pre_application | safe           |
| date        | issue_d                       | Issue date                   | origination     | safe           |
| date        | earliest_cr_line              | First credit line            | pre_application | safe           |
| date        | last_credit_pull_d            | Last credit pull             | post_loan       | avoid          |
| date        | last_pymnt_d                  | Last payment date            | post_loan       | avoid          |
| date        | next_pymnt_d                  | Next payment date            | post_loan       | avoid          |
| categorical | loan_status                   | Loan outcome                 | post_loan       | avoid          |
| numeric     | total_pymnt                   | Total payment                | post_loan       | avoid          |
| numeric     | total_pymnt_inv               | Total payment investors      | post_loan       | avoid          |
| numeric     | total_rec_prncp               | Principal received           | post_loan       | avoid          |
| numeric     | total_rec_int                 | Interest received            | post_loan       | avoid          |
| numeric     | recoveries                    | Recoveries after default     | post_loan       | avoid          |
| numeric     | collection_recovery_fee       | Recovery fee                 | post_loan       | avoid          |
| numeric     | last_pymnt_amnt               | Last payment amount          | post_loan       | avoid          |
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