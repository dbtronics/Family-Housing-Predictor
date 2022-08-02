# Family Housing Predictor
## Background
Real estate is a billion-dollar industry but comes with many inefficiencies. Soon, realtors will be replaced by technology for their role as intermediaries between buyers and sellers. New innovations are changing how we approach real estate and it is for the better for ordinary people looking to buy or sell their first place.

This is used as a proof-of-concept idea where this model acts as a one-stop-shop for families to check the prices of the house that they chose, and then check their approval rate for the amount of mortgage they need.

## Data Source
### Ontario House Prices
Ontario data has been extracted from Kaggle source which can be viewed [HERE](https://www.kaggle.com/code/thiagoribeiro/house-sales-in-ontario-data-analysis/data). The statistics for the data is shown as below:
<img width="262" alt="Screen Shot 2022-08-01 at 8 55 40 PM" src="https://user-images.githubusercontent.com/37752863/182269506-7722415f-3cca-49a8-95f5-d129d2595ee5.png">

This data source has 25K data with minimum price of $0 (anomaly) and maximum price of $32.5M. This data is based on July 2016 housing prices.

### Loan Prediction
Loan prediction dataset was extracted from Kaggle source which can be viewed [HERE](https://www.kaggle.com/datasets/altruistdelhite04/loan-prediction-problem-dataset). The statistics for the training dataset is shown below:

<img width="232" alt="Screen Shot 2022-08-01 at 9 15 24 PM" src="https://user-images.githubusercontent.com/37752863/182271038-c3e75da4-a3d2-4e18-a2c6-2deef6af7cf2.png">
<img width="389" alt="Screen Shot 2022-08-01 at 9 23 01 PM" src="https://user-images.githubusercontent.com/37752863/182271758-76185c08-b115-417f-84a1-9d40c1cfd50b.png">


The statistics for the test dataset is shown below:

<img width="226" alt="Screen Shot 2022-08-01 at 9 15 37 PM" src="https://user-images.githubusercontent.com/37752863/182271073-46a4c073-bb18-4bcb-9e86-6b89785fa765.png">
<img width="388" alt="Screen Shot 2022-08-01 at 9 23 11 PM" src="https://user-images.githubusercontent.com/37752863/182271793-43b8682e-42e3-49c6-8af1-ae0be5bdf7c7.png">

## Normalization and Data Cleaning
For both data we needed to do certain data cleaning and had to convert qualitative data into a quantitative data so that it can be passed to MLP (Multi-Layered Perceptron) network model which can accurately predict our data. 

For housing dataset we did the following ammendments in the data:
* Remove all the housing prices that were less than $100k as it doesn't make sense since the housing prices are so inflated in Canada.
* Removed "S.No" and "Address" fields as that is unnecesssary.
* "AreaName" is qualitative so, had to serialize all the unique area name into numbers. Turns out there are 1,120 different area names in the dataset and has been serialized from {0, 1, 2... 1120}.

The following dataset is shown below:

<img width="427" alt="Screen Shot 2022-08-01 at 9 34 58 PM" src="https://user-images.githubusercontent.com/37752863/182272894-8b3b4f8b-dd97-4c33-ae74-5a7df81a25a7.png">

For loan dataset, we did the following changes:
* We removed all the blank entries in a field (this significantly reduced the dataset for both test and train).
* We serialized all the qualitative data into quantitiative numbers for our network model.
* Since this was based on personal loans, we had to multiply the "LoanAmount" by 10, so it can be treated as a mortgage.

Final Train Dataset is shown below:

<img width="567" alt="Screen Shot 2022-08-01 at 9 39 07 PM" src="https://user-images.githubusercontent.com/37752863/182273324-6ee20141-7fa8-4a3b-bbf3-8085587c8788.png">

Final Test Dataset is shown below:

<img width="565" alt="Screen Shot 2022-08-01 at 9 39 55 PM" src="https://user-images.githubusercontent.com/37752863/182273389-282385a1-dcc6-4ffd-b57a-076d5a518248.png">

## MLP Network and Perimeter Tuning
For this dataset we're using 4 layer neural network architecture with 64 and 32 hidden neurons respectively with relu activation and adams gradient descent for better convergence. We make a model for both housing and loan dataset. We used housing model to predict the price and then use the mortgage value in loan prediction to see whether the family is approved for the loan or not.

The perimeters to test out the network is given below:

<img width="660" alt="Screen Shot 2022-08-01 at 10 22 13 PM" src="https://user-images.githubusercontent.com/37752863/182278021-50464744-2fec-4285-b16c-3fb56214b390.png">

The results for housing price and loan prediction are given below:

`Price Range: 400,000 – 500,000 --> $490,916.88`

```House Price: $490,916.88
Down Payment: $98,183.38
Mortgage Needed: $392,733.51

Loan Approval: N
```
