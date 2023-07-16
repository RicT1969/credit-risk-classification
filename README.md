# Credit-Risk-Classification
Assignment using various techniques to train and evaluate a model based on loan risk using a dataset of historical lending activity from a peer-to-peer lending services company aiming to build a model identifying the creditworthiness of borrowers.

<b>As part of this assignment we have been asked to provide a Credit Risk Analysis Report</b>

# Credit Risk Analysis Report

<h2>The purpose of the analysis.</h2>

<p>The purpose of this analysis is to train and evaluate a machine learning model for the purposes of screening the applicants to a lending services company for personel loans. The intention is to identify those applicants at risk of default.</p>

<h2>What financial information has the model used?</h2>

<p>The model is a logistic regression model trained with a dataset of details about past loans. The dataset contains the following data per loan agreement:<ul><li>
size of loan;</li><li> 
the current interest rate at the time of the loan;</li><li>
the borrower's income;</li><li>
the borrower's total debt;</li><li>
the proprtion of debt to income;</li><li>
marks scored against the application during vetting;</li></ul>
<p>These are the independent variables used to train the model.</p>
<p>Additionally, the loan status (presumably indicating repayment or default) is the dependent or target variable against which the model is trained and which, should the model be deployed, is the element we are trying to predict.</p>

<h2>What is a Linear Regression Model?</h2>

<p>The problem we are trying to solve - whether we can predict if a future loan will be good or bad -  is a classification problem with a binary result: yes, this loan is a high-risk of default;no, it is not. Linear regression is designed to deal with classification problems, particularly binary problems such as this. Logistic regression examines the relationship between the input features (the independent variables outlined above) and the probability of them belonging to a particular class (the dependent varaible). This is achieved by applying a sigmoid function (which produces an 's' shaped curve) to the data set to provide a line seperating the two classes of data (the 'decision boundary') based on the probability of the loan being a 1 (high-risk) or 0 (healthy). The model can then be applied to future applications to assess if they represent a high-risk of default.</p>

<h2>How do we train the model?</h2>

<p>We split the data set into two subsets: one to train the model and the other to test it. The split is 75:25 between the two, preserving the balance of classes within the original data. Once the model is trained, it can then be used with the test set and we can analyse the results for accuracy. The training data is used to calculate the best fitting s-shaped boundary between data that is marked as 1 (a default) or 0 (non-default) in the target variable. To calculate the best fitting boundary, the regression model uses an optimisation algorithm - which is used to 'optimise' the different weightings used for the vairables to maximise the accuracy of the classification of the training data. We have a choice of 'optimisation' algorithms, and we have chosen 'lbfgs' as the preferred method. This is one of a range of algorithms, and the choice depends on a comparison of outcomes. Of the methods tested, 'lbfgs' and liblinear' provided the highest scoring results. We can also seek to limit the number of times that the model will iterate over the data to attempt to adjust the decision boundary to optimise the result. We want the data to have learned to distinguish between the good and bad loans, but we do not want the model to have produced a result which has been overfitted; becoming specialised in classifying the training data, but not generalised enough to deal with variations in other unseen datasets. Here we have not defined a maximum.</p>

<h2>How do we test the accuracy of the model?</h2>

<p>We apply the trained model to the test set of data and compare the predicted results against the actual instances of good loana and defaults.</p>

<h2>Results and accuracy</h2>

<p>Which measures are likely to be the most relevant depends on the purpose of the model and any issues that exist with the training data. The lending company wishes to identify borrowers who have a high probability of default. The measures most relevant are those that indicate how well the model has correctly identified bad debtors, as opposed to false positives (good debtors incorrectly classified as bad) and false negatives (bad debtors incorrectly identified as good). The measures of greatest relevance are recall and precision.</p><ol>

<li>Recall:</li><ul>

<li>Recall is the number of true positive predictions divided by the total number of actual positive instances in the data. It measures the model's ability correctly to capture positive instances. Maximising recall is more important to the use case as we wish to minimise the misclassification of high-risk applicants.</li>
<li>In the case of the good loans, the ratio is approximately 100%, which is not surprising given the significant class imbalance.</li>
<li>For the high-risk loans this ratio equals 89%, meaning that the model has misclassified bad loans in 11% of instances. This represents a good outcome, potentially screening out 89% of future loans with a high-risk of default. The orginal data set of 77,500 applications had 2,500 identified defaults. If this model were applied than it would have reduced that number to approximately 275. It could therefore represent a significant improvement to the current screening and a significant saving to the lending company.</li></ul>

<li>Precision:</li><ul>

<li>Precision is the number of true positive predictions divided by the total number of positive predictions made by the model, measuring the model's ability to identify positive instances correctly. This measure is useful in looking at the ability of the model to minimise false positives, i.e. misclassifying good loans, so potentially excluding good investments.</li>
<li>In predicting good loans the model's precision is again almost 100%; however, as observed, this is subject to the significant class imbalance in the dataset.</li> 
<li>The proportion of bad loans detected out of the entire instance of bad loans is 87%. This is a positive indication that the model is accurate.</li></ul>

<li>Accuracy:</li><ul>

<li>Accuracy is the proportion of correct predictions (true positives and true negatives) over total predictions.</li>
<il>In relation to the its ability to predict whether a loan is good or bad, the score is 99%, meaning that in 99% of cases the model has predicted the correct outcome</li>
<li>Whilst this appears to be an extremely good score, we are dealing with a highly imbalanced dataset. The accuracy measure is very sensitive to imbalance, and in this case, where the minority class (the high risk loans) is such a small proportion of the total, the accuracy measure will be heavily skewed by the majority class.</li>
<li>Given the use case for this model, the accuracy measure is not a useful gauge for assessing the model's results and we should place greater relaince on precision and recall (which will be less effected by calss imbalance).</ol></ul>


<h2>Issues</h2><ol>

<li>Imbalance</li><ul>
<li>The dataset is highly imnbalanced with a significantly larger number of non-default instances (class 0) compared to default instances (class 1). This class imbalance can have implications for model evaluation and potential concerns regarding overfitting. The 'defaults' class of loans forms only 3% of the total records (which is similarly represented in both training and test data).</li>
<li>The imbalance may mean that the performance metrics are misleading or skewed. For this reason the measure of "accuracy" is not useful.</li>
<li>There are several risks associated with an imbalanced dataset:<ul>
<li>The model might focus on predicting the majority class (the healthy loans) resulting in a higher number of false negatives and a lower recall for the defaults;</li>
<li>the risk of overfitting the majority class leading to the model being less able to predict instances of the bad loans.</li></ul>
<li>the model should undergo further training on sample sets with a greater number of defaulting loans for further evaluation. Although we can expect a much smaller number of defaulting loans in any sample, given that applications are already screened, consideration should be given to using techniques that can help address the risks of an imbalanced dataset.</li></ul>

<li>Overfitting</li><ul>
<li>Overfitting occurs when a model becomes too specialized in the training data and fails to generalize well to new, unseen data.</li>
<li>I have also produced a classification report for the training data within the code to see whether there are any obvious signs of overfitting. The training results are comparable to the test data results, with no indication that the model has been overfitted (recall for default loans is 89% and precision is 85%). Notably recall and precision are less sensitive to class imbalance, but this would still not pick up any overfitting of the majority class.</li>
<li>Despite the fact that the metrics do not suggest that the model is overfitted, the imbalance between the classes means that the model may be biased towards predicting the majority class correctly. It may not pay sufficient attention to the minority class, resulting in lower recall (sensitivity) for the minority class, leading to a higher number of false negatives.</li></ul></ol>

<h2>Summary</h2><ul>

<li>The model has performed well in predicting high-risk loans in the test data, with a high degree of recall and precision. The model shows promise of producing a much more effective screening process than currently employed by the lending servicescompany.</li>
<li>The greatest concern in evaluating the model is the class imbalance between non-default instances (class 0) compared to default instances (class 1). the default instances form aproximately 3% of the total dataset. There is a risk that this will have skewed the results of the model, which is potentially overfitted to the majority class and that it is biased towards predicting the majority class correctly leading to a higher number of false negatives in for the minority class</li>
<li>If the class imbalance is causing overfitting and impacting the ability of the model to predict instances of the minoirty class accurately, then this will impact the appropriateness of the model given that its purpose is to identify potentially high-risk loans.
<li>In order to mitigate this risk a number of steps are recommmended:</li><ol>
<li>Resampling - employ resampling techniques such as oversampling the minority class (e.g., SMOTE) or undersampling the majority class. These techniques can help balance the dataset and mitigate the bias towards the majority class.</li>
<li>Class weighting, forcing the model to give greater representation to instances of default.</li>
<li>Consider alternative classification algorithms or techniques designed to handle imbalanced data, such as ensemble methods like Random Forest</li>
<li>Utilise cross-validation in conjunction with resampling to test the accuracy of the model. This involves splitting the dataset up into a number of equally sized samples (or folds). Each sample containing a balanced representation of the target variable's classes. The purpose is to  train the model on one fold and test it against the remainder. This process is repeated with each fold being used as a training set and then validated against the rest of the folds. This allows us to aggregate the model's performance metrics to assess its ability to generalise.</li>




