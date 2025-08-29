- what are hyperparameters?
	- parameters that control fitting/training process of the model
	-  ex: train a linear regression with SGD:
		- parameters: slope and bias
		- hyperparameter: learning_rate
	- the best hyperparam combo will give the best results
		- check with metrics

- there are inifinite  hyperparam combinations:
	- ex: sklearn.ensemble.RandomForestClassifier()
		- n_estimators=100, criterion='gini', max_depth=None, min_samples_split=2, min_samples_leaf=1, min_weight_fraction_leaf=0.0, max_features='auto', max_leaf_nodes=None, min_impurity_decrease=0.0, min_impurity_split=None, bootstrap=True, oob_score=False, n_jobs=None, random_state=None, verbose=0, warm_start=False, class_weight=None, ccp_alpha=0.0, max_samples=None,
		- 19 parameters
- best to find combinations using grid Search
	- ex:
		- n_estimators can be 100, 200, 250, 300, 400, 500;
		- max_depth can be 1, 2, 5, 7, 11, 15 
		- and criterion can be gini or entropy.
	- not very popular due to computational demand
		- even more if there is crossval
	- an example is given with a mobile phone price prediction
		- 20 features

- next best is random SearchCV
	- random select parameters combo and calculate crossval score
	- less time consumed (just depends on how many times you eval your model)
	- code is almost the same as GridSearch

- sometimes you may need a pipeline
	- ex: training data = 2 columns --> build a model to predict class
	- assume following pipeline:
		- tf-idf semisupervised
		- use Single Vector decomposition ( SVD ) with support vector machine classifier
			- select components of SVD
			- tune parameters of SVM

- advanced hyperparam optimization techs?:
	- minimization of functions
		- downhill simplex algorithms --> c11 -ensemble chapter
		- Nelder-Mead optimization --> c11 -ensemble chapter
		- Bayesian tech with Gaussian Processfor best hyperparam
			- scikit-optimize ( skopt) library

- libraries for hyper param optimization
	- scikit-optimize ( skopt)
	- hyperopt
		- uses Tree-structured Parzen Estimator(TPE)

- those ways are the most common for hyper-param tuning:
	- work with almost all models:
		- : linear regression, logistic regression, tree-based methods, gradient boosting models such as xgboost, lightgbm, and even neural networks!
	- start tuning hyper param by hand (manually)
		- if you get good here--> may not even need automated HPT
	- avoid overfitting by 
		- introducing noise to the data
		- penalizing cost function:
			- L1 - Lasso regression
			- L2 - Ridge Regression
		- if neural networks:
			- use dropouts
			- add augmentations, noise etc