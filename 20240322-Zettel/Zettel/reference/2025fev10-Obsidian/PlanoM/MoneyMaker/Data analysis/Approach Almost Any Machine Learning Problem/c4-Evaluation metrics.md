understanding what metric to use is the 1st part of the problem

- most common metrics for classification problems:
	- Accuracy
	- Precision (P)
	- Recall (R)
	- F1 score (F1)
	- Area under the ROC (Receiver Operating Characteristic) curve or simply AUC (AUC)
	- Log loss
	- Precision at k (P@k)
	- Average precision at k (AP@k)
	- Mean average precision at k (MAP@k)


- most common metrics to regression problems:
	- Mean absolute error (MAE)
	- Mean squared error (MSE)
	- Root mean squared error (RMSE)
	- Root mean squared logarithmic error (RMSLE)
	- Mean percentage error (MPE)
	- Mean absolute percentage error (MAPE)
	- R2


- start with a simjple problem:
	- binary classification problem
	- suppose a 200 sample: 100 positive and 100 negative
		- 1st step: stratified training and validation set

Tp - true positive
TN - true Negative
FP - False Positive
FN - False Negative

- binary classification metrics for equal number of positives and negatives:
	- accuracy
	- % of right predictions in total set
	- (TP+TN)/ (all samples)
	- it wont be good if target samples are skewed. Example: 180 positives and 20 negatives
		- might get high accuracy even without a model
		- better to look at precision
	- precision
	- TP / (TP + FP)
	- measure ratio of true positives among true and false positives
	- only weighs in the positives 
	- recall 
	- TP/(TP+FN)
	- this model weighs FAlse negatives --> you dont want to say to patientes they dont have the deisease when they have it
	- most models predict a probability
		- threshold is 0.5 --> not always ideal
		- the assumed threshold will affecty precision and recall 
			- precision recall curve
			- high precision relates to a low false positive rate, and high recall relates to a low false negative rate.
	- aim to get precision and recall as close to 1 as possible
	- f1 - harmonic mean of precision and recall 
	- F1 = 2PR / (P+ R)
		- 	combina precision e recall
	- f1 = 2tp / (2tp+fp +fn)
	- perfect prediction model has f1 of 1 ( from 0 to 1)

- other crucial terms:
	- TPR - True Positive Rate == same as recall
	- Tp/(TP + FN)
	- also known as sensitivity
	- FPR - False Positive Rate
	- FP /(TN + FP)
	- TNR - True Negatie Rate
	- 1 - FPR

assume 15 samples with binary target values

the ROC Curve 
	- Receiver Operating Characteristic curve
	- x:FPR (x) y:TPR
	- AUC = the Area under ROC Curve 
		- often used with datasets with skewed binary targets
		- sklearn.metrics.roc_auc_score(ytru,ypre)

- AUC interpretation
	- near extremes --> best
	- if near 1 , its great
	- if near 0, try to use 1-p
	- near middle 0.5 --> your predictions are random
	- example: pneumothorax detection model:
	- say auc = 0.85
	- a positive sample wil rank higher than a negative sample with probab of 0.85

- after Probabs and Auc --> time to make predictions on test set
	- in case of binary classification:
	- could have : Prediction = probab >= threshold ( ==1)

use ROC Curve to choose threshold
	- threshold impacts false positive rate and true positive rate
	- dont want many false positives? have a high threshold ( = more false negatives)
	- vice versa
	- best for skewed binary classification tasks

LogLoss:
	- Log loss = -1.0 * (target * log(prediction) + (1-target) * log(1-prediction) )
	- target is 0 or 1
	- prediction is probab of sample being of class 1
	- for multiple samples:
		- average of all individual log losses
	- logloss punish for being very high probability of very wrong prediction
	- any non-confident prediction wil have very high log loss:
		- example, predict 51% class 1 ( or 49% class 0) --> logloss = 0.67


-  all thode metrics discssed so farcan be converted tyo multiclass classification
	- 3 different ways:
	- macro avewrage: calc precision for allclasses.. then average them
	- micro averaged: calc class tp and fp and calc overall precision
	- weighted precision: same as macro , but weighted by number of items in each class


 the confusion matrixc
	- table of TP, FP, Tn and FN
	- right and wrong classification
	- Sometimes, people also prefer calling FP as Type-I error and FN as Type-II error
	- can be multi-class --> N classes return a xN matrix

-  multi-label classification problem
	each sample has one or more labels in it
	example: objects in a given picture
	- this kind of problem may make use of:
		-  Log loss
		- Precision at k (P@k)
		- Average precision at k (AP@k)
		- Mean average precision at k (MAP@k)

precision at k or P@k
	If you have a list of original classes for a given sample 
	and list of predicted classes for the same, 
	precision is defined as the number of hits in the predicted list 
	considering only top-k predictions, divided by k.

![[Attachments/apk_2.jpg]]

-  log loss for multi-label classification
	- convert targets to binary
	- use log loss for each columns
	- take the avg log loss for each column

------

regression metrics
	- error --> most common and easy to undestand
	- error = predicted value - true value

MAE - Mean absolute error:
	mean of all absolute errors

MSE - Mean Squared Error
	eman of all sqaured errors

RMSE - Square Root of Mean SQuared Error

SLE - Squared Log error
MSLE - Mean Squared Log Error

Percentage Error:
- (predValue - TruValue) /TruValue

 MPE Mean Percentage Error
 - mean of all percent errors

MAPE - Mean Absolute Percentage Error

R2 (R-squared) --> coefficient of determination
	- how good your model fits the data
	- 1.0 means model is a good fit
	- 0 to -1 means bad to absurd predictions
![[Attachments/Pasted image 20220427221709.png]]


Some advanced metrics:
	quadratic weighted Kappa (QWK --> Cohen's kappa)
		measures "agreemetn" between 2 ratings
			ratings = any real number from 0 to N
			"agreement " = how close those ratings are to each other
			high agreement --> closer to 1.0
			low agreement --> closer to 0.0
			in sklearn:
				metrics.cohen_kappa_score(y_true, y_pred, weights="quadratic")
	Matthew’s Correlation Coefficient (MCC)
		![[Attachments/Pasted image 20220427223814.png]]
		uses TP, FP, TN, FN --> good for skewed classes in datasets

when you evaluate unsupervised methods:
	example: clustering
	create or manually label test set
		keep it separated from all in modeling part
	after donbe with clustering --> evaluate test set performance with supervised learning metrics