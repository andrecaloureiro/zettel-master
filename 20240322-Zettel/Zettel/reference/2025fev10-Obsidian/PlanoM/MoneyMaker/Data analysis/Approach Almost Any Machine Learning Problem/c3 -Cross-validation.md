Cross-val is a step in the process of building a machine learning model which ensure that our models fit the data accurately and also ensures we do not **overfit**

- example on the red-wine dataset
	- predict wine quality from 0 to 10 from 11 different attributes
	- use hold-out set:
		- for large amount of data
		- time consuming model inference
		- split all rows in a training set and validation set
			- with wine dataset --> 1000 for training and 599 for validation

overfitting concept:
	ML model and hyperparameter tuning:
		improves with training model
		but doenst improve on test data

overfitting concept 2:
	test loss increases and training loss decreases
	common in neural networks

STOP TRAINING WHEN VALIDATION LOSS IS AT MINIMUM

**Occam's razor** --> simplest solutions are the ones most generalizable
	if your model does not obey Occam's razor --> probably overfitting

![[Attachments/Pasted image 20220425231612.png]]

- cross val techinqiues:
	- hold-out set
	- k-fold cross val
		- divide in k parts
		- each part will be labeled ( train and validation set... possible to use a test set also)
		- ![[Attachments/Pasted image 20220425232147.png]]
		- use KFold from Scikit-learn --> each sample has a value of 0 to k-1
	- stratified k-fold cross-val
		- used with skewed datasets. Example: 90% positive samples and 10% negative samples
		- simple k-fold can result in all negative samples --> stratified keeps proportions --> each fold will reproduce ratio of main fold
		- modify KFold code:
			- model_selection.StratifiedKFold
			- kf.split(...) --> specify target column to stratify ( assuming there is a target column and its a classification problem)
			-  CHOOSE STRATIFIERD KFOLD BLINDLY , if dealing with classification problem
	- hold-out based valid
		- for bigger datasets: example: 1Million rows --> example create 10 folds and keep one out as test
		- very much used in time-series data
			- example: predict 2020 sales from 2015-2019 history --> train with 2015-2018 and hold out 2019
	- leave-one-out crossval
		- kfold = N ( N is the number of samples in dataset)
		- 1 is left out for validation
		- better for small datasets
	- group k-fold crossval
		- sklearn's GroupKFold
		- to ensure that instances in training data do not appear in validation data
		- prevent data leakage
		- cant combine stratKfold with GroupKfold
		- **practical exercise to try**

- for regression problems --> simple kfold cross val
	- if target distro is not consistent: 
		- 1st divide target into bins,
			if lots of samples: (>10k, >100k): just dividie into 10 or 20 bins
			if few samples: use simple rule like **Sturge's Rule**  to get appropriate num of bins:
				number of bins = **1+log2(N)** ( N is number of samples in dataset)

	