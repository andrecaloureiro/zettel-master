- What are categorical variables?
	- major types:
		- nominal
			- no order
			- 2 or more
				- binary: if only 2 categories
				- cyclic: present in cycles: ex: day of the week or hours in a day
			- example: gender or neighboorhood
		- ordinal
			- levels in a particular order
			- ex: low, medium, high

- this chaptyer uses kaggle competition data: cat-in-the-dat-ii
	- Start checking0 target skewness
		- dataset skewed --> use AUC (Area under ROC Curve, )
			- or use precision and recall (AUC incorporates both)
	- Overall, there are:
			- Five binary variables(bin_0 to 6)
			- Ten nominal variables(nom_0 to 9
			- Six ordinal variables(ord_0 to 5)
			- Two cyclic variables(day, month)
			- And a target variable (target)
	- apply numerical encoding method: 
	- 1st method -- mapping categories using a dictionary
		- convert to numbers starting from 0 to N-1 ( N is total number of categories)
		- also function of sklearn.preperocessing. LabelEncoder()
			- LabelEncoder() cant hadnddle NaN values
				- fillna('NONE')
		- models that can use this:
			- Decision trees 
			- Random forest
			- Extra Trees 
			- any kind of boosted trees model
				- XGBoost
				- GBM
				- LightGBM
		- modelos that cant use this:
			- Support vector machines, linear models or neural networks
			- those expect data to be normalized/ standardized
				- must binarize the data (2nd and 3rd method)
	- 2nd method) convert to decimal --> convert to binary
						- Example:
							- Freezing --> 0 --> 0 0 0 
							- Warm --> 1 --> 0 0 1 
							- Cold --> 2 --> 0 1 0 
							- Boiling Hot --> 3 --> 0 1 1 
							- Hot --> 4 --> 1 0 0 
							- Lava Hot --> 5 --> 1 0 1
						- sparse format --> store only values that matters (1's)
							- example:
								- ![[Attachments/Pasted image 20220429155811.png]] occupies all slots ina 3x3 table --> uses 9 x 8bytes = 72 bytes
								- this dictionary has same info and occupies only 4x8 = 32 bytes:
									- (0, 2) 1 
									- (1, 0) 1 
									- (2, 0) 1 
									- (2, 2) 1
	- 3rd method) One Hot Encoding
						- binary encoding --> not a binary representation
						- N columns are made ( N is the number of different categories)
						- vector (row) size N, only one 1  , rest all other values are 0s

- those 3 methods are the most important ways of handling categorical data:

- other ways can be used:
	- Example: check how many ids there are for ord_2 == 'Boiling Hot'
		- you can also use category count as reference:
			- check how many instances per category
			- use count() method to assign new value to ord_2
		- you can also use 2+ features as count code:


- Create new features from these combinations ( NaN will also convert as string)

- Whenever you get categorical features:
	- fill NaN
		- drop them --> not the best
		- preferred --> treat them as category, assgin ('none')
	- convert them to integers ( LabelEncoder or mapping)
	- create one hot encoding
	- go for modelling

- production problem: What if an unkonwn categories come during live executioon?
	- model will give an error
	- you can try using nearest neighbour to fit the other categories
	- you can selecty the feature/s more prone to have new values and not train omdel with this feature
	- you can fit your model using the feature categories of the test set
		- may it overfit? not if crossvalidation is ok
		- ![[Attachments/Pasted image 20220501201834.png]]
	- any new catyegories in live production mnay be trated as "NONE"
		- natural language processing works and expands this way
		- by adaptaing the NONE category
	- RARE categories may be given a threshold to be considered so

- 2 models were trained --> logistic regression ( using OHE for categorical) and random forest, using label Encoder()
	- the simples ( log reg ) performed best
	- also tried ranfom forestr using OHE -> SVD
		- very time and memory consuming
	- also tried XGBoost

--> new experiment on USCensus Dataset
- drop numerical columns
- start making the cross validation folds]
- apply OHe + log regression
- REMEMBER: 
	- tree based models: no need to normalize data
	- linear models --> vital to normalize
- final feature matrix has:
	- numerical columns as is
	- encoded categ columns
	- any tree based can handle


- trying some feature engineering

- target encoding method
	- careful : too prone to overfit
		- use some smoothing or add noise


- entity embbeding 
	- categories as vectors
		- binarization
		- one hot encode
	- if tens of thousands of categories --> use float values , instead