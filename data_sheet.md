# Datasheet 

## Motivation

HDDs Dataset (Baidu Inc.) - Baidu SMART Dataset for Seagate ST31000524NS drive model is available in Kaggle:  (https://www.kaggle.com/datasets/drtycoon/hdds-dataset-baidu-inc)
to be used to build AI models and solve data science challenges.

 
## Composition

This dataset includes data from an enterprise-class disk model - Seagate  ST31000524NS collected at Baidu's datacenter. There are samples from 5750 disks in this dataset. The data has been scaled to avoid presenting the actual measurement values.

## Collection process

SMART Attribute values were read per hour for each disk. For good disks, the samples in a week's period are kept in the dataset, so every good disk has 168 samples. For failed disks, samples in a more extended time period (20 days before actual failure) are saved. Samples may be less than 480 for failed disks if they didn't survive 20 days of operation since Baidu began to collect data.


## Preprocessing/cleaning/labelling

This is a SMART Dataset of HDDs from the Baidu Inc. Datacenter.

Every attribute value is scaled to the same interval [-1, 1] and their exact values withhold for privacy and security. The serial number of the disk is replaced by a number ranging from 1 to 5750.

Each line in the dataset contains 14 columns which are separated by commas. The meaning of each column is listed as follows:<br>
Column 1 : index of the disk representing its serial number, ranging from 1 to 5749<br>
Column 2 : class label of the disk, it is -1 for disks that failed and +1 for disks that are good<br>
Column 3 : VALUE of SMART ID #1, Raw Read Error Rate<br>
Column 4 : VALUE of SMART ID #3, Spin Up Time<br>
Column 5 : VALUE of SMART ID #5, Reallocated Sectors Count<br>
Column 6 : VALUE of SMART ID #7, Seek Error Rate<br>
Column 7 : VALUE of SMART ID #9, Power On Hours<br>
Column 8 : VALUE of SMART ID #187, Reported Uncorrectable Errors<br>
Column 9 : VALUE of SMART ID #189, High Fly Writes<br>
Column 10 : VALUE of SMART ID #194, Temperature Celsius<br>
Column 11 : VALUE of SMART ID #195, Hardware ECC Recovered<br>
Column 12 : VALUE of SMART ID #197, Current Pending Sector Count<br>
Column 13 : RAW_VALUE of SMART ID #5, Reallocated Sectors Count<br>
Column 14 : RAW_VALUE of SMART ID #197, Current Pending Sector Count<br>
<br>
## Uses

In this analysis, only the last sample (timestamp) is used. The historic per hour data can be used for further time series analysis.
One issue with this data is that it is provided with scaling to the interval [-1,1], therefore withholding the real values, which can be very useful for further analysis on identify the range of correctness of the parameters.
This data refers to computer hardware parameters, therefore there are no ethical issues involved.


## Distribution

This data is distributed in Kaggle's site. It is downloadable in .csv format (60MB), and has a CC0 Public Domain license.

## Maintenance

The data is maintained by a user, expected update frequency is annually.

