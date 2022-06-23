General Assembly Project - 2
Date: Apr. 18, 2022
Author: Chenhao (Andy) Xu

1. Problem Statement
When predicting the sale price of a house, there are many methods and many parameters could influence the price, such as time of the purchase, location, house type and area. Models can be simple but also can be very complicated. The project utilized linear regression method to predict the house sale price by analyzing the existing information that provided known house sale price and a lot of selected factors which highly correlated with the price. 


2. Data Cleaning
The project had two datasets, train.csv and test.csv. The train dataset provided the information to create the model and the test dataset helped exam the model accuracy. 
Since there are around 80 columns in the dataset, it's almost impossible to mannually select columns needed in the analysis. Also, there were no reference about mannual selection. thus, the main idea of the data analysis was to let python to choose the parameters that had higher impact on sale price. 

2.1. Load and Check the Data
After load the data, data type, data shape, and null value were checked. Column of SalePrice was only exist in train set not in test set. Around 20 columns contained null values in train set. The null value was not something to focused on this step since we would let python select columns first, then we'd deal with null values. 
The shape of original train dataset was 2051 by 81. 

2.2. Initial Data Cleaning
The initial data cleaning includes column addition, column deletion, and scale convertion. 
The age of house since built and the age of house since last remodeling were added. Meanwhile, columns of year sold, year built, and year remodeled were removed. 
Around 10 columns showed ratings of certain parameters. However, the ratings were in string, like Ex, Gd. In order to simplify the model, scale of 1 - 5 was used, instead of Po, Fa, TA, Gd, and Ex. In addition, several columns contained Yes/No information only. For the same reasion, numeric numbers were used to instead. For example, 1 replaced Y, 0 replaced N, and 0.5 replaced P. 
At the end of initial cleaning, the shape of train dataset was 2051 by 79. 

2.3. Data Split and Separation of Numeric and Object Columns
Data split came ealier than the rest of data cleaning. Since train dataset was planned to split into two sets, train and validation. The train-train set was actually used for model creation and the train-validation was used to validate the model, which means the same as test dataset in general. In oder to aviod data leakage, all the analysis work would only apply to the train set, including column selection. The validation set can only follow the step of train set. 
After data spliting, numeric and object columns were further splited due to different methods for data cleaning. 
At the end of data split, the shape of train dataset was 1640 by 78, validation dataset was 411 by 78, train_num dataset was 1640 by 48, train_obj was 1640 by 30. 

2.4. Numeric Columns Selection
The nuermic columns were analyzed under the principle of correlation value. Columns that had higher correlations with the sale price were selected while the rest was dropped. 0.45 of correlation score was introduced in the case which means columns had more than 0.45 correlation score with the price were selected. 
After the selection, the other rule was applied to the dataset. Due to the missing value, only columns had less than 5% of missing values were selected. Too many missing value may indicate data unaccuracy. 
At the end of numeric column selection, the data shape was 1640 by 17, including the id column. 

2.5. Object Columns Selection
The object columns were selected under the rule of number of the categories. Each column contained different number of categories in the content. If all columns were selected, the model would have high varience which means the model fit the train dataset very well but may not perform well in other dataset. Columns with equal or less than 6 categories were selected. One mannually added column was the neighborhood since we believed the neighborhood had important influence on price even though it contained the most categories. In addition, the null value rule was applied to object columns. 
At the end, the object data shape was 1640 by 20. 

2.6. Combine Numeric and Object Columns
Now, the data cleaning was almost finished. Both datasets were combined to a single dataset as train dataset. 
At the end of this step, the train dataset had the shape of 1640 by 37, the shape of validation dataset was 411 by 37, and the shape of test dataset was 878 by 37. 


3. Feature Engineering and Preprocessing

3.1. Simple Imputer
Due to the existing of null values, simple imputer was introduced. the strategy used as the most frequent number or category.  

3.2. One Hot Encoder
One Hot Enocoder helped dummify the categories in single columns. In this case, all object columns were applied to One Hot Encoder. By removing the first category column of each object column, the final shape of train dataset was 1640 by 110. 

3.3. Polynomial Feature
There were already 58 columns. The polynomial Feature is supposed to largely increase the number of columns. by applying this feature, the columns of each dataset would be 1711, which resulted in too many dimensions in linear regression later on. Thus, the step was skiped. 

3.4. Standard Scaler
Standard Scaler helped evenly rate each columns since each column may have different data range. For example, column of 0 or 1 is not directly compariable with column of people's height. The standard scaler would make all columns fair in the later modeling. 
At the end of data cleaning and processing, the shape of train dataset was 1640 by 110. validation data set was 411 by 58, and test dataset was 878 by 110. 

4. Modeling
Linear regression was applied. The r2 score of the train data set was 0.91, and the validation dataset was 0.89. The root mean squared error of the train dataset was 24,142, the validation data set was 25,842. 


5. Ridge and Lasso
Ridge and Lasso may help further improved the model. 
By applying ridge, The best alpha value was 258, the r2 score of the train data set was 0.88, and the validation dataset was 0.88. The root mean squared error of the train dataset was 27,913, the validation data set was 27,123, which were not improved the model. 
By applying lasso, The best alpha value was 9, the r2 score remained the same as original model. The root mean squared error of the train dataset was 24,148, the validation data set was 25,773, which were not improved the model. 

6. Conclusions and Recommandations
Features add value of house the most: Miscellaneous features not covered (elevator, 2nd garage, tennis court), Roof materials, Above ground living area. 
Features hurt value of house the most: Building type (townhouse), House age since built, House age since last remodeling, Garage in rough finish. 
If house for sale: imporve roof material, masonry veneer area, kitchen, basement, heating system
if buying house for investment: buy house in the neighborhood of Northridge heights, Stone brook, Green hills, Northridge, Crawford


