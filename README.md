# credit-risk-classification
Assignment using various techniques to train and evaluate a model based on loan risk using a dataset of historical lending activity from a peer-to-peer lending services company aiming to build a model identifying creditworthiness of borrowers.

<b>As part of this assign,ent we have been asked to provide a Credit Risk Analysis Report</p>

## Overview of the Analysis

<h2>Explain the purpose of the analysis.</h2>

<p>The purpose of this analysis is to train and evaluate a machine learning model for the purposes of screening the applicants to a lending services company for personel loans. The intention is to identify those applicants at risk of default.</p>

<h2>What financial information has the model used?</h2>

<p>The analysis has used a logistic regression model trained with a dataset with details about past loans. The dataset contains a number of datapoints per loan agreement:<ul><li>
size of loan;</li><li> 
the current interest rate at the time of the loan;</li><li>
the borrower's income;</li><li>
the borrower's total debt;</li><li>
the proprtion of debt to income;</li><li>
marks scored against the application during vetting;</li></ul>
<p>These are the independent variables used to train the model.</p>
<p>Additionally, the loan status (presumably indicating repayment or default) forms the dependent or target variable against which the model is trained.</p>

<<h2>>What is a Linear Regression Model?</h2>
<p>The problem we are trying to solve - whether we can predict if a future loan will be good or bad is a classification problem - the result can only be yes, this loan is high-risk fo default, or no, it is not. Linear regression is designed to deal with classification problems, particularly binary problems such as this with only two results. Logistic regression examines the relationship between the input features (the independent variables outlined above) and the probability of them belonging to a particular class (the dependent varaible). This is achieved by applying a sigmoid function (which produces an 's' shaped curve) to the data set to provide a line seperating the two classes of data (the 'decision boundary') based on the probability of the loan being high-risk or healthy. The result can then be applied to future applications to assess whether they represent a high-risk of default.

<h2>How did we train the model?</h2>

We split dataset into two, one dataset to train the model and one to test it. The training data is used to calculate the best fitting s-shaped boundary between data that is marked as a 1 (a default) or 0 in the "loan staus" column (the dependent variable). In order to calculate the best fitting boundary the regression model will use an optimization algorithm - which is used to 'optimise' the different weightings used for the independent vairables to maximise the accuracy of the classification of the training data. We have a choice of 'optimisation' algorithms, and here we have chosen 'lbfgs' as the preferred method. This is one of a range of algorithms, and the choice depends on a comparison of outcomes - of the methods tested, 'lbfgs' and liblinear' prvided the highest scoring results. We can also seek to limit the number of times that the model will iterate over the data to attempt to adjust the decision boundary to optimise the result. We wnat the data to have learned to distinguish between the good and bad loans, but equally, we do not want the model to have produced a result which has been overfitted to the training dataset - in effect becoming cery good at calculating the probabulity of a bad loan on this dataset.

<h2>How do we test the accuracy of the model?</h2>

We apply the trained model to the test set of data, to monitor how the model performs against a different set of data, where we can measure the result against whether these loans were healthy. The test set is part of the original sample dataset, split from the the training data with a simiLar incidence of good and bad debt. The origianl dataset is roughly 77,500 rows, with the training set forming 75% (58,000 rows), and the remaining 25% producing the test set. Once the model is trained, it can then be used with the test set and we can anayse the results for accuracy. 

<h2>Results and accuracy</h2>

<b>Overfitting</b>


).
