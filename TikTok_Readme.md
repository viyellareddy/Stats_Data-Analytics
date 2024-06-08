
# TikTok Project: Data Exploration and Hypothesis Testing

## Project Overview
This project involves analyzing data from TikTok to understand the relationship between verified status and video view counts. The goal is to conduct hypothesis tests and statistical analysis to determine if videos from verified accounts have different average view counts compared to videos from unverified accounts. This analysis aims to provide insights that could help TikTok make data-driven decisions.


## Project Structure
The project is structured as follows:
- **data**: Contains the dataset used for the analysis.
- **notebooks**: Contains the Jupyter notebooks used for EDA and hypothesis testing.
- **results**: Contains the results of the analysis and visualizations.
- **README.md**: Project documentation.

## Dependencies
- Python 3.x
- pandas
- numpy
- matplotlib
- seaborn
- scipy


## Data Preparation
The dataset used for this project is a CSV file containing data on TikTok videos, including attributes such as video view count, verified status, video duration, and more.

### Loading the Data
The dataset is loaded using pandas:
```python
import pandas as pd

# Load the dataset
data = pd.read_csv("data/tiktok_dataset.csv")
```

## Exploratory Data Analysis (EDA)
Descriptive statistics are used to understand the data and explore the relationship between verified status and video view counts.

### Code for EDA
```python
# Display first few rows
data.head()

# Generate a table of descriptive statistics about the data
data.describe()

# Check for missing values
data.isna().sum()

# Drop rows with missing values
data = data.dropna(axis=0)

# Compute the mean `video_view_count` for each group in `verified_status`
mean_view_counts = data.groupby("verified_status")["video_view_count"].mean()
print(mean_view_counts)
```

### Data Cleaning
The dataset was cleaned by removing rows with missing values:
```python
# Drop rows with missing values
data = data.dropna(axis=0)
```

## Hypothesis Testing
The main component of the project is to conduct a two-sample t-test to determine if there is a significant difference in view counts between verified and unverified accounts.

### Hypotheses
- Null hypothesis (H0): There is no difference in the average view count between TikTok videos posted by verified accounts and unverified accounts.
- Alternative hypothesis (HA): There is a difference in the average view count between TikTok videos posted by verified accounts and unverified accounts.

### Code for Hypothesis Testing
```python
from scipy import stats

# Save each sample in a variable
not_verified = data[data["verified_status"] == "not verified"]["video_view_count"]
verified = data[data["verified_status"] == "verified"]["video_view_count"]

# Implement a t-test using the two samples
t_stat, p_value = stats.ttest_ind(a=not_verified, b=verified, equal_var=False)
print(f"T-statistic: {t_stat}, P-value: {p_value}")
```

## Results
The two-sample t-test resulted in a p-value significantly smaller than the 5% significance level, leading to the rejection of the null hypothesis. This indicates a statistically significant difference in the average view counts between videos from verified and unverified accounts.

## Conclusion
### Business Insights
- The analysis shows that there is a statistically significant difference in the average view counts between videos from verified and unverified accounts. This suggests there might be fundamental behavioral differences between these two groups of accounts.


