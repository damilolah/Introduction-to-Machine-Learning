---
title       : A Random Forest Prediction
description : Here, you will learn to use the random forest algorithm to create a model.




--- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:4c2e1e4e93
## Decision Tree Algorithm

Decision tree is a type of `supervised learning` algorithm and is mostly used in `classification` problems. This algorithm involves splitting the population or sample into two or more subpopulation based on most significant splitter in input variables.

Suppose we have a sample of `30 students` with two input variables `Gender` (Boy / Girl) and `Height` (5 to 6 ft). 15 out of these 30 play `Basketball` in leisure time. Students in red play basketball and those in blue do not. Let’s say we want to create a model to predict who will play basketball during leisure period? Basically, we want to separate students who play basketball in their leisure time based on highly significant input variable among all two variables (a.k.a. predictors)


Decision tree is useful here in that it will segregate the students based on all values of two variable. The variable which creates the best similar sets of students (i.e. sets which are dissimilar to each other). 



![](http://s3.amazonaws.com/assets.datacamp.com/production/course_4925/datasets/rf.png)




In the figure above, you can see that variable Gender is able to identify best subpopulation sets compared to the variable height.



`Random Forest` algorithm is a variant of decision tree algorithm. The algorithm involves constructing a multitude of decision trees at training time and outputting a result that is the `mode class` or `mean prediction` of the individual trees. This makes random forest `very accurate` and popular among data people.


### `CLASS ACTIVITY:`
Use `help(randomForest)` to find the documentation for randomForest package. 
Study the manual and answer the question below:

Which of the following argument is used to specify the number of trees to grow?

*** =instructions
- mtry
- nodesize
- forest
- ntree

*** =hint
- Type `help(randomForest)` in the R console to find the documentation for randomForest package.

*** =pre_exercise_code
```{r}
library(randomForest)


```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly!"
test_mc(correct = 4, feedback_msgs = c(msg_bad, msg_bad, msg_bad, msg_success))

```


--- type:NormalExercise lang:r xp:100 skills:1 key:a2a9af68a2
## Will I Make it Big?

Now let’s see an example. Using the Wage dataset provided by the `ISLR` package, you will create a model to predict wage based on three input variables - age, education and job class.



*** =instructions
- Load the required packages -  ISLR, ggplot2, caret, randomForest
- Use `data()` function to load the `Wage` dataset into your workspace
- Know more about the Wage dataset. Use str() and dim() on the Wage. Can you interpret the results?
- Call head() and tail() on your dataset to reveal the first and last 6 observations.
- Finally, call the summary() function to generate a summary of the dataset. What does the printout tell you?

*** =hint
- Use `library()` for each package in the first instruction. 
- Make sure you have loaded the caret package into your workspace by typing `library(caret)` 
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



# Partition the data into training and test datasets

inTrain <- 

training <- emp_data[inTrain,]

test <- 

# Print out training and test sets and show the dimensions of each set

```

*** =solution
```{r}

# Load the required packages

library(ISLR)
library(ggplot2)
library(caret)
library(randomForest)

# Creating the dataset
earnings <- c(120, 100, 700, 200, 60, 20, 200, 130, 150, 160, 170, 180, 190, 210, 220, 400, 550, 670, 695, 300)

s_rating<- c(50, 60, 80, 75, 50, 70, 75, 60, 50, 65, 70, 71,80, 82, 85, 80, 88, 90, 90, 60)

emp_data  <- data.frame(earnings, s_rating)

emp_data 

dim(emp_data)


# Some exploratory data analyses 
par(cex=.8)
plot(earnings, s_rating, data = emp_data, col=s_rating, main="Regression Modelling")


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

Here, you will create a function called `predict_happiness` to test your model. 

You are to get coefficients `a` and `b` from `reg_model` and predict satisfaction when employee is paid `$200`, `$400`, and `$1200` using `predict_hapiness` function.

predict_happiness <- function(x){
  
  a = 
  
  b =
  
  Result<- a + (b * x) 
 
  percent<- "%"
  
  cat(sprintf("The employee should be %s%s satisfied", Result, percent))
  
  }

*** =instructions
- Complete the predict_happiness function 
- Insert $200, $400 and then $1200
- Instead of using `predict_happiness` function, you can also use the built-in `predict` funtion provided by caret package.The predict function takes in the model and the test dataset like this
`predict(red_model, test)`. Put all your predicted values in a variable called `pred_rating` as in `pred_rating <- predicted(reg_model, test)`
- Compare pred_rating with the s_rating column in the test data.

*** =hint
- Get coefficents `a` and `b` from  `reg_model` using the `coef()` function as in previous exercises.
- Use the data.frame() function to create a table with two variables pred_rating and test$s_rating.

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

# Create predict_happiness() function
# Get coefficients a and b from reg_model

predict_happiness <- function(x){

  a = 
  b = 
  Result<- a + (b * x) 
  percent<- "%"
  cat(sprintf("The employee should be %s%s satisfied", Result, percent))
}

# Predict satisfaction when employee is paid $200, $400, and $1200 

predict_happiness(200)




# pred_rating - Predicted satisfaction rating for test set

pred_rating <- 

# Compare test set s_rating with predicted s_rating for the test set



```

*** =solution
```{r}

# Create predict_happiness() function
# Get coefficients a and b from reg_model

predict_happiness <- function(x){

  a = coef(reg_model)[1]
  b = coef(reg_model)[2]
  Result<- a + (b * x) 
  percent<- "%"
  cat(sprintf("The employee should be %s%s satisfied", Result, percent))
}

# Predict satisfaction when employee is paid $200, $400, and $1200 

predict_happiness(200)





# pred_rating - Predicted satisfaction rating for test set

pred_rating <- predict(reg_model, test)

# Compare test set s_rating with predicted s_rating for the test set
data.frame(pred_rating, test$s_rating)


```

*** =sct
```{r}

test_object("predict_happiness")
test_object("pred_rating")


test_error()

success_msg("Good work!")

```

--- type:NormalExercise lang:r xp:100 skills:1 key:a299b37ba8
## Check Accuracy

There a number of ways to evaluate your model. For this exercise, you will use the root-mean-square error (RMSE). 
RMSE is gotten by calculating mean squared errors. This is simply a measures of deviation of predicted points from the original value.


The formula is:

  rmse  = ![](http://s3.amazonaws.com/assets.datacamp.com/production/course_4925/datasets/rmse.png)


Where:

 * f = predicted values 
 * o = true values 
The bar above the squared differences means find the mean of the squared difference.


*** =instructions
- You can find the rmse of the test dataset by running the code below in the console:

    `sqrt(sum((pred_rating - test$s_rating)^2))`

*** =hint


*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Check accuracy bu calculating the RMSE 



```

*** =solution
```{r}

# Check accuracy bu calculating the RMSE 

check_accuracy <- sqrt(sum((pred_rating - test$s_rating)^2))


```

*** =sct
```{r}
test_object("check_accuracy")


test_error()

success_msg("Good work! At this point, you can accept your model and present your work or seek to improve your model.")


```






