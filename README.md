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

![](https://github.com/ridhit10/Loan-Detection-Model/blob/main/photo.png)

We will use P-Values to determine if a particular variable is significant using a significance level 0.05. The **p-value** represents the probability of observing the data assuming the null hypothesis is true. The **significance level alpha** is the threshold (e.g., 0.05) below which the p-value indicates a statistically significant result, leading to rejection of the null hypothesis.

Removed Variables: 
Variables with p-values > 0.05 such as:
- Education levels (Bachelor, Doctorate, High School, Master)
- Marital statuses (Married, Single, Widowed)
- Variables like NumberOfDependents, UtilityBillsPaymentHistory, and others with insignificant p-values.

## Final Model:
![](


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




