# Data
The Ames Housing dataset is a widely used dataset for introduction to regression problems.
Ames is city in Iowa, US.
The dataset has a comprehensive list of features concerned with information stakeholders might want to know when evaluating the price of a house.

# Problem Statement
Construct a linear regression model that can generate predicted SalePrice from test.csv with lowest RMSE possible, through EDA, feature engineering and feature selection. 

# Executive Summary
- Understanding of the different variables in the dataset was gained through reading the data dictionary on http://jse.amstat.org/v19n3/decock/DataDocumentation.txt


- Data cleaning and preliminary feature engineering was done on the train.csv file 
    - Conversion of NaN values in categorical variables to 'None' or 0
    - Dropping of features which had relatively weak correlation to SalePrice
    - Combination of the separate features related to size of the house into a single variable Total_Living_SF
    - Dropping of true outliers as suggested from http://jse.amstat.org/v19n3/decock/DataDocumentation.txt
    - Dropping of variables with multicollinearity to certain features in the dataset


- Splitting of train.csv to a training set and testing set


- EDA and continued feature engineering
    - EDA on target variable (SalePrice)
    - Feature engineering: Median (target) encoding of categorical variables
    - Heatmap to plot correlation btw. the different features to SalePrice
    - Scatterplot of the 6 strongest correlated features to SalePrice
    
    
- Feature selection for modelling
    - The 5 strongest positively correlated features + 1 strongest negatively correlated features were chosen
    
    
- Model Construction
    - Cross-validation done on training set using Linear Regression, Ridge and Lasso to choose which to use
        - Linear Regression chosen as very similar performance between the 3
    - Baseline model created with 'Total_Living_SF' as it was the most strongly correlated (non-interacting) feature
    - Subsequently more models were created using more predictors
        - Adjusted R^2 score was used to see if there is actual improvement
    - A new poly-features dataframe was created using the 6 predictor variables + combination of interactions
        - Cross-validation done on this new dataframe


- Model Evaluation on testing set
    - Model 6 (poly-features) chosen as best model
    - Linear Regression, Ridge and Lasso used to see which is the best model on the validating set (testing_set df)
    - Turned out Linear Regression was able to generalize to the unseen testing set
    
    
- Selected model utilized to predict SalePrice using test.csv
    - Kaggle RMSE score of 26181
    
 # Data Dictionary
Due to the extensive number of features in the dataset, only those that were used in the final model will be included in the data dictionary.

|Feature|Type|Usage|Description|
|-------|----|-----|-----------|
|SalePrice|*float*|Target Variable|The target variable; the price of the house at sale|
|Total_Living_SF|*float*|Predictor Variable|Addition of all features related to size of the house, in sq ft.|  
|Neighborhood_MedianPrice|*float*|Predictor Variable|Median price of houses within that neighborhood|
|Overall Qual|*int*, *ordinal*|Predictor Variable|The rating (1-10), 10 being the best, of the overall material & finish of the house|
|Overall Cond|*int*, *ordinal*|Predictor Variable|The rating (1-10), 10 being the best, of the overall condition of the house|
|Garage Area|*float*|Predictor Variable|Size of the garage in sq ft.|
|Year Built|*int*|Predictor Variable|The year the house was built

- Rest of the features can be found on:  http://jse.amstat.org/v19n3/decock/DataDocumentation.txt