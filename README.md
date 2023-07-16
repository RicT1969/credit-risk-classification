# credit-risk-classification
Assignment using various techniques to train and evaluate a model based on loan risk using a dataset of historical lending activity from a peer-to-peer lending services company aiming to build a model identifying creditworthiness of borrowers.

<b>As part of this assign,ent we have been asked to provide a Credit Risk Analysis Report</p>

## Credit Risk Analysis Report

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
<p>Additionally, the loan status (presumably indicating repayment or default) is the dependent or target variable against which the model is trained and which, should the model be deployed, is the element we are trying to predict.</p>

<h2>>What is a Linear Regression Model?</h2>

<p>The problem we are trying to solve - whether we can predict if a future loan will be good or bad is a classification problem - the result can only be yes, this loan is high-risk fo default, or no, it is not. Linear regression is designed to deal with classification problems, particularly binary problems such as this with only two results. Logistic regression examines the relationship between the input features (the independent variables outlined above) and the probability of them belonging to a particular class (the dependent varaible). This is achieved by applying a sigmoid function (which produces an 's' shaped curve) to the data set to provide a line seperating the two classes of data (the 'decision boundary') based on the probability of the loan being high-risk or healthy. The result can then be applied to future applications to assess whether they represent a high-risk of default.</p>

<h2>How do we train the model?</h2>

We split dataset into two, one dataset to train the model and one to test it. The training data is used to calculate the best fitting s-shaped boundary between data that is marked as a 1 (a default) or 0 in the "loan staus" column (the dependent variable). In order to calculate the best fitting boundary the regression model will use an optimization algorithm - which is used to 'optimise' the different weightings used for the independent vairables to maximise the accuracy of the classification of the training data. We have a choice of 'optimisation' algorithms, and here we have chosen 'lbfgs' as the preferred method. This is one of a range of algorithms, and the choice depends on a comparison of outcomes - of the methods tested, 'lbfgs' and liblinear' prvided the highest scoring results. We can also seek to limit the number of times that the model will iterate over the data to attempt to adjust the decision boundary to optimise the result. We want the data to have learned to distinguish between the good and bad loans, but equally, we do not want the model to have produced a result which has been overfitted to the training dataset - in effect becoming specialised in classifying this set of data, but poor at classifying other unseen sets because the model is not generalised enough to deal with variations.

<h2>How do we test the accuracy of the model?</h2>

We apply the trained model to the test set of data, to monitor how the model performs against a different set of data, where we can measure the result against whether these loans were healthy. The test set is part of the original sample dataset, split from the the training data with a simiLar incidence of good and bad debt. The origianl dataset is roughly 77,500 rows, with the training set forming 75% (58,000 rows), and the remaining 25% producing the test set. Once the model is trained, it can then be used with the test set and we can anayse the results for accuracy. 

<h2>Results and accuracy</h2>

<p>We have used a number of measures of accuracy. Which measures are likely to be the most relevant depends on the purpose of the model and the issues we may have with the training data. The credit company wishes to identify borrowers who have a high probability of default. The measures most relevant are those that indicate how well the model has correctly identified bad debtors, as opposed to false positives (good debtors incorrectly classified as bad) and false negatives (bad debtors incorrectly identified as good). The measures of greatest relevance are recall and precision.<ol>

<li>Recall:</li><ul>

<li>Recall is the number of true positive predictions divided by the total number of actual positive instances in the data. It measures the model's ability correctly to capture positive instances. Maximising recall is important hre, as it is more important to the use case that the model does not miss potential high-risk applicants.</li>
<li>In the case of the good loans, the ratio is approximately 100%, which is not surprising given that the data has a significant class imbalance where the total of good loans outnumbers bad loans.</li>
<li>In the case of the high-risk loans this ratio equals 89%, meaning that the model has incorrectly classified bad loans as good 11% of the time. This represents a good outcome, potentially screening out 89% of future loans with a high-risk of default. The orginal data set of 77,500 applications had 2,500 identified defaults. If this model were applied than it would have reduced that number to approximately 275. It could therefore represent a significant improvement to the loan company'sscreening and a significant saving.</li></ul>

<li>Presicion:</li><ul>

<li>Precision is the number of true positive predictions divided by the total number of positive predictions made by the model, measuring the model's ability to identify positive instances correctly. This measure is useful in looking at the ability of the model to minimise false positives, that is classifying good loans as bad, so potentially excluding good investments for the loan company</li>
<li>In predicting good loans the model's precision is again almost 100%; however, as observed, this is subject to the significant class imbalance that exists within the dataset.</li> 
<li>The proportion of bad loans detected out of the entire instance of bad loans is 87%. This is a positive indication that the model is accurate.</li></ul></ol>

<h2>Issues</h2><ol>

<li>Imbalance</li><ul>
<li>The dataset is highly imnbalanced with a significantly larger number of non-default instances (class 0) compared to default instances (class 1). This class imbalance can have implications for model evaluation and potential concerns regarding overfitting. The 'defaults' class of loans forms 3% of the total records (which is similarly represented in both the training and test data).</li>
<li>The imbalance may mean that the performance metrics are misleading or skewed.</li>
<li>There are several risks associated with an imbalanced dataset, in particular the model might focus on predicting the majority class (the healthy loans) resulting in a higher number of false negatives and a lower recall for the bad loans. There is also a risk of overfitting the majority class, having learned the patterns within the data for the healthy loans, leading to the model being less able to predict instances of the bad loans.</li>
<li>the model should undergo further training on sample sets with a greater number of defaulting loans for further evaluation. Although we can expect a much smaller number of defaulting loans in any sample, given that applications are already screened, consideration should be given to using techniques that can help address the risks of an imbalanced dataset - we could resample the dataset, producing an oversample of the bad debts compared to the majority set, or employ class weighting, to force the model to attach greater importance to occurrences of the minority class. </li></ul>

<li>Overfitting</li><ul>
<li>Overfitting occurs when a model becomes too specialized in the training data and fails to generalize well to new, unseen data.</li>
<li>To examine whether there are any clear indications of overfitting I have also produced a classification report for the training data. This is comparable with the test data results, with no indication that the model has performed better at predicting the training set of results compared to the test data (recall for the deault loans is 89% and precision is 85%).</li>
<li>Despite the fact that the metrics do not suggest that the model is overfitted, because the majority class has a higher number of instances, the model may be biased towards predicting the majority class correctly. It may not pay sufficient attention to the minority class, resulting in lower recall (sensitivity) for the minority class, leading to a higher number of false negatives.</li></ul></ol>

<h2>Summary</h2><ul>

<li>The model has performed well in predicting high-risk loans in the test data, with a high degree of recall and precision. The model therefore shows promise of producing a much more effective screening process than currently employed by the lending servicescompany.</li>
<li>The greatest concern in evaluating the model is the class imbalance between non-default instances (class 0) compared to default instances (class 1). the defualt instances form aproximately 3% of the total dataset. There is a risk that this willhave skewed the results of the model, which is potentially overfitted to the majority class meaining that it is biased towards predicting the majority class correctly leading to a higher number of false negatives in for the minority class</li>
<li>If the class imbalance is causing overfitting and impacting the ability of the model to predict instances of the minoirty class accurately, then this will impact the appropriateness of the model given that its purpose is to identify potentially high-risk loans.
<li>In order to mitigate this risk a number of steps are recommmended:</li><ol>
<li>Resampling - employ resampling techniques such as oversampling the minority class (e.g., SMOTE) or undersampling the majority class. These techniques can help balance the dataset and mitigate the bias towards the majority class.</li>
<li>Consider alternative classification algorithms or techniques designed to handle imbalanced data, such as ensemble methods like Random Forest</li>
<li>Utilise cross-validation in conjunction with resampling to test the accuracy of the model. This involves splitting the dataset up into a number of equally sized samples (or folds). Each sample containing a balanced representation of the target variable's classes. We can then train the mdoel on one fold and test it against the remainder. This is repeated with each fold being used as a training set and then validated against the rest of the folds which serve as a training set. This will allow us to aggregate the model's performance metrics to assess its ability to generalise.</li>




