
# Automatidata Project: A/B Testing for NYC Taxi & Limousine Commission

## Project Overview
This project involves analyzing data from the New York City Taxi & Limousine Commission (NYC TLC) to understand the relationship between fare amount and payment type. The goal is to conduct an A/B test to determine if customers who use credit cards pay higher fares than those who use cash. This analysis aims to provide insights that could help generate more revenue for taxi cab drivers.

## Project Structure
The project is structured as follows:
- **data**: Contains the dataset used for the analysis.
- **notebooks**: Contains the Jupyter notebooks used for EDA and hypothesis testing.
- **results**: Contains the results of the analysis and visualizations.
- **README.md**: Project documentation.

## Dependencies
- Python 3.x
- pandas
- scipy
- matplotlib


## Data Preparation
The dataset used for this project is a CSV file containing data on taxi trips in New York City. It includes various attributes such as fare amount, payment type, trip distance, and more.

### Loading the Data
The dataset is loaded using pandas:
```python
import pandas as pd

# Load the dataset
taxi_data = pd.read_csv("data/2017_Yellow_Taxi_Trip_Data.csv", index_col=0)
```

## Exploratory Data Analysis (EDA)
Descriptive statistics are used to understand the data and explore the relationship between fare amount and payment type.


# Group by payment type and calculate mean fare amount
mean_fare_by_payment = taxi_data.groupby('payment_type')['fare_amount'].mean()
print(mean_fare_by_payment)
```

### Payment Type Encoding
- 1: Credit card
- 2: Cash
- 3: No charge
- 4: Dispute
- 5: Unknown

## Hypothesis Testing
The main component of the project is to conduct a two-sample t-test to determine if there is a significant difference in fare amounts between credit card and cash payments.

### Hypotheses
- Null hypothesis (H0): There is no difference in average fare between customers who use credit cards and those who use cash.
- Alternative hypothesis (HA): There is a difference in average fare between customers who use credit cards and those who use cash.

### Code for Hypothesis Testing
```python
from scipy import stats

# Define groups
credit_card = taxi_data[taxi_data['payment_type'] == 1]['fare_amount']
cash = taxi_data[taxi_data['payment_type'] == 2]['fare_amount']

# Conduct two-sample t-test
t_stat, p_value = stats.ttest_ind(a=credit_card, b=cash, equal_var=False)
print(f"T-statistic: {t_stat}, P-value: {p_value}")
```

## Results
The two-sample t-test resulted in a p-value significantly smaller than the 5% significance level, leading to the rejection of the null hypothesis. This indicates a statistically significant difference in the average fare amounts between credit card and cash payments.

## Conclusion
### Business Insights
- Encouraging customers to pay with credit cards could generate more revenue for taxi cab drivers, as the average fare amount for credit card payments is higher than for cash payments.
- This analysis assumes that customers were randomly assigned to payment methods, which may not reflect real-world behavior.

