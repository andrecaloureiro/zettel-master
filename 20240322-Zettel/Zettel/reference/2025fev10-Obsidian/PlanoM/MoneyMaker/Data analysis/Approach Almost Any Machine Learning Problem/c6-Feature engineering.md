#datascience #Mental 
 
 - one of the most crucial parts of building a good ML model
 - many situations where you avoid complicated, large models
	 - use simple models with engineered features
 - done best when having domain knowledge
- involves:
	- creating new features from data
	- different types of normalization and transformation
	- convert categorical to counts
	- target encoding
	- using embedddings

- ALWAYS REMEMBER: NO NEED TYO IMPUTE VALUES FOR TREE BASED MODELS --> THEY HANDLE IT THEMSELVES

- this chapter will be limited to
	- num variables
	- combo of num and categorical

- one of the most simple and most widely used: datetime
	- can originate feats like:
		- Year 
		- Week of year 
		- Month 
		- Day of week 
		- Weekend 
		- Hour 
		- And many more

- using aggregates in pandas
	- ex: ![[Attachments/Pasted image 20220502152938.png]]
	- ![[Attachments/Pasted image 20220502153001.png]]
	- example of aggreagtes:
		- Mean, Max, Min
		- Unique, Skew, Kurtosis
		- Kstat, Percentile, Quantile
		- Peak to peak, And many more

- using TSfresh l,ibrary for time-series data
- using sklearn.preprocessing.PolynomialFeatures()

- binning numerical features

- high variance can be reduced using log transformation
	- ex: ![[Attachments/Pasted image 20220502160452.png]]
	- df.f_3.var() = 8077265.875858586
	- : df.f_3.apply(lambda x: np.log(1 + x)).var() = 0.6058771732119975

- most of the time, those features are created out of intuition
	- if an industry, industry specific features

- feature enginneering also about habndling NaN
	- if you ever encounter missing values--> treat as new category
		- label as NONE
		- if numerical: use 0... or better yet, use mean()
		- using a k-nearest neighbour imputer
			- Sklearn KNNImputer
		- using a regression model that tries to predict missing value based on other columns
		- 

