 Mushroom Classification using C5.0 Algorithm
Overview:
This set of R code snippets focuses on the classification of mushrooms into edible and poisonous types using the C5.0 algorithm. The dataset used is named mushrooms.

Libraries Used:
tidyverse: For data manipulation and visualization.
skimr: For providing summary statistics.
gmodels: For creating contingency tables.
C50: For implementing the C5.0 decision tree algorithm.
Instructions:
Library Loading:
Load the necessary libraries:

library(tidyverse)
library(skimr)
library(gmodels)
library(C50)
Dataset Overview and Preprocessing:
Load the mushrooms dataset and perform initial data exploration:

glimpse(mushrooms)
Rename the target variable and convert it into a factor:

mushrooms <- mushrooms %>% rename(type = class)
mushrooms$type <- factor(mushrooms$type, levels = c("p", "e"),
                         labels = c("poisonous", "edible"))
Inspect the modified dataset:

head(mushrooms)
glimpse(mushrooms)
Data Transformation:
Convert all character columns to factors:

mushrooms <- mushrooms %>% 
  mutate_if(is.character, as.factor)
Data Exploration:
Explore unique levels of specific columns:

levels(mushrooms$veil.type)
levels(mushrooms$veil.color)
skim(mushrooms)
unique(mushrooms)
Data Cleaning:
Remove the "veil.type" column:

mushrooms$veil.type <- NULL
glimpse(mushrooms)
Data Splitting:
Split the dataset into training and testing sets:

mush_train <- mushrooms[1:7000,]
mush_test <-  mushrooms[7001:8124, ]
Model Training:
Train the C5.0 decision tree model:

mush_model <- C5.0(mush_train[-1], mush_train$type)
Model Summary:
Display a summary of the trained model:

summary(mush_model)
Model Prediction and Evaluation:
Make predictions on the test set and create a confusion matrix:

mush_pred <- predict(mush_model, mush_test)
CrossTable(mush_test$type, mush_pred, prop.chisq = FALSE,
           prop.r = FALSE, prop.c = FALSE,
           dnn = c("actual type", "predicted type"))
Usage:
Copy and paste the code snippets into an R environment.
Execute the code to load libraries, preprocess data, train the model, and evaluate predictions.
Note:
This code assumes that the mushrooms dataset is available in your R environment.
Modify the code as needed based on specific analysis requirements.
