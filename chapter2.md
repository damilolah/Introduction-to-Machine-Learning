---
title       :  Does Money Buy Happiness?
description : Insert the chapter description here


--- type:NormalExercise lang:r xp:100 skills:1 key:4c2e1e4e93
## Knowing Your Data

You will create a dataset called `emp_data` having two attributes - earnings and s_rating and 20 observations

`emp_data` = Employee dataset

`earnings` = What each employee earns in dollars per day

`s_rating` = how satisfied the employee is with his/her wage

From this dataset, we will try to predict a new employee's satisfaction rating when he is paid $200, $400, or $1200 per day.
So, earnings is the predictor and s_rating is the class we'll predict.

This exercise uses just one attribute for prediction and that is employee’s `earnings`. 

It is Machine learning practice to partition dataset for analysis into Training and Test sets.

The training set could be 60 - 70% of the entire dataset while the test set is the percentage remaining.


*** =instructions
- Plot `emp_data` with earnings on the x-axis and s_rating on the y-axis
- Use createDataPartition() function in R to partition your dataset
- You training set should be 60% of the entire dataset 
- Print out the training and test sets  
- Check the dimension of both datasets to know more about the data
*** =hint
- Use `plot()` for the first instruction.
- Make sure yo have loaded the caret package into your workspace by typing `library(caret)` 
- type ?createDataPartition to know how to use the createDataPartition() function
- Make p=0.6 and set list=FALSE
- To print a variable to the console, simply type the name of the variable on a new line.
- Use the `dim()` function on training and test set for the fourth instruction

*** =pre_exercise_code
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code
#None
# Clean up the environment

```

*** =sample_code
```{r}
# Loading the required package

library(caret)

# Creating the dataset
earnings <- c(120, 100, 700, 200, 60, 20, 200, 130, 150, 160, 170, 180, 190, 210, 220, 400, 550, 670, 695, 300)

s_rating<- c(50, 60, 80, 75, 50, 70, 75, 60, 50, 65, 70, 71,80, 82, 85, 80, 88, 90, 90, 60)

emp_data  <- data.frame(earnings, s_rating)

emp_data 

dim(emp_data)

# Some exploratory data analyses - plot emp_data



#Set seed to make your analysis reproducible

set.seed(222)

# Partition the data into training and test datasets

inTrain <- 

training <- emp_data[inTrain,]

test <- 

# Print out training and test sets and show the dimensions of each set

```

*** =solution
```{r}

# Loading the required package

library(caret)

# Creating the dataset
earnings <- c(120, 100, 700, 200, 60, 20, 200, 130, 150, 160, 170, 180, 190, 210, 220, 400, 550, 670, 695, 300)

s_rating<- c(50, 60, 80, 75, 50, 70, 75, 60, 50, 65, 70, 71,80, 82, 85, 80, 88, 90, 90, 60)

emp_data  <- data.frame(earnings, s_rating)

emp_data 

dim(emp_data)


# Some exploratory data analyses 
par(cex=.8)
plot(earnings, s_rating, data = emp_data, col=s_rating, main="Regression Modelling")

#Set seed to make your analysis reproducible

set.seed(222)

# Partition the data into training and test datasets

inTrain <- createDataPartition(y= emp_data$s_rating, p=0.6, list=FALSE)

training <- emp_data[inTrain, ]

test <- emp_data[-inTrain, ]

# Print out training and test sets and show the dimensions of each set

training

test

dim(training)

dim(test)


```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki


test_function("plot",
              not_called_msg = "You didn't call `plot()`")

test_object("inTrain")
test_object("training")
test_object("test")


test_function("dim",
              not_called_msg = "You didn't call `dim()`")



test_error()

success_msg("Good work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:a2a9af68a2
## Create Model

The `lm()` function in R is an implementation of the Linear Regression algorithm. 

You will create a linear model called `reg_model` by plugging in the training set into the `lm()` function.

This model is simply a line. Regression modelling is used to find equations(lines) that fit data.

The equation is of the form:

y = a + bx + ei

y is what we want to predict and x includes all the predictors required to form the model above.

a and b are coefficients determined by the `lm()` function we’ll use shortly. ei stands for error as a result of the factors we did not consider. 
The best model is one that minimizes ei the most. 

Regression model is easy to implement but it often produces low performance models. This method is useful when the variable involved can be modelled in a linear way.

For example, increase in age leads to increase in weight, or increase in age leads to decrease in the number of hairs on head. This cannot be used in showing increase in library visitor per day of the week. This is usually non-linear.

*** =instructions
- Create a linear model called reg_model
- Plot the `training` set with earnings on the x-axis and s_rating on the y-axis
- Draw a regression line on the plot above that represents the model reg_model 
- Print out the coefficients a and b 

*** =hint
- Type `?lm` to learn how to use the lm() function
- Use `abline()` function to fit a line to the plot  
- type ?coef to know how to use the coef() function

*** =pre_exercise_code
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_4925/datasets/ml.RData"))


# Clean up the environment

```

*** =sample_code
```{r}

# Create a linear model called reg_model

reg_model <- 


# Know more about your model

summary(reg_model)

# Plot the training set



# Draw a regression line that represents the model reg_model



# Print out coefficient 'a'



# Print out coefficient 'b'





```

*** =solution
```{r}

# Create a linear model called reg_model

reg_model <- lm(s_rating ~ earnings, data=training)

# Know more about your model

summary(reg_model)

# Plot the training set
par(cex=.8)
plot(training$earnings, training$s_rating, col = s_rating, main="Regression Modelling")

# Draw a regression line that represents the model reg_model
abline(reg_model)



# Print out coefficient 'a'

a <- coef(reg_model)[1]

# Print out coefficient 'b'

b <- coef(reg_model)[2]


```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_object("reg_model")



test_function("abline",
              not_called_msg = "You didn't call `abline()`")

test_object("a")
test_object("b")

test_error()

success_msg("Good work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:e98de586cb
## Test Model

We could create a function to test our model



*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

# Create predict_happiness() function
predict_happiness <- function(x){

  a = coef(reg_model)[1]
  b = coef(reg_model)[2]
  Result<- a + (b * x) 
  percent<- "%"
  cat(sprintf("The employee should be %s%s satisfied", Result, percent))
}

# Predict satisfaction when employee is paid $200, $400, and $1200 using predict_hapiness function

predict_happiness(200)






# pred_rating - Predicted satisfaction rating for test set

pred_rating <- predict(reg_model, test)

# Compare test set s_rating with predicted s_rating for the test set
print(data.frame(test$s_rating, pred_rating))


```

*** =sct
```{r}

```
