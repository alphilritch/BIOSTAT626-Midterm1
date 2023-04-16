# BIOSTAT626-Midterm1
All the code and the final results can be seen in this repository. The results can be repeated completely by the code.
Original Data Source: https://github.com/xqwen/bios626/tree/main/data

Environment: RStudio 2023.03.0+386 "Cherry Blossom" Release (3c53477afb13ab959aeb5b34df1f10c237b256c3, 2023-03-09) for Windows
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) RStudio/2023.03.0+386 Chrome/108.0.5359.179 Electron/22.0.3 Safari/537.36

Instructions:
Run all the R code. Because some possible problems about the environment, one can ignore the part which cannot run correctly and simply go on with next part.
Please note that the address of the data in the code should be changed to work in other environments.

Binary classification:
Run BIOSTAT626 Midterm1 binary.Rmd till we get binary_3712.txt. 

Multiclass:
1. GLM method
Run BIOSTAT626 Midterm1 binary.Rmd till we get multi_3712.txt. In the remaining part of the code, I have made some tests on multiclass.
2. Random Forest Method
Run multiclass test.Rmd tll we get multiclass_itriedmybest.txt.
3. SVM
Run multiclass test svm.Rmd till we get multiclass_3712death.txt.
4. Other tests
See the ut2.Rmd, which is not good enough to produce a result.

Detailed Answers of the Problem Set:
1. Complete the Task 1 and 2 and submit your classification results via Canvas. 
2. Set up a Github repository and upload all your code used for training, evaluation, and generating results of test data. Provide the url to your Github repository as the answer to this question.
URL:
https://github.com/alphilritch/BIOSTAT626-Midterm1

3. Write a text file (name the file “README.md”) to provide necessary instructions, so that other people can reproduce all your results.
See the README.md in the URL above.

4. Describe your baseline algorithm and provide necessary tables and/or figures to summarize its performance based on the training data.
Our goal is to build a binary classifier model using logistic regression to predict the binaryclass variable based on the 561 parameter values present in the training dataset. The binaryclass variable is created from the original activity variable where values less than or equal to 3 are classified as 1 and values greater than 3 are classified as 0.
The training dataset is read in from the "training_data.txt" file located in the "E://Desktop//Biostat 626//Midterm1" directory and stored in a dataframe called "my_data". The first few rows of the "my_data" dataframe are printed to verify that it was read in correctly. The binaryclass variable is created using a for loop that iterates through each row of the "my_data" dataframe and assigns a value of 1 or 0 to the binaryclass variable based on the activity value. The resulting dataframe is then stored in a new dataframe called "training_data".
A logistic regression model is fit to the "training_data" dataframe using the glm() function with binaryclass as the dependent variable and all the other variables as independent variables. The resulting model is stored in an object called "fit.logit". A summary of the model is printed to the console.
The test dataset is read in from the "test_data.txt" file located in the same directory as the training dataset. The first few rows of the "test_data" dataframe are printed to verify that it was read in correctly.
The "predict()" function is used to generate the predicted probabilities of binaryclass values for the test dataset using the logistic regression model "fit.logit". The resulting probabilities are converted to integer values using the "as.integer()" function and rounded to the nearest integer using the "round()" function. The resulting integer values are stored in an object called "output1". The "write.table()" function is used to write the "output1" object to a file called "binary_3712.txt" with no row or column names.
As for the baseline algorithm, it appears to be a simple logistic regression model with no additional feature engineering or model tuning. The performance of the model based on the training data can be summarized using the summary() function on the "fit.logit" object, which provides information on the coefficients, standard errors, z-values, and p-values of the model.
Fig 1. Summary of baseline algorithm
 
Fig 2. Deviance and AIC of binary classification
 

5. Describe your final algorithm and provide necessary tables and/or figures to summarize its performance based on the training data.
The code for multiclass is training a random forest model to predict the multiclass activity level of a subject based on a set of 561 parameters. The first part of the code loads necessary packages, reads in the training and test data, and preprocesses the training data by converting the activity variable into a multiclass variable.
The second part of the code sets up cross-validation and control parameters, trains the model using the random forest method with 100 trees, and makes predictions on the test data. The predictions are rounded to the nearest integer, and any values greater than or equal to 7 are set to 7. The predicted values are then written to a file called "multi_3712.txt".
The third part of the code sets up different cross-validation and control parameters, trains a new random forest model with 150 trees, and makes predictions on the test data. The predictions are rounded to the nearest integer, and any values greater than or equal to 7 are set to 7. The predicted values are then written to a file called "multiclass_itriedmybest.txt".

To evaluate the performance of the model, cross-validation is used with 5 and 15 folds respectively. The model's performance is summarized using a confusion matrix, which shows the number of correctly and incorrectly predicted values for each class. Additional performance metrics such as accuracy, sensitivity, specificity, and precision can also be calculated.
About GLM method, the summary can be seen below:
Fig 3. Summary of multiclass
 
Fig 4. Deviance and AIC of multiclass
 

6. Use a figure or a table to show your leaderboard performance. Describe your efforts to improve the performance.
Table 1. Leaderboard performance
Accuracy	03/28	03/31	04/04	04/07	04/11	04/14
Binary	1.000	1.000	1.000	1.000	1.000	1.000
Multiclass	Unpublished	0.767	0.883	0.890	0.890	0.592
For the binary classification, I have made a nearly perfect result at the first try, which can reach 100% accuracy of the test data. So I did not revise it in the later submissions.
For the Multiclass part, in the 03/28 version, I used the GLM method but submitted the file with wrong name. In 03/31 version, I made a little improvement on 03/28 version. It is still based on General Linear Regression, but I made a calibration according to the binary classification result. For example, if the binary result of one sample is static, while the multiclass result belongs to one of motion status, it will be round up or down to the corresponding status.
In the 04/04, 04/07, 04/11 versions, I used the Random Forest method. It is really time consuming so I made improvements mainly by adjusting the parameters. As the number of trees and cross validation affect the final result, I increase the cv and trees number gradually in order to improve the performance. But in 04/07 version(cv=5, ntree=100) and 04/11 version(cv=15, ntree=150), the accuracy remain the same. So I consider it reaches its upper limit.
In the 04/14 version, I tried another different method, i.e. Support Vector Machine(SVM). But it does not work very well according to the accuracy performance of the test data. I think the problem is probably generated from the parameter choice in the svm model. I made some improvements in the final code but did not test it with leaderboard.

7. Comment on your final results and potential ways to further improve the classification accuracy.
As for me, my final result of binary classification is great. Because the method is easy and convenient to fulfill. And its running time is not too long. The accuracy of it on test dataset is 1.000. So I consider it as a general way to judge the status of samples which can be applied to other dataset with the same parameters.
For the multiclass classification, I have tried different ways including general linear regression, Random Forest and Support Vector Machine(SVM) to fulfill the function. But I must admit that the accuracy is not very satisfactory.
First, the General Linear Regression is limited to some specific distributions. I used Poisson distribution to simulate multinomial distribution. But even if after some hand-put calibration, the result is up to 0.767. I think there may be other R packages and functions more suitable for multinomial distribution but I did not figure it out.
After that, I tried Random Forest method. I think increasing the number of trees and cross-validation will help to improve the performance. But as it is really time consuming, maybe I need more advanced device to tackle with it.
About the code I have done using SVM, it need more practice to find appropriate value for gamma and cost. As I have tested, a higher cost and a lower gamma may be helpful. Svm_tune() may give out some useful information. Using new parameters, it is possible to reach a higher accuracy.
