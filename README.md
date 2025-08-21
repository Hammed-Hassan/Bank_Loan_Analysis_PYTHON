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
#
### ✅Analysis and Visualization
Monthly Trends by Issue Date (Line/Area Chart)
```python code
monthly_funded = (
    df.sort_values('issue_date')
      .assign(month_name=lambda x: x['issue_date'].dt.strftime('%b %Y'))
      .groupby ('month_name', sort=False)['loan_amount']
      .sum()
      .div(1000000)
      .reset_index(name='loan_amount_millions')
)
    
plt.figure(figsize=(10, 5))
plt.fill_between(monthly_funded['month_name'], monthly_funded['loan_amount_millions'], color='skyblue', alpha=0.5) 
plt.plot(monthly_funded['month_name'], monthly_funded['loan_amount_millions'], color='blue', linewidth=2)
    
for i, row in monthly_funded.iterrows():
    plt.text(i, row['loan_amount_millions'] + 0.1, f"{row[ 'loan_amount_millions']:.2f})",
              ha='center', va='bottom', fontsize=9, rotation=0, color='black')
    
plt.title('Total Funded Amount by Month', fontsize=14)
plt.xlabel('Month')
plt.ylabel('Funded Amount ($ Millions)')
plt.xticks(ticks=range(len(monthly_funded)), labels=monthly_funded['month_name'], rotation=90)
plt.grid(True, linestyle='--', alpha=0.6)
plt.tight_layout()
plt.show()
```
![Alt text for the image](https://github.com/Hammed-Hassan/Bank_Loan_Analysis/blob/main/Monthly%20Trends%20by%20Issue%20Date.png)

Regional Analysis by State (Bar Chart)
```python code
state_funding = df.groupby('address_state')['loan_amount'].sum().sort_values(ascending=True)
state_funding_thousands = state_funding / 1000

plt.figure(figsize=(10, 8))
bars = plt.barh(state_funding_thousands.index, state_funding_thousands.values, color='lightcoral')

for bar in bars:
    width = bar.get_width()
    plt.text(width + 10, bar.get_y() + bar.get_height() / 2, f'{width:,.0f}K', va='center', fontsize=9)
    
plt.title('Total Funded Amount by State (in # Thousands)') 
plt.xlabel('Funded Amount (# \'000)')
plt.ylabel('State')
plt.tight_layout()
plt.show()
```
![Alt text for the image](https://github.com/Hammed-Hassan/Bank_Loan_Analysis/blob/main/Total%20Funded%20Amount%20by%20State.png)

Loan Term Analysis (Donut Chart)
```python code
term_funding_millions = df.groupby('term')['loan_amount'].sum() / 1000000


plt.figure(figsize=(5, 5))
plt.pie(
    term_funding_millions,
    labels=term_funding_millions.index,
    autopct=lambda p:f"{p:.1f}%\n${p*sum(term_funding_millions)/100:.1f}M",
    startangle=90,
    wedgeprops={'width': 0.4}
)

plt.gca().add_artist(plt.Circle((0, 0), 0.70, color='white'))
plt.title("Total Funded Amount by Term (in $ Millions)")
plt.show()
```
![Alt text for the image](https://github.com/Hammed-Hassan/Bank_Loan_Analysis/blob/main/Total%20Funded%20Amount%20by%20Term.png)

Employee Length Analysis (Bar Chart)
```python code
emp_funding = df.groupby('emp_length')['loan_amount'].sum().sort_values(ascending=True)
emp_funding_thousands = emp_funding / 1000

plt.figure(figsize=(10, 6))
bars = plt.barh(emp_funding_thousands.index, emp_funding_thousands.values, color='lightcoral')

for bar in bars:
    width = bar.get_width()
    plt.text(width + 5, bar.get_y() + bar.get_height() / 2, f'{width:,.0f}K', va='center', fontsize=9)
    
plt.title('Funded Amount (# Thousands)') 
plt.xlabel('Total Funded Amount by Employment Length')
plt.grid(axis = 'x', linestyle = '--', alpha = 0.5)
plt.tight_layout()
plt.show()
```
![Alt text for the image](https://github.com/Hammed-Hassan/Bank_Loan_Analysis/blob/main/Employee%20length%20by%20Total%20Funded%20Amount.png)

Loan Purpose Breakdown (Bar Chart)
```python code
purpose_funding = df.groupby('purpose')['loan_amount'].sum().sort_values(ascending=True)
purpose_funding_millions = purpose_funding / 1000000

plt.figure(figsize=(10, 6))
bars = plt.barh(purpose_funding_millions.index, purpose_funding_millions.values, color='lightcoral')

for bar in bars:
    width = bar.get_width()
    plt.text(width + 5, bar.get_y() + bar.get_height() / 2, f'{width:,.0f}M', va='center', fontsize=9)
    
plt.title('Total Funded Amount by Loan Purpose (# Millions)') 
plt.xlabel('Funded Amount (# Million)')
plt.ylabel('Loan Purpose')
plt.grid(axis = 'x', linestyle = '--', alpha = 0.5)
plt.tight_layout()
plt.show()
```
![Alt text for the image](https://github.com/Hammed-Hassan/Bank_Loan_Analysis/blob/main/Loan%20Purpose%20by%20Total%20Funded%20Amount.png)

Home Ownership Analysis (Tree Map)
```python code
home_funding = df.groupby('home_ownership')['loan_amount'].sum().reset_index()
home_funding['loan_amount_millions'] = home_funding['loan_amount'] / 1000000


fig = px.treemap(
    home_funding,
    path=['home_ownership'],
    values='loan_amount_millions',
    color='loan_amount_millions',
    color_continuous_scale='Blues',
    title='Total Funded Amount by Home Ownership (# Millions)'
)

fig.show()
```
![Alt text for the image](https://github.com/Hammed-Hassan/Bank_Loan_Analysis/blob/main/Home%20ownership%20by%20Total%20Funded%20Amount.png)
