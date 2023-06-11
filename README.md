# PROJECT TITLE : Disk failure analysis

## INTRODUCTION
Prediction of failures in High Performance Computing storage systems components  can help to  increase availability, decrease maintenance cost and help allocate spare parts and manpower more efficiently. The idea behind the project is to use data collected on hard disks health from logs and monitoring in the storage system, using the SMART technology,  to predict the probability of a disk failure. 
This is called a classification problem, in which the final result is a binary finding - the disk is good or defective. 
The objective of the analysis is also shed light on the principal variables that may be useful to predict failure of hard disks. 
 
## DATA
The open HDD Dataset from Baidu Inc datacenter was used. (https://www.kaggle.com/datasets/drtycoon/hdds-dataset-baidu-inc).
The data contains samples from SMART (Self-Monitoring, Analysis and Reporting Technology) measurements of Seagate ST31000524NS disks. This data is tagged as CC0 1.0 Universal (CC0 1.0) - Public Domain, and according to Kaggle's site it is updated annually.
Each disk is labeled good or defective, with only 433 disks in the failed class and the rest of the disks in the good class. This dataset is imbalanced, as the number of good disks in it is more than 10 times that of failed disks.
The dataset provides hourly measurements of the disk SMART measured parameters. For this project we use only the final sample for all disks, as we are not performing a time series analysis of the data. 
The data is normalized to the interval [-1, 1], as the exact values are withheld by for confidentiality.

## MODEL 
Logistic Regression is a classification method that works as a generalized linear model, it can perform supervised binary classification, in our case predict if a component will fail or not based on the variables, which themselves are obtained from historical data (logs), and continuous sensor monitoring. Logistic regression extends linear regression to categorical output. Based on the likelihood of failure, we can then fit a threshold to classify the component as going to fail or not.

There are several advantages for the use of logistic regression in this type of problems:
-	Simple to implement, even if potentially not the most accurate.
-	Interpretable – it is a parametric method, and as we have insight on the parameters we are using, we can have an understanding on which are significant to the outcome, having an impact in the actual failures.
-	It is better at collinearity, can take in account predictor interactions.
-	Provides a measure of the probability of the event, it has strong statistical properties, which help to evaluate the level of confidence of our estimations. This is important as the cost of replacing a good spare part incurs an unnecessary overhead in the maintenance organization, requiring both hardware and manpower to replace the part.
. 

## HYPERPARAMETER OPTIMIZATION
Hyperopt is used to search for the optimal configuration of hyperparameters of the logistic regression. The hyperparameters that were targeted are:
- C: Inverse of regularization strength
- Solver : newton-cg', 'lbfgs', 'liblinear'or 'saga'
- Max number of iterations
- Tol: Tolerance for stopping criteria
- Fit intercept : Specifies if a constant (a.k.a. bias or intercept) should be added to the decision function.
 

## RESULTS
From the execution of the model we obtain the following results for the value of the parameters:<br>
Seek Error Rate  				=  5.0404 <br>
Power on Hours  				=  4.1121<br>
SpinUpTime  					=  2.7639<br>
Reallocated Sector Count  		=  1.0562<br>
Current Pending Sectors counts  =  1.0064<br>
Reported Uncorrectable Error  	=  0.8956<br>
Temperature Celsius  			=  0.3809<br>
Hardware ECC Recovered  		=  0.1807<br>
Raw Read Error Rate  			=  0.0469<br>
High Fly Writes  				=  -0.3776<br>
Current Pending Sector  		=  -1.2449<br>
<br>
The most important parameter highlighted from this analysis is the "uncorrectable errors", which indicates a number of errors that could not be recovered using hardware ECC . Similarly, high seek error rate is also a predictor of failure, it indicates a serious problem with the drive. This could be due to severely bad sectors, mechanical issues, or overheating and servo damage. The total time the disk is powered, and in use have also impact of the lifetime of the disk. It is interesting to see that temperature has a lower impact in the predictions of the failures in disks
