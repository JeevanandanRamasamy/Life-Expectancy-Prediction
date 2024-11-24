# Life Expectancy Prediction

This project develops a series of regression models to predict the average life expectancy of countries in 2009, using socio-economic and health-related variables. It incorporates both continuous and discrete predictors, applying transformations as needed to address skewness and non-linearity in the data. The following guide outlines the process, from data exploration to model development and evaluation.

## Dataset Variables

The dataset contains the following variables for each country:

-	**country**: The name of the country
- **population**: The total population of the country
- **life_expectancy**: The life expectancy in 2009 (target variable)
- **income**: The income per capita of the country
- **babies_per_woman**: The average number of children born per woman
- **child_mortality**: The child mortality rate in the country
- **CO2_emissions_per_person**: The CO2 emissions per person in the country
- **gdp_per_capita**: The GDP per capita of the country
- **total_health_spending_per_person**: The total health spending per person
- **population_density**: The population density of the country
- **at_least_basic_water_source**: The percent of the country’s population that has access to at least basic water sources
- **murders**: The murder rate in the country

---

## Data Transformation

We begin by transforming the dataset. Several new variables are created through transformations:

- **Income Level**: Countries are grouped into income levels based on their income. This allows us to classify countries into different categories for comparison.
- **Logarithmic Transformations**: Several variables, such as life expectancy, income, and child mortality, are log-transformed to linearize relationships and stabilize variance.
- **Additional Variables**: We create new variables like `income2` (income squared) to capture potential non-linear effects, and `two_babies_per_women` to distinguish countries with lower fertility rates.

These transformations help to simplify the relationships between the variables and make the data more suitable for modeling.

---

## Boxplots for Indicator Variables

Boxplots are used to visualize the distribution of life expectancy based on categorical variables such as income level and fertility rate (whether the number of babies per woman is less than or equal to 2). These boxplots provide insight into how life expectancy differs across categories, highlighting any potential outliers or patterns.

## Influential Points or Erroneous Records?

By inspecting the top records for variables like life expectancy, income, and child mortality, we examine whether there are any influential points or erroneous data. In our analysis, no concerning records were identified that would significantly affect the results.

## Correlation Matrix of Variables

A correlation matrix was computed to examine the relationships between continuous variables. Some variables are highly correlated, such as:

- **Child Mortality and Babies per Woman**: These two variables are closely related, suggesting that countries with higher fertility rates tend to have higher child mortality.
- **Income and Babies per Woman**: There is a strong correlation, indicating that wealthier countries tend to have lower fertility rates.
- **GDP per Capita and Income**: These two variables are also strongly correlated, which is expected since they both reflect economic factors.
- **Total Health Spending per Person and Income**: Countries with higher incomes typically spend more on health care per capita.

These correlations suggest that some variables may be collinear, which could affect the results of regression models.

---

## Model Evaluation

- **Residual Analysis**: For each model, residuals were examined to ensure that the model assumptions are met (normality and homoscedasticity).
- **Model Performance**: The goodness-of-fit was evaluated using metrics such as Adjusted R-squared, AIC, and BIC. These metrics help assess how well the model explains life expectancy while penalizing for unnecessary complexity.
- **Cross-Validation**: To evaluate the robustness of Model 7, we used 100 iterations of training and testing splits (70% training, 30% testing) and calculated the Sum of Squared Errors (SSE) for each iteration. The mean and standard deviation of the SSE are also computed.

## Best Model

The final model in this analysis, `life_exp_model7`, is a linear regression model designed to predict life expectancy (in log-transformed form) based on two key predictors: **income** (log-transformed income per capita) and **child mortality** (log-transformed child mortality rate). Additionally, it includes an interaction term between **income** and **child mortality**, which allows the model to capture how the effect of income on life expectancy changes depending on the level of child mortality.

---

## R Packages Needed

To run the models and analysis in this project, the following R packages are required:
1. `tidyverse`: This is a collection of R packages that work together to simplify data manipulation, visualization, and analysis. It includes packages like `ggplot2` (for visualization), `dplyr` (for data manipulation), `tidyr` (for tidying data), and `readr` (for reading data). These packages are used extensively throughout the code for tasks such as creating plots, filtering data, and summarizing results.
2. `gapminder`: This package provides the gapminder dataset, which contains information on global life expectancy, GDP, and population for various countries over time. While not directly used in all parts of the code, it could be helpful for illustrative purposes or additional data analysis in similar contexts.
3. `countrycode`: This package helps in converting country names or codes between different standards (e.g., ISO codes to country names). It could be useful for mapping country-level data in your analysis if the dataset includes country identifiers that need conversion.
4. `moderndive`: This package is designed to streamline the analysis and presentation of linear regression models. It provides functions for summarizing regression output in a more readable format and for performing model diagnostics, making it easier to interpret results. Functions like `get_regression_table()` and `get_regression_summaries()` might come from this package or have similar functionality.
5. `caTools`: This package provides tools for data splitting, which is useful when working with machine learning models or when you want to divide your data into training and test sets. The `sample.split()` function is used to split the data for cross-validation or model evaluation.
