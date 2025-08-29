https://www.kaggle.com/alexisbcook/introduction

--> improve model quality
-->< handle categorical var and missing values
--> cross-validation for model validation
--> use XGBoost to enhance models
--> avoid data leakage
--> pipelines to improve MachLearn code

--> data from kaggle [Melbourne Housing prices competition](https://www.kaggle.com/c/home-data-for-ml-course)


https://www.kaggle.com/alexisbcook/missing-values

--> 3 approaches to deal with missing values

- 1st option : drop columns with missing values
- 2nd option ( better): imputaion of values
	- fill with mean value ( numerical)
	- fill with most common value ( categorical)
- 3rd option: extend the imputation
	- fill the missing values
	- add a bool column stating TRUE or FALSE for Feature_was_missing

model building and score Example:
	y for labels:
		y = data.Label_Feature
		X = data.drop(['Label_Feature'], axis = 1)
			X = X.select_dtypes(exclude =['object']) `#exclude particular dataType`
		`#divide data into train and validate subset`:
		X_train, X_valid, y_train, y_valid = train_test_split(X, y, train_size=0.8, test_size=0.2, random_state=0) 
		Running the model:
			model_var = ensemble.ModelSelection_From_ScikitLearn(n_estimators=10, random_state=0)
			model_var.fit (X_train,y_train)
			y_preds = model_var.predict(X_valid)
			metrics.mean_absolute_error(y_valid, y_preds)

Score from Approach 1:
	select cols with missing values:
		cols_with missing = [col for col in X_train.columns if X_train[col].isnull().any()]
	reduced_X_train = X_train.drop(cols_with_missing, axis=1)
	reduced_X_valid = X_valid.drop(cols_with_missing, axis=1)

	MAE-Approach1 (drop columns) : 183550.22137772635

Score from Approach 2:
	using sklearn.impute.SimpleImputer()
		other form may be regression imputation --> not much additional benefit
		my_imputer = SimpleImputer(strategy = 'median')
		imputed_X_train = pd.DataFrame(my_imputer.fit_transform(X_train))
		imputed_X_valid = pd.DataFrame(my_imputer.transform(X_valid))
	--> # imputation removes column names, put them back
		imputed_X_train.columns = X_train.columns
		imputed_X_valid.columns = X_valid.columns

	MAE Approach2( imputation): 178166.46269899711

Score from approach3:
	copy original data:
		X_train_ext = X_train.copy()
		y_train_ext = y_train.copy()
	make new columns indicating what was imputed
		`X_train_plus[col + '_was_missing'] = X_train_plus[col].isnull()`
	 `X_valid_plus[col+ '_was_missing'] = y_train_plus[col].isnull()`
	repeat approach 2

	MAE approach 3: 178927.503183954
	
=====
exercisees code: 

from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error

\# Function for comparing different approaches
		def score_dataset(X_train, X_valid, y_train, y_valid):
		    model = RandomForestRegressor(n_estimators=100, random_state=0)
		    model.fit(X_train, y_train)
		    preds = model.predict(X_valid)
		    return mean_absolute_error(y_valid, preds)

\# Define and fit model
	model = RandomForestRegressor(n_estimators=100, random_state=0)
	model.fit(final_X_train, y_train)

\# Get validation predictions and MAE
	preds_valid = model.predict(final_X_valid)
	print("MAE (Your approach):")
	print(mean_absolute_error(y_valid, preds_valid))
	
https://www.kaggle.com/alexisbcook/categorical-variables
* categorical approach takes limited number of values --> fixed set
	* need preprocessing
	* 3 approaches
		* **1st: drop categoriacal variables( not best)**
			drop_X_train = X_train.select_dtypes(exclude=['object'])
			drop_X_valid = X_valid.select_dtypes(exclude=['object'])
		* **2nd: ordinal encoding assign** --> values to each answer category (
			
			from sklearn.preprocessing import OrdinalEncoder
			
			\# Make copy to avoid changing original data 
			label_X_train = X_train.copy()
			label_X_valid = X_valid.copy()
			
			\# **Apply ordinal encoder to each column with categorical data**
			ordinal_encoder = OrdinalEncoder()
			label_X_train[object_cols] = ordinal_encoder.fit_transform(X_train[object_cols])
			label_X_valid[object_cols] = ordinal_encoder.transform(X_valid[object_cols])

			print("MAE from Approach 2 (Ordinal Encoding):") 
			print(score_dataset(label_X_train, label_X_valid, y_train, y_valid))
			
		* 3rd: **One Hot Encoding:** generate boolean table with each category in a column
				`handle_unknown='ignore'` to avoid errors when the validation data contains classes that aren't represented in the training data,
				`sparse=False` ensures that the encoded columns are returned as a numpy array (instead of a sparse matrix).

			from sklearn.preprocessing import OneHotEncoder
			
			\# Apply one-hot encoder to each column with categorical data
			OH_encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)
			OH_cols_train = pd.DataFrame(OH_encoder.fit_transform(X_train[object_cols]))
			OH_cols_valid = pd.DataFrame(OH_encoder.transform(X_valid[object_cols]))

			\# One-hot encoding removed index; put it back
			OH_cols_train.index = X_train.index
			OH_cols_valid.index = X_valid.index

			\# Remove categorical columns (will replace with one-hot encoding)
			num_X_train = X_train.drop(object_cols, axis=1)
			num_X_valid = X_valid.drop(object_cols, axis=1)

			\# Add one-hot encoded columns to numerical features
			OH_X_train = pd.concat([num_X_train, OH_cols_train], axis=1)
			OH_X_valid = pd.concat([num_X_valid, OH_cols_valid], axis=1)

			print("MAE from Approach 3 (One-Hot Encoding):") 
			print(score_dataset(OH_X_train, OH_X_valid, y_train, y_valid))
---------------
exercises 
	cardinality = number of unique ocurrences in a column
	only use One hot encode  with low cardinality features

 # Get number of unique entries in each column with categorical data
object_nunique = list(map(lambda col: X_train[col].nunique(), object_cols))
d = dict(zip(object_cols, object_nunique))

 # Print number of unique entries by column, in ascending order
sorted(d.items(), key=lambda x: x[1])
---- xtest preprocess 
\# Categorical columns in the training data
object_cols = [col for col in X_train.columns if X_train[col].dtype == "object"]

\# Columns that can be safely ordinal encoded
good_label_cols = [col for col in object_cols if 
                   set(X_valid[col]).issubset(set(X_train[col]))]
        
\# Problematic columns that will be dropped from the dataset
bad_label_cols = list(set(object_cols)-set(good_label_cols))
        
print('Categorical columns that will be ordinal encoded:', good_label_cols)
print('\nCategorical columns that will be dropped from the dataset:', bad_label_cols)

\# Drop categorical columns that will not be encoded
label_X_train = X_train.drop(bad_label_cols, axis=1)

\# Apply ordinal encoder to each column with categorical data
label_X_test[good_label_cols] = ordinal_encoder.transform(X_test[good_label_cols])

https://www.kaggle.com/code/alexisbcook/pipelines
pipeline bundles preprocessing and modeling steps so you can use the whole bundle as if it were a single step.

Example -start from train and validation sets 
			import pandas as pd
			from sklearn.model_selection import train_test_split
			\# Read the data
			data = pd.read_csv('../input/melbourne-housing-snapshot/melb_data.csv')
			\# Separate target from predictors
			y = data.Price
			X = data.drop(['Price'], axis=1)
			\# Divide data into training and validation subsets
			X_train_full, X_valid_full, y_train, y_valid = train_test_split(X, y, train_size=0.8, test_size=0.2, random_state=0)
			\# "Cardinality" means the number of unique values in a column
			
\# Select categorical columns with relatively low cardinality (less than 10) (convenient but arbitrary)
			categorical_cols = [cname 
				for cname in X_train_full.columns 
					if X_train_full[cname].nunique() < 10 
					and X_train_full[cname].dtype == "object"]
			\# Select numerical columns
			numerical_cols = [cname 
				for cname in X_train_full.columns 
					if X_train_full[cname].dtype in ['int64', 'float64']]
			\# Keep selected columns only
			my_cols = categorical_cols + numerical_cols
			X_train = X_train_full[my_cols].copy()
			X_valid = X_valid_full[my_cols].copy()

Step1: preprocessing steps
			python
			from sklearn.compose import ColumnTransformer
			from sklearn.pipeline import Pipeline
			from sklearn.impute import SimpleImputer
			from sklearn.preprocessing import OneHotEncoder
			
\# Preprocessing for numerical data
			numerical_transformer = SimpleImputer(strategy='constant')
			
\# Preprocessing for categorical data
			categorical_transformer = Pipeline(steps=[
			    ( 'imputer', SimpleImputer(strategy='most_frequent') ),
			    ('onehot', OneHotEncoder(handle_unknown='ignore'))
				])
\# Bundle preprocessing for numerical and categorical data
					preprocessor = ColumnTransformer(
					    transformers=[
							  ('num', numerical_transformer, numerical_cols),
					        ('cat', categorical_transformer, categorical_cols)
			    ])

step2: define the model:
		from sklearn.ensemble import RandomForestRegressor
		model = RandomForestRegressor(n_estimators=100, random_state=0)

Step 3: Create and Evaluamyte the Pipeline[¶](https://www.kaggle.com/code/alexisbcook/pipelines#Step-3:-Create-and-Evaluate-the-Pipeline)
	from sklearn.metrics import mean_absolute_error

\# Bundle preprocessing and modeling code in a pipeline
	my_pipeline = Pipeline(steps=[('preprocessor', preprocessor),
                              ('model', model)
                             ])

\# Preprocessing of training data, fit model 
	my_pipeline.fit(X_train, y_train)

\# Preprocessing of validation data, get predictions
	preds = my_pipeline.predict(X_valid)

\# Evaluate the model
	score = mean_absolute_error(y_valid, preds)
	print('MAE:', score)

----------------
Exercises:

X_full e e X_test_full definidos
X_full tem eliminada rows  sem label

 y sao os labels
 X_full é o X

X_train_full, X_valid_full, y_train e y_valid definidos

categorical_cols --> list de colunas com dtype 'object' 
e <10 elementos unicos no conjunto

numerical_cols --> colunas com dtype int64 e float64

my_cols = categorical_cols + numerical_cols

X_train, X_valid e X_test

numerical_transformer --> simpleimputer class

\# Preprocessing for numerical data
numerical_transformer = SimpleImputer(strategy='constant')

\# Preprocessing for categorical data
categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
])


\# Save test predictions to file
output = pd.DataFrame({'Id': X_test.index,
                       'SalePrice': preds_test})
output.to_csv('submission.csv', index=False)


https://www.kaggle.com/code/alexisbcook/cross-validation
-> uses differente experiments to improve model
	number of experiments = number of divided parts ( train test split)
		example if test =20% of dataset, 5 experiments will be run 
--> when to use:
	small dataset --> demands less computing power
		(check time that it takes to process)
	you can also check if scores for each experiment are close


example:
import pandas as pd

\# Read the data
data = pd.read_csv('../input/melbourne-housing-snapshot/melb_data.csv')

\# Select subset of predictors
cols_to_use = ['Rooms', 'Distance', 'Landsize', 'BuildingArea', 'YearBuilt']
X = data[cols_to_use]

\# Select target
y = data.Price

from sklearn.ensemble import RandomForestRegressor
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer

my_pipeline = Pipeline(steps=[('preprocessor', SimpleImputer()),
                              ('model', RandomForestRegressor(n_estimators=50,
                                                              random_state=0))
                             ])

from sklearn.model_selection import cross_val_score

\# Multiply by -1 since sklearn calculates *negative* MAE
\# number of folds with the `cv` parameter.
scores = -1 * cross_val_score(my_pipeline, X, y,
                              cv=5,
                              scoring='neg_mean_absolute_error')

print("MAE scores:\n", scores)

print("Average MAE score (across experiments):")
print(scores.mean())

-----------------

exercise
import pandas as pd
from sklearn.model_selection import train_test_split

\# Read the data
train_data = pd.read_csv('../input/train.csv', index_col='Id')
test_data = pd.read_csv('../input/test.csv', index_col='Id')

\# Remove rows with missing target, separate target from predictors
train_data.dropna(axis=0, subset=['SalePrice'], inplace=True)
y = train_data.SalePrice              
train_data.drop(['SalePrice'], axis=1, inplace=True)

\# Select numeric columns only
numeric_cols = [cname 
			for cname in train_data.columns 
					if train_data[cname].dtype in ['int64', 'float64']]
X = train_data[numeric_cols].copy()
X_test = test_data[numeric_cols].copy()

\# make the pipeline with preprocess steps
from sklearn.ensemble import RandomForestRegressor
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer

my_pipeline = Pipeline(steps=[
    ('preprocessor', SimpleImputer()),
    ('model', RandomForestRegressor(n_estimators=50, random_state=0))
])


\# evaluate model
from sklearn.model_selection import cross_val_score

\# Multiply by -1 since sklearn calculates *negative* MAE
scores = -1 * cross_val_score(my_pipeline, X, y,
                              cv=5,
                              scoring='neg_mean_absolute_error')

print("Average MAE score:", scores.mean())

-----
from sklearn.ensemble import RandomForestRegressor
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer

my_pipeline = Pipeline(steps=[
    ('preprocessor', SimpleImputer()),
    ('model', RandomForestRegressor(n_estimators=50, random_state=0))
])

----
from sklearn.model_selection import cross_val_score

\# Multiply by -1 since sklearn calculates *negative* MAE
scores = -1 * cross_val_score(my_pipeline, X, y,
                              cv=5,
                              scoring='neg_mean_absolute_error')

print("Average MAE score:", scores.mean())

--------
\# method to get the best hyper parameters from a pre defined list
n = list(range(50,401,50))
results = {}
for i in n:
    results[i] = get_score(i)

\# plot the dictionaire generated
import matplotlib.pyplot as plt
%matplotlib inline

plt.plot(list(results.keys()), list(results.values()))
plt.show()

https://www.kaggle.com/code/alexisbcook/xgboost
--> gradient boosting : dominates many kaggle competitions --> achieves state-of-the art results

Introducition?:
	random forest -- > ensemble method --> combine several models

Gradient Boosting ( XG boost = Extreme Gradient Boosting)
	method --> goes thourgh cycles --> add models into ensemble
	the cycle:
			1st: current ensemble --> generate predicxtions:
			2nd: loss fucntions based on predictions of all models added
			3rd use lossfucntion to fit new model into ensemble
				this will reduce the loss( gradient boosting == gradient descent)	
			4th add new model to ensemble
			5th repeat the process

Example:
	given:
import pandas as pd
from sklearn.model_selection import train_test_split

\# Read the data
data = pd.read_csv('../input/melbourne-housing-snapshot/melb_data.csv')

\# Select subset of predictors
cols_to_use = ['Rooms', 'Distance', 'Landsize', 'BuildingArea', 'YearBuilt']
X = data[cols_to_use]

\# Select target
y = data.Price

\# Separate data into training and validation sets
X_train, X_valid, y_train, y_valid = train_test_split(X, y)

\# import XGBoost
from xgboost import XGBRegressor

my_model = XGBRegressor()
my_model.fit(X_train, y_train)

\# make predictions and evaluate model:

from sklearn.metrics import mean_absolute_error

predictions = my_model.predict(X_valid)
print("Mean Absolute Error: " + str(mean_absolute_error(predictions, y_valid)))

--> parameter Tuning (to affect accuracy and training speed)
- n_estimators --> number of models to include in ensemble
	- too low ==> underfitting
	- too high --> overfitting
	- typical values --> from 100 to 1k]

my_model = XGBRegressor(n_estimators=500)
my_model.fit(X_train, y_train)

* early_stopping_rounds --> auto find best n_estimators--> stop iteration when score stops improving
	* set high n_estimators and use early_stopping_rounds
	* example : early_stopping_rounds= 5 --> stops after 5 rounds of deteriorating validation scores
	* also need to set eval_set --> calculate validation set 

my_model = XGBRegressor(n_estimators=500)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)],
             verbose=False)

* learning_rate ( default= 0.1) --> each ensambled tree helps us less --> appropriateds number will be automatically determined

my_model = XGBRegressor(n_estimators=1000, learning_rate=0.05)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)], 
             verbose=False)

* n_jobs --> parallelism
	* good for larger datasets, n_jobs = numebr of cores in machine


my_model = XGBRegressor(n_estimators=1000, learning_rate=0.05, n_jobs=4)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)], 
             verbose=False)


\# Get predictions
predictions_1 = my_model_1.predict(X_valid) 

-----
Exercise

import pandas as pd
from sklearn.model_selection import train_test_split

\# Read the data
X = pd.read_csv('../input/train.csv', index_col='Id')
X_test_full = pd.read_csv('../input/test.csv', index_col='Id')

\# Remove rows with missing target, separate target from predictors
X.dropna(axis=0, subset=['SalePrice'], inplace=True)
y = X.SalePrice 
X.drop(['SalePrice'], axis=1, inplace=True)

\# Break off validation set from training data
X_train_full, X_valid_full, y_train, y_valid = train_test_split(X, y, train_size=0.8, test_size=0.2,

 random_state=0)

\# "Cardinality" means the number of unique values in a column
\# Select categorical columns with relatively low cardinality (convenient but arbitrary)

low_cardinality_cols = [cname for cname in X_train_full.columns if X_train_full[cname].nunique() < 10 and  X_train_full[cname].dtype == "object"]

\# Select numeric columns

numeric_cols = [cname for cname in X_train_full.columns if X_train_full[cname].dtype in ['int64', 'float64']]

\# Keep selected columns only
my_cols = low_cardinality_cols + numeric_cols
X_train = X_train_full[my_cols].copy()
X_valid = X_valid_full[my_cols].copy()
X_test = X_test_full[my_cols].copy()

\# One-hot encode the data (to shorten the code, we use pandas)
X_train = pd.get_dummies(X_train)
X_valid = pd.get_dummies(X_valid)
X_test = pd.get_dummies(X_test)
X_train, X_valid = X_train.align(X_valid, join='left', axis=1)
X_train, X_test = X_train.align(X_test, join='left', axis=1)



-----
https://www.kaggle.com/code/alexisbcook/data-leakage
* what is: when training data has info on target
	* high performance on training but poor in production
* types:
	* target leakeage
		* 1) when model includes data not available on production time
			* post prediction features
		* 2) example a data set  on  (got disease) and  (took medication for disease). this feature would be unavailable in production --> you must check when feature is produced - only use features produced b4 prediction projected time
	* train-test contamination:
		* corruption of (training --> validation) chain
		* example: how you impute NaN? 
		* do preprocessing inside pipelines

Example
import pandas as pd

\# Read the data
data = pd.read_csv('../input/aer-credit-card-data/AER_credit_card_data.csv', 
                   true_values = ['yes'], false_values = ['no'])

\# Select target
y = data.card


\# Select predictors
X = data.drop(['card'], axis=1)

print("Number of rows in the dataset:", X.shape[0])
X.head()

--
\#small dataset? use cross validation

from sklearn.pipeline import make_pipeline
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score

\# Since there is no preprocessing, we don't need a pipeline (used anyway as best practice!)
my_pipeline = make_pipeline(RandomForestClassifier(n_estimators=100))
cv_scores = cross_val_score(my_pipeline, X, y, 
                            cv=5,
                            scoring='accuracy')

print("Cross-validation accuracy: %f" % cv_scores.mean())

---
Exercises

