
# Statistical Analysis of Risk Factors Associated with Sleep Disorder

## Introduction
This study investigates the relationships between key lifestyle factors and the occurrence of sleep disorders. It also explores how these lifestyle factors are associated with sleep duration, with a focus on variables such as physical activity and stress level.

## Project Objective
The primary objective of this study is to investigate the relationships between key lifestyle factors and the occurrence of sleep disorders. Additionally, the study aims to explore how these lifestyle factors are associated with sleep duration, with a particular focus on variables such as physical activity and stress level.

## Hypotheses
- **Null Hypothesis (H0):** Various factors, including age, gender, occupation, physical activity, and stress level, do not have a statistically significant impact on the presence of sleep disorders.
- **Alternative Hypothesis (HA):** Various factors, including age, gender, occupation, physical activity, and stress levels, have a statistically significant impact on the presence of sleep disorders.

## Methods

### Data
The data for the analysis is obtained from Kaggle's sleep health and lifestyle dataset. The data contains information from 374 participants on their age, gender, occupation, sleep duration, quality of sleep, blood pressure, heart rate, stress level, BMI category, physical activity, daily steps, and their sleep disorder status.

### Loading Libraries
The following libraries are required for the analysis:
- `ggplot2` for data visualization
- `reshape2` for data reshaping
- `dplyr` for data manipulation
- `GGally` for enhanced ggplot2 plots

### Preprocessing Data
The data is preprocessed to convert categorical variables into numeric formats for analysis.

### Descriptive Analysis
Descriptive statistics and visualizations are used to explore the data and understand the distributions and relationships between variables.

## Instructions

### Step 1: Load the Data
```r
sleep_data <- read.csv("~/Desktop/Sleep_health_and_lifestyle_dataset.csv", header = TRUE, row.names = 1)
```

### Step 2: Load the Required Libraries
```r
if (!requireNamespace("GGally", quietly = TRUE)) {
  install.packages("GGally")
}
library(ggplot2)
library(reshape2)
library(dplyr)
library(GGally)
```

### Step 3: Preprocess the Data
```r
sleep_data_mod <- sleep_data
sleep_data_mod$Gender <- ifelse(sleep_data_mod$Gender == 'Male', 1, 0)
mapping_vector <- c("None" = 0, "Sleep Apnea" = 1, "Insomnia" = 2)
sleep_data_mod$Sleep.Disorder <- mapping_vector[sleep_data_mod$Sleep.Disorder]

data <- sleep_data_mod[, c(1, 2, 4, 5, 6, 7, 10, 12)]
```

### Step 4: Descriptive Analysis
```r
# Calculate descriptive statistics for numerical variables
sleep_data %>%
  summarize(
    mean = mean(Age),
    median = median(Age),
    sd = sd(Age),
    iqr = IQR(Age)
  ) %>%
  print()

# Define age ranges and corresponding colors
age_ranges <- c("26-35", "36-45", "46-55", "56-60")
age_colors <- c("pink", "lightgreen", "lightblue", "purple")

# Create a new variable that represents age ranges
sleep_data$Age_Group <- cut(sleep_data$Age, breaks = c(26, 35, 45, 55, max(sleep_data$Age)), labels = age_ranges)

# Create a histogram with custom colors for different age groups
ggplot(sleep_data, aes(x = Age, fill = Age_Group)) +
  geom_histogram() +
  labs(title = "Distribution of Age by Age Group") +
  scale_fill_manual(values = age_colors)

# Create a histogram for Age with colors
ggplot(sleep_data, aes(x = Age, fill = Gender)) +
  geom_histogram() +
  labs(title = "Distribution of Age")

# Create boxplots for numerical variables
ggplot(sleep_data, aes(x = Gender, y = Sleep.Duration, fill = Gender)) +
  geom_boxplot() +
  labs(title = "Distribution of Sleep Duration by Gender")

# Create frequency tables for categorical variables
table(sleep_data$Sleep.Disorder)

# Create a boxplot for Quality of Sleep by Gender
ggplot(sleep_data, aes(x = Gender, y = Quality.of.Sleep, fill = Gender)) +
  geom_boxplot() +
  labs(title = "Distribution of Quality of Sleep by Gender")

# Create a boxplot for Physical Activity Level by Gender
ggplot(sleep_data, aes(x = Gender, y = Physical.Activity.Level, fill = Gender)) +
  geom_boxplot() +
  labs(title = "Distribution of Physical Activity Level by Gender")

# Create a bar plot to visualize the distribution of Sleep Disorder by Gender
ggplot(sleep_data, aes(x = Gender, fill = Sleep.Disorder)) +
  geom_bar(position = "fill") +
  labs(title = "Distribution of Sleep Disorder by Gender") +
  scale_fill_manual(values = c("None" = "lightgreen", "Insomnia" = "purple", "Sleep Apnea" = "lightblue"))

# Create a contingency table of "Sleep Disorder" and "Gender"
contingency_table <- table(sleep_data$Sleep.Disorder, sleep_data$Gender)
contingency_table
```

## Results

### Descriptive Analysis
The descriptive analysis revealed the following key insights:
- The mean age of participants is approximately 37.6 years.
- The average sleep duration is 6.8 hours.
- There is a notable variation in sleep quality and physical activity levels among participants.

### Visualizations
- The distribution of age shows a concentration of participants in the 26-35 and 36-45 age groups.
- Males and females have different distributions in terms of sleep duration and quality of sleep.
- Physical activity levels vary significantly between genders.

### Statistical Tests
#### ANOVA
An ANOVA test was conducted to determine if there are statistically significant differences in sleep disorders based on gender, age, stress level, and physical activity level. The results indicate that these factors significantly impact the presence of sleep disorders.

#### Pairwise T-tests
Pairwise t-tests were conducted to compare the means of different groups:
- Gender vs. Sleep Disorder
- Age vs. Sleep Disorder
- Physical Activity Level vs. Sleep Disorder
- Sleep Duration vs. Sleep Disorder

The t-tests revealed significant differences between these groups, suggesting that these factors are associated with the presence of sleep disorders.

#### Chi-square Test of Independence
A chi-square test was conducted to assess the relationship between gender and sleep disorder status. The test results indicate a significant association between gender and the occurrence of sleep disorders.

## Conclusion
The analysis demonstrates that various lifestyle factors, including age, gender, physical activity level, and stress level, have a significant impact on the presence of sleep disorders. These findings can help inform interventions aimed at improving sleep health by addressing these key factors.

