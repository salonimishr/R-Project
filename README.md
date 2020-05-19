# R-Project
## Linear Regession

In the dataset of automobiles, in order to find the relationship between miles per gallon(dependent variable) with cylinder, displacement,
weight, horsepower, acceleration and model year(independent variables). I used simple and multiple linear models. There were total 398 
observations about automobiles. Using Rstudio*, I explored the data and found that variable horsepower was captured in factor instead of
numeric format and there were some data entry issues as some entries were marked as "?". When I changed this variable from factor to 
numeric format, the issue resolved as NA; in R, missing values are represented by the symbol NA (not available). After this, I divided the
dataset into two parts, i.e., training set and test set. Training set has 300 observations, whereas test set has 98. I did this for 
validation. Using the training dataset, I fitted approximately 60 models (please refer the log submitted with the report) and selected the
best model based on the highest value of adjusted R squared. I use adjusted R squared  instead of multiple R squared because it also 
adjusts the number of predictors in selecting the best model. The best model: 
	
mpg=6.761682+(-0.353565 )cylinder+(-0.005489)weight+(0.447231)model.year

has adjusted R squared 0.8143 and multiple R squared 0.8161. Using this model, I predicted the value of the mpg of test set
(98 observations). Then found residuals by subtracting actual mpg to predicted mpg.residuals are normally distributed and are almost 
homogeneous, hence the linear model can be used and the average value of residuals is 4.03,  hence is near to actual value. It can be
interpreted from the model that increase in the number of cylinders and weight decreases mpg whereas the newer the model year, higher 
the mpg. 

## Logistic Regression

, I used the available dataset of UCI repository that is default of credit card clients in Taiwan from April 2005 to September 2005. 
In this dataset, there are 25 variables and 30000 individuals.There are 25 variables. Default Payment is dependent variable with value 0
as No and 1 as yes. Other variables are ID, limit balance, SEX: Gender (1=male, 2=female), EDUCATION: (1=graduate school, 
2=university, 3=high school, 4=others),MARRIAGE: Marital status (1=married, 2=single, 3=others), AGE: Age in years, PAY_0: Repayment 
status in September, 2005 (-1=pay duly, 1=payment delay for one month, 2=payment delay for two months, … 8=payment delay for eight 
months, 9=payment delay for nine months and above), PAY_2, PAY_3, PAY_4, PAY_5, PAY_6 where PAY_2 is Repayment status in August, 2005
and other variables of PAY as subsequent months. From BILL_AMT1: Amount of bill statement in September, 2005 (NT dollar) to BILL_AMT6
i.e., till April, 2005. From PAY_AMT1: Amount of previous payment in September, 2005 (NT dollar) to PAY_AMT6 i.e., till April, 2005.

### EXPLAROTARY DATA ANALYSIS (EDA):
Exploration of data is very necessary step to understand the data and its variables.  In this dataset, “default payment next month” is 
response variable and is categorical. It has two levels, 1 Yes (defaulter) and 0 (not defaulter). I labeled them defaulter and not 
defaulter for further use. In this dataset, 23364 individuals are not defaulters, whereas 6636 are defaulters. 
The ggplot2 library of R is used to get the visualization as the first step of EDA (please see output for more details).
The discussion about only few plots are given ahead. The violin plot is used to explore the association of age with being defaulter,
the width of plot is wider for defaulter around age 30 and is less in both the groups after age 60 which suggest more defaulter around 
age 30 and presence of less old age people in the random sample of credit card users and can be linked to the less use of credit card in
old age people. Surprisingly, in pie chart the female percentage is slightly higher in defaulter group which could be non-significant
and merely by chance. Using bar chart, the presence of married and single in default group is similar but singles are more in 
non-defaulter group which can be linked to less economic burden on singles. As second step of EDA, five-point summary is generated for
all continuous variables. However, frequency is generated for categorical variables (please see output for details). 
DATA ANALYSIS:
Before training a model to predict the probability of being defaulter, first, the multicollinearity among the variables is explored and 
addressed as its presence could mislead us about the significance of variables present in the model. For this purpose, heatmap and
VIF are used.  Heatmap for continuous variables suggests that variables for amount of bill from April to September are highly correlated.
The variance inflation factor (VIF) of these variables found to have the value of more than 10 (which should be less than 5) so only one
such variable for amount of bill for September is kept in the model while for other months are dropped from the model. Moving forward 
data set was divided into two parts: training set (21000) and test set (9000). The training set is used to train the model, whereas the
test set was used for validating the model. To model the response variable which is categorical with values 0 and 1, the logistic
regression model is used which is based on binary classification and provide detection of payment defaulter where a client can be either
defaulter or not.  Among the independent variables included in the model, variables representing the repayment status are changed into 
binary variables. For this, the level -2, -1, 0 for on time and early payments are coded as 0 and levels greater than 1 for delayed 
payment are coded as 1. In the training set, variables for amount of the given credit, age, repayment status, amount of bill statement,
and amount paid in September and August months are found highly significant. The trained model is found to be a good prediction model 
with sensitivity of 86% along with the specificity of 53.1% after using threshold of 0.3 (please see the confusion matrix below).
The sensitivity and specificity were comparable for other thresholds. The model trained using the training set was validated on the test
set. 
CONFUSION MATRIX FOR TRAINING SET & TEST SET
 
The test set validated the model for its accuracy in predicting defaulter and provided the sensitivity of 87% along with the specificity of 51% at the same threshold of 0.3. The other thresholds, i.e., 0.1 to 0.75 are also used, but the highest sensitivity was observed for 0.3 threshold. For further analysis, I created ROC (Receiver Operating Characteristics) curve (please see the output) by plotting the true positive rate (TPR) against the false positive rate (FPR) at various threshold cutoffs. The area under the ROC curve is 0.76, confirming again that trained model is very good in predicting the defaulters with high sensitivity. I also plotted the lift chart (please see the output) and it shows the likeliness of model to identify more defaulters than a random sample. By using the lift curve, it is found that the model can identify 2 times more defaulters than the random sample even by just using 50% of the data. Due to the presence of a large number of independent variables, model is not provided here (please see the output for estimates), but other than marriage, education and bill amount the parameter estimates of variables are negative and suggest the log odds of being defaulter are decreasing after increasing the independent variable. Therefore, the past six months payments are negatively correlated with the log odds of the defaulter. For bill amount, the odds of being defaulter is increasing for an increase in bill amount. The similar inferences can be made for each of the independent variable. In conclusion, the logistic model suggested here can be used to predict the defaulter with high sensitivity. 
