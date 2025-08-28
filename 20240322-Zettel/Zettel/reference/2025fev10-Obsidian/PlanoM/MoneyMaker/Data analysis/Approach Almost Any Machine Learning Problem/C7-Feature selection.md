- after creating features, it's time to select a few of them
	- too many features = curse of dimensionality
	- more features demands more training samples
	- "a lot" is subjective and depends on
		- model validation
		- time to train models

- simplest selection:
	- remove feats with very low variance
		- variance depends on scaling of data
		- sklearn's feature_selection.VarianceThreshold
	- remove those with high correlation
		- numerical

- Univariate Feature Selection
	- Score each feature against given target
	- Methods:
		- Mutual Information
		- ANOVA
		- F-test
		- chi^2 --> only for non-negative data
	- sklearns methods:
		- SelectKBest --> keeps top-k scoring features
		- SelectPercentile --> keeps top features ina percentage specified by user
	- better to focus on less and important features

- Using machine Learning Model for selection:
	- simplest form: greedy feat selection
		- 1st step: choose a model
		- 2nd step: choose loss/scoring fucntion
		- 3rd step: evaluate each feature and get in list of "good" features if it iumproves score/loss
		- high computational cost
		- bad implementation may overfit the model
		- ![[Attachments/Pasted image 20220503105118.png]]
		- previous graph shows how AUC ROC Score improves over each iteration

- RFE Recursive Feature Elimination
	- another greedy approach
	- each iteration remove feature with least ikmportance or coeff close to 0
	- sklearns.feature_selection.RFE

- feature coefficients or importance of features
	- fit the data to the model, select a coeff thresholod and keep what is above bar
	- can choose features from one model and choose another model to train
		- ex: use LogRegression to seelct features and RandomForest to train
		- sklearn's SelectFromModel class --> helps choose features directly from given model
			- set threshold for coefficients/feat importance
			- set max number of features

- L1 (Lassso ) penalization
	- most coeffs will be zero or close to zero
	- select feats with non-zero coeffs