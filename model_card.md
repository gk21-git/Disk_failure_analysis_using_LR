# Model Card

## Model Description
The model analyzes the main factors that may predict the failure of a hard disk. The data used has been collected from Baidu's Datacenter. Samples were collected from an enterprise-class disk - Seagate  ST31000524NS. There are samples from 5750 different disks in this dataset.

##Input

Each line in the dataset contains 14 columns which are separated by commas. The meaning of each column is listed as follows.
Column 1 : index of the disk representing its serial number, ranging from 1 to 5750 <br>
Column 2 : class label of the disk, it is -1 for disks that failed and +1 for disks that are good.
Column 3 : VALUE of SMART ID #1, Raw Read Error Rate
Column 4 : VALUE of SMART ID #3, Spin Up Time
Column 5 : VALUE of SMART ID #5, Reallocated Sectors Count
Column 6 : VALUE of SMART ID #7, Seek Error Rate
Column 7 : VALUE of SMART ID #9, Power On Hours
Column 8 : VALUE of SMART ID #187, Reported Uncorrectable Errors
Column 9 : VALUE of SMART ID #189, High Fly Writes
Column 10 : VALUE of SMART ID #194, Temperature Celsius
Column 11 : VALUE of SMART ID #195, Hardware ECC Recovered
Column 12 : VALUE of SMART ID #197, Current Pending Sector Count
Column 13 : RAW_VALUE of SMART ID #5, Reallocated Sectors Count
Column 14 : RAW_VALUE of SMART ID #197, Current Pending Sector Count

Every attribute value has been scaled to the interval [-1, 1] and their exact values withhold. The serial number of the disk is replaced by a number ranging from 1 to 5749.
##OUTPUT

The output of the disk is a binary variable, which predicts if the disk has failed (-1) or it is good (+1)

#Model Architecture:
Logistic Regression is used to predict if the disk fails or not, and to understand the weights of the parameters. Hyperopt has been used to optimize the hyperparameters of the model.

## Performance

The model performs well in the analysis of the main causes of disk failure. 
Confusion Matrix for the Test Data:
 
                       Predicted
    True  Failed [[  82          1]
          Good    [  31      1036]]
                   Failed    Good
                       
Test data accuracy  = 0.9721
Test date precision = 0.9990

## Limitations

The main limitation of the model is that it uses a dataset for a specific type of disks. It has not been tested in additional disks, therefore the results and accuracy of the model is limited to this dataset.

## Trade-offs

There is a high accuracy for identifying failed disks. However, it is possile to see that there is a relative high number of good disks that have been labeled as failed. This means that the classification conditions are overly strict and skewed toward detection of failed disks conditions. While it is critical to recognize the failed disks, due to their impact upon MTBF and availability of the system, the false positives will require additional analysis. The number of false positives is still low by comparison to the total number of disks sampled.
