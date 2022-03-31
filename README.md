# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Useful Resources
- [ScriptRunConfig Class](https://docs.microsoft.com/en-us/python/api/azureml-core/azureml.core.scriptrunconfig?view=azure-ml-py)
- [Configure and submit training runs](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-set-up-training-targets)
- [HyperDriveConfig Class](https://docs.microsoft.com/en-us/python/api/azureml-train-core/azureml.train.hyperdrive.hyperdriveconfig?view=azure-ml-py)
- [How to tune hyperparamters](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-tune-hyperparameters)


## Summary
**The bank marketing dataset contained data about individuals applying for bank loans. The task here was to develop a classification model that, based on the information provided about each individual (job_title, education, current_loan_status and more), could predict whether they will subscribe to a service.**

**The best performing model was a VotingEnsemble with an accuracy of 91.74%. A StackEnsemble model was also of comparable accuracy for this task.**

## Scikit-learn Pipeline
The Scikit-learn pipeline pulls data from the URL. The data cleaning process included the following stages:

**Removing NAs from the dataset.
One-hot encoding features: job title, contact type, and education level.
Encoding other categorical variables: marital status, previous loan defaults, current housing situation and current loan status. 
Encoding month and day of the week features.
Encoding the target variable.
Once the data has been prepared it is split into a training and test set. A test set size of 20% of total entries was selected as a compromise between ensuring adequate representation in the test data and providing sufficient data for model training.**

**Due to the nature of the problem (classicication), a logistic regression model was used. LR is statistical model that in its basic form uses a logistic function to model a binary dependent variable. The parameters available within the training script are C (which indicates the regularisation strength i.e. preference for sparser models) and maximum number of iterations.**

**Utilising Azure Hyperdrive, hyperparamter tuning was accomplished by utilising parameter sampling and implementing an early stopping policy.**

**Parameter Sampling: A random paramter sampling method was chosen, as this technique allows for a broad search space of potential optimial paramters to be chosen, without the effort of specifying values, and also has the benefit of supporting early termination of poor performance runs.**

**Early Stopping Policy: the BanditPolicy was chosen as it prevents future tested model who perform worse than previous models from being reported, based on comparison between the slack factor specified and the primary metric chosen, thus eliminating them. This method is a flexable approach to early stopping**

## AutoML
**The best model generated by the AutoML run was a VotingEmsemble, with an accuracy of 91.74%. This is an ensemble machine learning model that combines the predictions from multiple other models and can often out perform other, singular models.**

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**
**Comparison if performance between the LR and the VotingEmsemble (chosen from the AutoML run) showed that the performance of the model generated using AutoML outperformed our LR using the HyperDrive function (accuracy of 91.45%). Despite the differences between the two models being marginal, we can conclude that the AutoML model will result in a better performance as AutoML can through multiple classifciation models and a number of scalers alongside each tested model, adding an additional preprocessing step that could aid in model selection.**

**The main difference between a VotingEnsemble model and a standard Logistic Regression is that a VE averages the probabilities of class selection made from various models, while a LR performs classification by utilising a logistic function to make its classification predictions**

## Future work
**Altering the performnce metric to account for class imbalance and mitigate it. The results from the AutoML run highlighted that there was class imbalance present within our data.**

**Alongside removing class imbalance, some general steps such as increasing our hyperparamter seach space and increaing the timeout of the stopping policy could allow us to search a wider paramter space and give our runs more time to identify optimal models**
