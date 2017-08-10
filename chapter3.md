---
title       : Will I Make it Big?
description : This chapter introduces the decision tree algorithm. You will learn about random forest algorithm - a variant of the decision tree that improves it and performs better in general. Using random forest algorithm, you will create a model to predict a person's wage based on their age, education and type of job.



--- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:4c2e1e4e93
## Decision Tree Algorithm

Decision tree is a type of `supervised learning` algorithm and is mostly used in `classification` problems. This algorithm involves splitting the population or sample into two or more subpopulation based on most significant splitter in input variables.

Suppose we have a sample of `30 students` with two input variables `Gender` (Boy / Girl) and `Height` (5 to 6 ft). 15 out of these 30 play `Basketball` in leisure time. Students in red play basketball and those in blue do not. Let’s say we want to create a model to predict who will play basketball during leisure period? Basically, we want to separate students who play basketball in their leisure time based on highly significant input variable among all two variables (a.k.a. predictors)


Decision tree is useful here in that it will segregate the students based on all values of two variable. The variable which creates the best similar sets of students (i.e. sets which are dissimilar to each other). 



 ![](http://s3.amazonaws.com/assets.datacamp.com/production/course_4925/datasets/dtree.png)




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
## About the Data

The first step in Machine Learning is getting your data. This step involves finding the raw data in whatever format they are. They may be structured, unstructured, semi structured, whether flat files, tables, JSON format or in a database, video, audio, text etc. 

Now let’s see an example using the Wage dataset provided by the `ISLR` package. 

*** =instructions
- Load the required packages -  ISLR, ggplot2, caret, randomForest
- Use `data(Wage)` function to get the `Wage` dataset into your workspace
- Know more about the Wage dataset. Use str() and dim() on the Wage dataset. Can you interpret the results?
- Call head() and tail() on your dataset to reveal the first and last 6 observations.
- Finally, call the summary() function to generate a summary of the dataset. What does the printout tell you?

*** =hint
- Use library() function for the first instruction.
- The str() function gives you an overview of the different variables of the data.
- The dim() function tells you the number of observations and variables respectively.
- The summary() function returns several measures for each variable. Such as the maximum observed value, the mean and many more!

*** =pre_exercise_code
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code
#None
# Clean up the environment

```

*** =sample_code
```{r}

# Load the required packages




# Get your dataset



#Know more about the Wage dataset.



# Reveal first and last few observations



# Summary of the dataset



```

*** =solution
```{r}

# Load the required packages

library(ISLR)
library(ggplot2)
library(caret)
library(randomForest)

# Get your dataset

data(Wage)

#Know more about the Wage dataset.

str(Wage)
dim(Wage)

# Reveal first and last few observations

head(Wage)
tail(Wage)

# Summary of the dataset

summary(Wage)

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki



test_function("data",
              not_called_msg = "You didn't call `data()`")


test_function("str",
              not_called_msg = "You didn't call `str()`")
              
test_function("dim",
              not_called_msg = "You didn't call `dim()`")
              
test_function("head",
              not_called_msg = "You didn't call `head()`")
              
test_function("tail",
              not_called_msg = "You didn't call `tail()`")
              
                            
test_function("summary",
              not_called_msg = "You didn't call `summary()`")

test_error()

success_msg("Good work!")
```






--- type:NormalExercise lang:r xp:100 skills:1 key:372a383227
## Data Preprocessing

Data preprocesing involves transforming data into a basic form that makes it easy to work with. One characteristics of a tidy dataset is that: one observation per row and one variable per column.
Activities done in this step also includes detecting the presence of missing (NA) values, noise and outliers, or duplicate data

* Do some exploratory data analysis
   
        qplot(age, wage, data=Wage, colour = race)


* We don’t need the variable “logwage” for our analysis, so we remove it.
    
        Wage<- subset(Wage, select=- c(logwage))

*** =instructions
- Now plot age against wage but this time make the colour based on education. 
- Remove other variables not necessary for this analysis such as health, health_ins, region, race, year, sex, and maritl.

*** =hint
- Use subset() function to remove these variables

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Some exploratory data analysis

qplot(age, wage, data=Wage, colour = race)

# Remove unnecessary variables

Wage<- subset(Wage, select=- c(logwage)

```

*** =solution
```{r}
# Some exploratory data analysis

#qplot(age, wage, data=Wage, colour = race)
qplot(age, wage, data=Wage, colour = education)

# Remove unnecessary variables
# Wage<- subset(Wage, select=- c(logwage))  remove this line after creating pre-exercise code
Wage<- subset(Wage, select=- c(health, health_ins, region, race, year, sex, maritl))

```

*** =sct
```{r}

test_function("qplot",
              not_called_msg = "You didn't call `qplot()`")
test_object("Wage")


test_error()

success_msg("Good work!")
```
--- type:NormalExercise lang:r xp:100 skills:1 key:e98de586cb
## Forest of Trees


In this step, you will:

* Partition the data into `training` and `test` sets.
* Create a model to predict `wage` based on three input variables - `age`, `education` and `ob class`.




*** =instructions
- Use createDataPartition() function to partition your dataset
- Your training set should be 70% of the entire dataset 
- Print out the training and test sets  
- Check the dimension of both datasets to know more about the data
- Now plot the training dataset with age on the x-axis, wage on the y-axis and make the colour based on education. What do you notice?
*** =hint
- type ?createDataPartition to know how to use the createDataPartition() function
- Make p=0.7 and set list=FALSE
- To print a variable to the console, simply type the name of the variable on a new line.
- Use `qplot()` for the last instruction. Just as you did in the previous exercise.
- Do you notice that the plot created usinf training set is similar to the plot done on the whole Wage dataset. This is because the createDataPartition function splits the data evenly into training and test sets.

*** =pre_exercise_code
```{r}
library(caret)
```

*** =sample_code
```{r}



```

*** =solution
```{r}


# Partition the data into training and test datasets

inTrain <- createDataPartition(y= training$wage, p=0.7, list=FALSE)

training <- Wage[inTrain, ]

test <- Wage[-inTrain, ]

# Print out training and test sets and show the dimensions of each set

training

test

dim(training)

dim(test)

# Observe plot of training set
qplot(age, wage, data=training, colour = education)

```

*** =sct
```{r}

test_object("training")
test_object("test")


test_function("dim",
              not_called_msg = "You didn't call `dim()`")

test_function("qplot",
              not_called_msg = "You didn't call `plot()`")
              

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






