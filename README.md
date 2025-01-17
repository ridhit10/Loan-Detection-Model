# Loan Detection Model 
![](https://github.com/ridhit10/Loan-Detection-Model/blob/main/reduced_size_github_graphic.png)

## Objective
Analyze how loan approval depends on various factors.

## Concepts and Tools used

- Data preprocessing and cleaning (e.g., handling irrelevant columns, splitting datasets).
- Multiple Linear Regression for loan approval prediction.
- Statistical analysis (e.g., interpreting R-squared values, and p-values).
- Data visualization and storytelling through Tableau


## Initial Model:

![](https://github.com/ridhit10/Loan-Detection-Model/blob/main/initial%20model.png)

We will use P-Values to determine if a particular variable is significant using a significance level 0.05. The **p-value** represents the probability of observing the data assuming the null hypothesis is true. The **significance level alpha** is the threshold (e.g., 0.05) below which the p-value indicates a statistically significant result, leading to rejection of the null hypothesis.

Removed Variables: 
Variables with p-values > 0.05 such as:
- Education levels (Bachelor, Doctorate, High School, Master)
- Marital statuses (Married, Single, Widowed)
- Variables like NumberOfDependents, UtilityBillsPaymentHistory, and others with insignificant p-values.

## Final Model:
![](https://github.com/ridhit10/Loan-Detection-Model/blob/main/final%20model.png)

## Model Validity
```r
predictions <- predict(model, test)
mse <- mean((test$LoanApproved - predictions)^2)
rmse <- sqrt(mse) #Lower Values of rmse means it is a good model
```
**MSE** (Mean Squared Error) measures the average squared difference between actual and predicted values, with lower values indicating better model performance. **RMSE** (Root Mean Squared Error) is the square root of MSE, providing the error in the same units as the target variable, making it more interpretable. In our case, rmse comes out to be 0.15 which indicates our model is good enough. 

```r
# Load necessary libraries
library(caret)

# Load the dataset
data <- read.csv("Loan.csv")

# Drop irrelevant columns
data$ApplicationDate <- NULL  # Remove ApplicationDate

# Split the data into training (70%) and testing (30%) sets
set.seed(42)
trainIndex <- createDataPartition(data$LoanApproved, p = 0.7, list = FALSE)
train <- data[trainIndex, ]
test <- data[-trainIndex, ]

# Train a regression model
model <- lm(LoanApproved ~ ., data = train)

# Summarize the model
summary(model)

# To check if model is good or not
predictions <- predict(model, test)
mse <- mean((test$LoanApproved - predictions)^2)
rmse <- sqrt(mse) # Lower values of RMSE mean it is a good model

```

## Loan Approval Trends Dashboard

### Overview
This Tableau dashboard visualizes trends in loan approvals over time, segmented by:
- Employment status (Employed, Self-Employed, Unemployed).
- Age groups (18-25, 26-35, 36-45, 46+).
- Credit scores (using an adjustable filter for average credit scores).

The visualization provides insights into:
- The relationship between employment status and loan approval counts.
- Variations in loan approvals across age groups over time.
- The impact of credit score ranges on loan approvals.

### Key Features
- **Line Chart**: Displays the sum of approved loans (`SUM(Loan Approved)`).
- **Segmentation**:
  - `Employment Status` on rows.
  - `Age Group` on colour for detailed comparison.
- **Interactivity**: Users can filter by `Credit Score` using the adjustable range slider.

![](https://github.com/ridhit10/Loan-Detection-Model/blob/main/tableau.png)

Here is the link to access the Dashboard: 
(My Dashboard)[https://public.tableau.com/app/profile/ridhit.arora/viz/LoanDetectionModel/Sheet1?publish=yes]




