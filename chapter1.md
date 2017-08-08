---
title       : Computer Wins!
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:ef1b76935a
## The Buzzword

The term "Machine Learning" has been in town for a while now. It is even being overused by some but to others, it will remain a black box.
This course will educate you on the idea of Machine Learning, from getting the data to improving the accuracy of the models you will create. 
Using two (2) examples, we'll see the processes involved in doing "Machine Learning". You should get the hang of this black box after this course.


According to Wikipedia, Arthur Samuel in 1959 defined Machine Learning as the subfield of computer science that gives computers the ability to learn without being explicitly programmed.

Which of the following is not a Machine Learning Task?

*** =instructions
- Self driving cars
- A program that prints the next 20 leap years
- A program that categorizes emails into spam and non-spam
- Predicting galaxies

*** =hint
Take a look at the options. Which task requires explicitly programming the computer?

*** =pre_exercise_code
```{r}
# None


```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! Even I can calculate the next 50 leap years and I'm only human."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```


--- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:c57adfc430
## A Model - The Secret Weapon


A human can learn the voices of 10 (maybe 100) co-workers and be able to identify them without looking while a machine can learn the voices of over 10,000 people and be able to predict whose voice it is.
Computer wins!

How?  

Answer = Machine Learning!

Processes involved in Machine Learning:

- Get data
- Preprocess (Clean, Prepare, Manipulate Data & Exploratory Data Analysis)
- Train Model
- Test Model
- Post-Process (Visualize, Evaluate, Improve Model & Present)

The first two steps are typical for any analysis involving data.
Creating a model is a critical part of the machine's studies.

A model is an artifact or a formula created by the process of learning from previous data.
When you plug in historical data into a machine learning algorithm, you get a model.

In the above example, the machine uses a model that takes in an input (a person’s voice), does some processing and predicts the name of the person as the output. 

Testing and evaluating the models you will create comes up in later chapters.
You will also learn to improve your model.

A good machine learning model depends on which of the following? 

*** =instructions
- Type of the data and software or statistical tool used for analysis
- Type of machine learning algorithm used and software or statistical tool used for analysis
- The quality of the dataset and type of machine learning algorithm used
*** =hint
Clean historical data + Good Machine Learning algorithm = Great Model!
*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly!"
test_mc(correct = 3, feedback_msgs = c(msg_bad, msg_bad, msg_success))
```
