# Bank Loan Analysis with Python

![Alt text for the image](https://github.com/Hammed-Hassan/Bank_Loan_Analysis/blob/main/Bank%20Loan%20Pictures.jpg)

## ✅Project Overview
This project provides a comprehensive analysis of a loan portfolio to identify key performance indicators (KPIs) and uncover insights into lending trends, borrower demographics, and loan health. The analysis is driven by a data-first approach, utilizing Python and its robust data science libraries to deliver actionable business intelligence. The entire analysis, from data wrangling to visualization, was performed in a Jupyter Notebook, which is included in this repository.

#
### ✅Problem Statement & Key Performance Indicators (KPIs)
- Total Loan Applications: Calculation of total applications and Month-to-Date (MTD) figures.
- Total Funded Amount: Calculation of total funds disbursed and MTD figures.
- Total Amount Received: Tracking of total repayments from borrowers and MTD figures.
- Average Interest Rate: Computation of the average interest rate across all loans to assess the overall cost of the lending portfolio.
- Average Debt-to-Income Ratio (DTI): Evaluation of the average DTI to gauge the financial health of borrowers.

#
### ✅Data Sourcing 

#
### ✅Data Tranformation & Manipulation

#
### ✅Solving with Python: The Code
1. Total Loan Applications
```python code
total_loan_application = df['id'].count()
print("Total Loan Applications:", total_loan_application)
```
2. Total Funded Amount
```python code
total_funded_amount = df['loan_amount'].sum()
total_funded_amount_millions = total_funded_amount/1000000 
print(f"Total Funded Amount: ${total_funded_amount_millions:.2f}M")
```
3. Total Amount Received
```python code
total_loan_application = df['id'].count()
print("Total Loan Applications:", total_loan_application)
```
MTD Total Loan Applications
```python code
latest_issue_date = df['issue_date'].max()
latest_year = latest_issue_date.year
latest_month = latest_issue_date.month

mtd_data = df[(df['issue_date'].dt.year == latest_year) & (df['issue_date'].dt.month == latest_month)]

mtd_loan_appliactions = mtd_data['id'].count()

print(f"MTD Loan Applications(for {latest_issue_date.strftime('%B %Y')}): {mtd_loan_appliactions}")
```
MTD Total Funded Amount
```python code
latest_issue_date = df['issue_date'].max()
latest_year = latest_issue_date.year
latest_month = latest_issue_date.month

mtd_data = df[(df['issue_date'].dt.year == latest_year) & (df['issue_date'].dt.month == latest_month)]

mtd_total_funded_amount = mtd_data['loan_amount'].sum()
total_funded_amount_millions = mtd_total_funded_amount/1000000 
print(f"MTD Total Funded Amount: ${total_funded_amount_millions:.2f}M")
```
MTD Total Amount Received
```python code
latest_issue_date = df['issue_date'].max()
latest_year = latest_issue_date.year
latest_month = latest_issue_date.month

mtd_data = df[(df['issue_date'].dt.year == latest_year) & (df['issue_date'].dt.month == latest_month)]

mtd_total_amount_recieved = mtd_data['total_payment'].sum()
mtd_total_amount_recieved_millions = mtd_total_amount_recieved/1000000 
print(f"Total Funded Amount: ${mtd_total_amount_recieved_millions:.2f}M")
```
4. Average Interest Rate
```python code
average_interest_rate = df['int_rate'].mean()*100
print(f"Avg Int Rate: {average_interest_rate:.2f}")
```
5. Average debt-to-Income Ration (DTI)
```python code
average_dti = df['dti'].mean()*100
print(f"Avg DTI: {average_dti:.2f}%")
```

#
### ✅Good and Bad Loan Metrics
Good Loan metrics
```python code
good_loan = df[df['loan_status'].isin(['Fully Paid', 'Current'])]
total_loan_applications = df['id'].count()

good_loan_applications = good_loan['id'].count()
good_loan_funded_amount = good_loan['loan_amount'].sum()
good_loan_received = good_loan['total_payment'].sum()

good_loan_funded_amount_millions = good_loan_funded_amount / 1000000
good_loan_received_millions = good_loan_received / 1000000

good_loan_percentage = (good_loan_applications / total_loan_applications) * 100

print(f"Good Loan Applications:{good_loan_applications}")
print(f"Good Loan Funded Amount(in Millions):${good_loan_funded_amount_millions:.2f}M")
print(f"Good Loan Total Received (in Millions):${good_loan_received_millions:.2f}M")
print(f"Percentage of Good Loan Applications:{good_loan_percentage:.2f}%")
```

Bad Loan Metrics
```python code
bad_loan = df[df['loan_status'].isin(['Charged Off'])]
total_loan_applications = df['id'].count()

bad_loan_applications = bad_loan['id'].count()
bad_loan_funded_amount = bad_loan['loan_amount'].sum()
bad_loan_received = bad_loan['total_payment'].sum()

bad_loan_funded_amount_millions = bad_loan_funded_amount / 1000000
bad_loan_received_millions = bad_loan_received / 1000000

bad_loan_percentage = (bad_loan_applications / total_loan_applications) * 100

print(f"bad Loan Applications:{bad_loan_applications}")
print(f"bad Loan Funded Amount(in Millions):${bad_loan_funded_amount_millions:.2f}M")
print(f"bad Loan Total Received (in Millions):${bad_loan_received_millions:.2f}M")
print(f"Percentage of bad Loan Applications:{bad_loan_percentage:.2f}%")

```
