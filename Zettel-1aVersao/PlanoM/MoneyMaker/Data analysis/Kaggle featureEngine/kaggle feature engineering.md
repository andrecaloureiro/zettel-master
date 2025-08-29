 #kaggle https://www.kaggle.com/code/sudalairajkumar/winning-solutions-of-kaggle-competitions/notebook
#kagglesolutions

## [what-is-featureengineering](https://www.kaggle.com/code/ryanholbrook/what-is-feature-engineering)

* which features are the most important
* invent new features
* high-cardinality --> target encoding
* k-means clustering --> segment features
* PCA --> decompose dataset variation

- transformation applied to a feature becomes part of the model itself
- transform features to linearize its relationship with target

Example - industry Concrete Formulations
	- adding a few synthetic features to improve predictive model
	- model --> predict concrete's compressive strength

```Python
import pandas as pd
from sklearn.ensemble import RandomForestRegressor
from sklearn.model_selection import cross_val_score

df = pd.read_csv("../input/fe-course-data/concrete.csv")
df.head()
```

--> 1st get a score on the original features ( no synthetic addition)
	- baseline score

```Python
X = df.copy()
y = X.pop("CompressiveStrength")

\# Train and score baseline model
baseline = RandomForestRegressor(criterion="mae", random_state=0)
baseline_score = cross_val_score(baseline, X, y, 
		cv=5, 
		scoring="neg_mean_absolute_error"
		)
baseline_score = -1 * baseline_score.mean()

print(f"MAE Baseline Score: {baseline_score:.4}")
```

--> try using ratio of component features of concrete

```
X = df.copy()
y = X.pop("CompressiveStrength")

\# Create synthetic features
X["FCRatio"] = X["FineAggregate"] / X["CoarseAggregate"]
X["AggCmtRatio"] = (X["CoarseAggregate"] + X["FineAggregate"]) / X["Cement"]
X["WtrCmtRatio"] = X["Water"] / X["Cement"]

\# Train and score model on dataset with additional ratio features
model = RandomForestRegressor(criterion="mae", random_state=0)
score = cross_val_score(
    model, X, y, cv=5, scoring="neg_mean_absolute_error"
)
score = -1 * score.mean()

print(f"MAE Score with Ratio Features: {score:.4}")
```

------
Exercises


---

## [Mutual Information](https://www.kaggle.com/code/ryanholbrook/mutual-information)
 --> getting lots of features?
	 - start building a ranking an utility ranking
	 - mutual info detects any kind of relationship
		 - correlation only detects linear relationships

 - Mutual info and what it meausres?
	 - in what measure MI knowledge of one quantity reduces uncertainty about the other
	 - example: how much the exterior of a House says about its saleprice?
	 - Mi can help understand -- relative potential -- of a feature .. by itself .. without interaction with other featurtes

Example - 1985 mobiles dataset
- predict car prices (193 cars 1985 model)
- MI needs to separate discrete from continuous features

```Python
# start dataset
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns

plt.style.use("seaborn-whitegrid")

df = pd.read_csv("../input/fe-course-data/autos.csv")
df.head()

```
get X and y


```
X = df.copy()
y = X.pop("price")

# Label encoding for categoricals
for colname in X.select_dtypes("object"):
    X[colname], _ = X[colname].factorize()

# All discrete features should now have integer dtypes (double-check this before using MI!)
discrete_features = X.dtypes == int
```
--> Apply mutual information

```Python
# use Mutual info regression and classif utility from sklearn
from sklearn.feature_selection import mutual_info_regression

def make_mi_scores(X, y, discrete_features):
    mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features)
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    mi_scores = mi_scores.sort_values(ascending=False)
    return mi_scores

mi_scores = make_mi_scores(X, y, discrete_features)
mi_scores[::3]  # show a few features with their MI scores
```

\# plot some visualization to get better info:
```
def plot_mi_scores(scores):
    scores = scores.sort_values(ascending=True)
    width = np.arange(len(scores))
    ticks = list(scores.index)
    plt.barh(width, scores)
    plt.yticks(width, ticks)
    plt.title("Mutual Information Scores")

plt.figure(dpi=100, figsize=(8, 5))
plot_mi_scores(mi_scores)

\# curb_weight and price shows strong relations with price. Explore!
sns.relplot(x="curb_weight", y="price", data=df);

\# you can split visualization by one more category, using hue
sns.lmplot(x="horsepower", y="price", hue="fuel_type", data=df);
```
-------

Exercvises

\# Setup feedback system
```
from learntools.core import binder
binder.bind(globals())
from learntools.feature_engineering_new.ex2 import *

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
from sklearn.feature_selection import mutual_info_regression
```

```
\# Set Matplotlib defaults
plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)


\# Load data
df = pd.read_csv("../input/fe-course-data/ames.csv")
```

\# Utility functions from Tutorial

```
def make_mi_scores(X, y):
    X = X.copy()
    for colname in X.select_dtypes(["object", "category"]):
        X[colname], _ = X[colname].factorize()
    # All discrete features should now have integer dtypes
    discrete_features = [pd.api.types.is_integer_dtype(t) for t in X.dtypes]
    mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features, random_state=0)
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    mi_scores = mi_scores.sort_values(ascending=False)
    return mi_scores


def plot_mi_scores(scores):
    scores = scores.sort_values(ascending=True)
    width = np.arange(len(scores))
    ticks = list(scores.index)
    plt.barh(width, scores)
    plt.yticks(width, ticks)
    plt.title("Mutual Information Scores")
```

\# review meaning of mutual info:
features = ["YearBuilt", "MoSold", "ScreenPorch"]
sns.relplot(
    x="value", y="SalePrice", col="variable", data=df.melt(id_vars="SalePrice", value_vars=features), facet_kws=dict(sharex=False),
);

X = df.copy()
y = X.pop('SalePrice')

mi_scores = make_mi_scores(X, y)

\# plot top and bottom ranks
print(mi_scores.head(20))
\# print(mi_scores.tail(20))  # uncomment to see bottom 20

plt.figure(dpi=100, figsize=(8, 5))
plot_mi_scores(mi_scores.head(20))
\# plot_mi_scores(mi_scores.tail(20))  # uncomment to see bottom 20

\# BldgType feature not good for distinguishing saleprice
sns.catplot(x="BldgType", y="SalePrice", data=df, kind="boxen");

\# investigate BldgType interation with GrLivArea and MoSold
\# YOUR CODE HERE: 
feature = "GrLivArea"

sns.lmplot(
    x=feature, y="SalePrice", hue="BldgType", col="BldgType",
    data=df, scatter_kws={"edgecolor": 'w'}, col_wrap=3, height=4,
);




## [creating-features](https://www.kaggle.com/code/ryanholbrook/creating-features)

\# check some transformations with 4 different datasets
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns

plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)

accidents = pd.read_csv("../input/fe-course-data/accidents.csv")
autos = pd.read_csv("../input/fe-course-data/autos.csv")
concrete = pd.read_csv("../input/fe-course-data/concrete.csv")
customer = pd.read_csv("../input/fe-course-data/customer.csv")


--> get some real knowledge on dataset ( example: if real estate dataset and price predicting you can make some research on real estate)
		- example: automobile dataset (autos) --> formulas like stroke ratio effciency / performance ratio
		- 
autos["stroke_ratio"] = autos.stroke / autos.bore
autos[["stroke", "bore", "stroke_ratio"]].head()

\#  some auto formulas may be more complicated:
autos["displacement"] = (
    np.pi * ((0.5 * autos.bore) ** 2) * autos.stroke * autos.num_of_cylinders
)

\# If the feature has 0.0 values, use np.log1p (log(1+x)) instead of np.log
accidents["LogWindSpeed"] = accidents.WindSpeed.apply(np.log1p)

\# Plot a comparison
fig, axs = plt.subplots(1, 2, figsize=(8, 4))
sns.kdeplot(accidents.WindSpeed, shade=True, ax=axs[0])
sns.kdeplot(accidents.LogWindSpeed, shade=True, ax=axs[1]);


--> Counts
	- some features may come in sets
		- ex: the presence or absence of certain roadway obstacles on an accidents dataset
		- 
roadway_features = ["Amenity", "Bump", "Crossing", "GiveWay",
    "Junction", "NoExit", "Railway", "Roundabout", "Station", "Stop",
    "TrafficCalming", "TrafficSignal"]
accidents["RoadwayFeatures"] = accidents[roadway_features].sum(axis=1)

accidents[roadway_features + ["RoadwayFeatures"]].head(10)


\# counting how many cement entries has more than 0 as active  components on formulation
components = [ "Cement", "BlastFurnaceSlag", "FlyAsh", "Water",
               "Superplasticizer", "CoarseAggregate", "FineAggregate"]
concrete["Components"] = concrete[components].gt(0).sum(axis=1)

concrete[components + ["Components"]].head(10)

--> build up and break down features
	- ex: phone numbers can be broken as ddi+ ddd + phone
	- ex: internet addresses, street address... dates and times
	- Example: customer Lifetime Value dataset. .. Policy feature (eX: Corporate + L3)could be separated:

customer[["Type", "Level"]] = (  # Create two new features
    customer["Policy"]           # from the Policy feature
    .str                         # through the string accessor
    .split(" ", expand=True)     # by splitting on " "
                                 # and expanding the result into separate columns
)

customer[["Policy", "Type", "Level"]].head(10)

\# you can also join features in a composition if you believe there is an interaction among features
autos["make_and_style"] = autos["make"] +```"_"``` + autos["body_style"]
autos[["make", "body_style", "make_and_style"]].head()

process features with the help of some coursees:
date and time: https://www.kaggle.com/alexisbcook/parsing-dates
lat and longitude: https://www.kaggle.com/learn/geospatial-analysis
text: https://www.kaggle.com/learn/natural-language-processing

--> Group Transforms
		-agrega info de varias rows , por categoria
			exaple: avg income by state
			example; proportion of movies released on a weekday by genre

customer["AverageIncome"] = (
    customer.groupby("State")  # for each state
    ["Income"]                 # select the income
    .transform("mean")         # and compute its mean
)

\# frequency each state occurs in the dataaset
\# could be used a frequency ecoding feature for any feature
customer["StateFreq"] = (
    customer.groupby("State")
    ["State"]
    .transform("count")
    / customer.State.count()
)

customer[["State", "StateFreq"]].head(10)

--> if using train and validation sets--> create grouped feat in training  --> join it to validation(use merge()

\# Create splits
df_train = customer.sample(frac=0.5)
df_valid = customer.drop(df_train.index)

\# Create the average claim amount by coverage type, on the training set
df_train["AverageClaim"] = df_train.groupby("Coverage")["ClaimAmount"].transform("mean")

\# Merge the values into the validation set
df_valid = df_valid.merge(
    df_train[["Coverage", "AverageClaim"]].drop_duplicates(),
    on="Coverage",
    how="left",
)

df_valid[["Coverage", "AverageClaim"]].head(10)

**Tips on Creating Features**  
It's good to keep in mind your model's own strengths and weaknesses when creating features. Here are some guidelines:

-   Linear models learn sums and differences naturally, but can't learn anything more complex.
-   Ratios seem to be difficult for most models to learn. Ratio combinations often lead to some easy performance gains.
-   Linear models and neural nets generally do better with normalized features. Neural nets especially need features scaled to values not too far from 0. Tree-based models (like random forests and XGBoost) can sometimes benefit from normalization, but usually much less so.
-   Tree models can learn to approximate almost any combination of features, but when a combination is especially important they can still benefit from having it explicitly created, especially when data is limited.
-   Counts are especially helpful for tree models, since these models don't have a natural way of aggregating information across many features at once.

------

Exercises

\# Setup feedback system
from learntools.core import binder
binder.bind(globals())
from learntools.feature_engineering_new.ex3 import *

import numpy as np
import pandas as pd
from sklearn.model_selection import cross_val_score
from xgboost import XGBRegressor


def score_dataset(X, y, model=XGBRegressor()):
    \# Label encoding for categoricals
    for colname in X.select_dtypes(["category", "object"]):
        X[colname], _ = X[colname].factorize()
    \# Metric for Housing competition is RMSLE (Root Mean Squared Log Error)
    score = cross_val_score(
        model, X, y, cv=5, scoring="neg_mean_squared_log_error",
    )
    score = -1 * score.mean()
    score = np.sqrt(score)
    return score


\# Prepare data
df = pd.read_csv("../input/fe-course-data/ames.csv")
X = df.copy()
y = X.pop("SalePrice")

\#1) create mathematical transforms

\# YOUR CODE HERE
X_1 = pd.DataFrame()  # dataframe to hold new features

X_1["LivLotRatio"] = X['GrLivArea'] / X['LotArea']
X_1["Spaciousness"] = (X['FirstFlrSF'] + X['SecondFlrSF']) / X['TotRmsAbvGrd']
X_1["TotalOutsideSF"] =  X['WoodDeckSF'] + X['OpenPorchSF'] + X['EnclosedPorch'] + X['Threeseasonporch'] + X['ScreenPorch']


\# Check your answer
q_1.check()

is there an interaciotn between numeric and categorical feature?  --> use one hot encoding

```
# One-hot encode Categorical feature, adding a column prefix "Cat"
X_new = pd.get_dummies(df.Categorical, prefix="Cat")

# Multiply row-by-row
X_new = X_new.mul(df.Continuous, axis=0)

# Join the new features to the feature set
X = X.join(X_new)
```


\# 2) are there interactions with categorical?
\# YOUR CODE HERE
\# One-hot encode BldgType. Use `prefix="Bldg"` in `get_dummies`
X_2 = pd.get_dummies(X.BldgType, prefix ='Bldg') 
\# Multiply
X_2 = X_2.mul(X.GrLivArea, axis=0)


\# Check your answer
q_2.check()


\# 3) Count Feature

\# create feature 'PorchTypes' that counts how many of following are greater than 0.0:
```
WoodDeckSF
OpenPorchSF
EnclosedPorch
Threeseasonporch
ScreenPorch
```

X_3 = pd.DataFrame()

porch_features = ['WoodDeckSF','OpenPorchSF','EnclosedPorch','Threeseasonporch','ScreenPorch']

X_3["PorchTypes"] = X[porch_features].gt(0).sum(axis=1)

\# Check your answer
q_3.check()

\#4) break down Categorical Feature 

df.MSSubClass.unique()
\#This feature could be split at the first word before _ . Use argument n=1
```
X_4 = pd.DataFrame()

# YOUR CODE HERE
X_4['MSClass'] = (
    X['MSSubClass']
    .str
    .split("_", n=1,expand=True)[0]
)

# Check your answer
q_4.check()
```

\#5) Use A grouped transform
\#create Feature MedNhbdArea --> median of GrLivArea grouped on Neighborhood 
```
X_5 = pd.DataFrame()

# YOUR CODE HERE
X_5["MedNhbdArea"] = (
    X.groupby('Neighborhood')
    ['GrLivArea']
    .transform('median'))

# Check your answer
q_5.check()
```

```
# add the new features and score the model

X_new = X.join([X_1, X_2, X_3, X_4, X_5])
score_dataset(X_new, y)

```

----




## [Clustering with-k-means](https://www. /code/ryanholbrook/clustering-with-k-means)

- unsupervised algorithm --> feature discovery technique
-  clustering --> grouping points based on their similarity
	ex: market segments

cluster labels as a feature
	works like a "binning" or "discretization " transform on continuous value features
	cluester break up complicated relationships into simpler chunks
	"divide and conquer" strategy


k-means clustering
	similarity using ordinary straight line distance ( euclidean distance)
	creates clusters using centroids
	the k in k-means is the numebr of centroids --> user defined
	**VORONOI Tessalation** --> cluster map with well defined frontiers

--> application of k-means clustering on [ames dataset](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data)
	- 3 parameters for scikit-learn implementation:
		- n_clusters --> the k
			- 1) assign points to nearest cluester centroid
			- 2) move each centroid to minimize distance to its points
		- max_iter --> iterate until reach this limit
			- best for large number of clusters
		- n_init --> max initial centroid placement  --> initial placement may define optimal clustering
			- for complex dataset

--> Example: California Housing
	- latitude and longitudfe
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
from sklearn.cluster import KMeans

plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)

df = pd.read_csv("../input/fe-course-data/housing.csv")
X = df.loc[:, ["MedInc", "Latitude", "Longitude"]]
\# clustering these with MedInc ( median Income)
X.head()

--> clustering is sensitive to scale
	- good idfea to rescale or normalize data with extreme values


\# Create cluster feature
kmeans = KMeans(n_clusters=6)
X["Cluster"] = kmeans.fit_predict(X)
X["Cluster"] = X["Cluster"].astype("category")

X.head()

sns.relplot(
    x="Longitude", y="Latitude", hue="Cluster", data=X, height=6,
);

--> MedHouseVal( Median House Value) is the target in this dataset
 
X["MedHouseVal"] = df["MedHouseVal"]
sns.catplot(x="MedHouseVal", y="Cluster", data=X, kind="boxen", height=6);

----
Exercises:

```
# Setup feedback system
from learntools.core import binder
binder.bind(globals())
from learntools.feature_engineering_new.ex4 import *

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
from sklearn.cluster import KMeans
from sklearn.model_selection import cross_val_score
from xgboost import XGBRegressor

# Set Matplotlib defaults
plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)


def score_dataset(X, y, model=XGBRegressor()):
    # Label encoding for categoricals
    for colname in X.select_dtypes(["category", "object"]):
        X[colname], _ = X[colname].factorize()
    # Metric for Housing competition is RMSLE (Root Mean Squared Log Error)
    score = cross_val_score(
        model, X, y, cv=5, scoring="neg_mean_squared_log_error",
    )
    score = -1 * score.mean()
    score = np.sqrt(score)
    return score


# Prepare data
df = pd.read_csv("../input/fe-course-data/ames.csv")

```
1) rescale features or not?
	no if they are comparable.)ex test reaulsts at different times)
	yes if they arent on comparable scales ( like height and weight)
	larger values will get more weight
	compraing different rescaling schemes (with crossval) might help
		also check **preprocessing** module in scikit-learn for rescaling methods

2) Create Feature of Cluster Labels

-   features: `LotArea`, `TotalBsmtSF`, `FirstFlrSF`, `SecondFlrSF`,`GrLivArea`
-   number of clusters: 10
-   iterations: 10

 ```
 X = df.copy()
y = X.pop("SalePrice")


# YOUR CODE HERE: Define a list of the features to be used for the clustering
features = ['LotArea', 'TotalBsmtSF', 'FirstFlrSF', 'SecondFlrSF','GrLivArea']

# Standardize
X_scaled = X.loc[:, features]
X_scaled = (X_scaled - X_scaled.mean(axis=0)) / X_scaled.std(axis=0)


# YOUR CODE HERE: Fit the KMeans model to X_scaled and create the cluster labels
kmeans = KMeans(n_clusters=10, n_init=10, random_state=0, verbose=True)
X["Cluster"] = kmeans.fit_predict(X_scaled)
X['Cluster'] = X['Cluster'].astype('category')

# Check your answer
q_2.check()
 ```

check the result of clustering with the next cell:

```
Xy = X.copy()
Xy["Cluster"] = Xy.Cluster.astype("category")
Xy["SalePrice"] = y
sns.relplot(
    x="value", y="SalePrice", hue="Cluster", col="variable",
    height=4, aspect=1, facet_kws={'sharex': False}, col_wrap=3,
    data=Xy.melt(
        value_vars=features, id_vars=["SalePrice", "Cluster"],
    ),
);

```

3) Cluster-Distance Features

--> k-means algorithm  --> alternative way of creating features
	- get distance features with fit_transform instead of fit_predict

## [Principal Component Analysis](https://www.kaggle.com/code/ryanholbrook/principal-component-analysis)

- clustering = partitioning dataset based on proximity
- PCA = partitioning of variation
	- typically applied to standardized data ( variation = correlation)
		- standardized data = correlation
		- un-standardized = covariance

--> Principal Component Analysis

- [Abalone](https://www.kaggle.com/rodolfomendes/abalone-dataset) dataset
	- Height and Diameter Check
	- the axes of variation
		- become the new feature
		- just linear combinations(weighted sums of original features)


```
df["Size"] = 0.707 * X["Height"] + 0.707 * X["Diameter"]
df["Shape"] = 0.707 * X["Height"] - 0.707 * X["Diameter"]
```
--> principal components --> the new features
--> loadings --> the weights thewmselves

- PCA tells the --ammount-- of variation in each component
	- percent of explained variation


PCA for feature Engineering
	- 2 ways of using
		- 1stuse it as descriptive techniqie
			'height' x 'diameter' if 'size' is important
			'height' / 'diameter' if 'shape' is important
		- 2nd use the components as features
			- compnents expose the variation of features
			- dimensionality reduction: for highly redundant features ( drop them)
			- anomaly detection: they show up in low var components --> use it for outlier detection and study
			- Noise reduction: sensor reading and background noise --> use PCA to boost signal to noise ratio
			- Decorrelation: Some ML algos struggle with high Correl --> PCA transforms features into uncorrelated
	- Only works with:
		- Numeric features: count or consinuous quantity
		- PCA is Sensitivbe to scale --> standardize ( unless there's good reason not to)
		- consider oulier constrain or removal --> they influence result


Example - 1985 Automobiles

[Automobile data set](https://www.kaggle.com/toramky/automobile-dataset)
```
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
from IPython.display import display
from sklearn.feature_selection import mutual_info_regression

plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)

def plot_variance(pca, width=8, dpi=100):
    # Create figure
    fig, axs = plt.subplots(1, 2)
    n = pca.n_components_
    grid = np.arange(1, n + 1)
    # Explained variance
    evr = pca.explained_variance_ratio_
    axs[0].bar(grid, evr)
    axs[0].set(
        xlabel="Component", title="% Explained Variance", ylim=(0.0, 1.0)
    )
    # Cumulative Variance
    cv = np.cumsum(evr)
    axs[1].plot(np.r_[0, grid], np.r_[0, cv], "o-")
    axs[1].set(
        xlabel="Component", title="% Cumulative Variance", ylim=(0.0, 1.0)
    )
    # Set up figure
    fig.set(figwidth=8, dpi=100)
    return axs

def make_mi_scores(X, y, discrete_features):
    mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features)
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    mi_scores = mi_scores.sort_values(ascending=False)
    return mi_scores

df = pd.read_csv("../input/fe-course-data/autos.csv")

\# sleect high four MI score features + standardize so they are in same scale

features = ["highway_mpg", "engine_size", "horsepower", "curb_weight"]

X = df.copy()
y = X.pop('price')
X = X.loc[:, features]

\# Standardize
X_scaled = (X - X.mean(axis=0)) / X.std(axis=0)
```



\# fit Sklearn PCA estimator and create principal components
```
from sklearn.decomposition import PCA

\# Create principal components
pca = PCA()
X_pca = pca.fit_transform(X_scaled)

\# Convert to dataframe
component_names = [f"PC{i+1}" for i in range(X_pca.shape[1])]
X_pca = pd.DataFrame(X_pca, columns=component_names)

X_pca.head()

\# the `PCA` instance contains the loadings in its `components_` attribute
loadings = pd.DataFrame(
    pca.components_.T,  # transpose the matrix of loadings
    columns=component_names,  # so the columns are the principal components
    index=X.columns,  # and the rows are the original features
)
loadings
\# check the signals
```

\# Look at explained variance
plot_variance(pca);


\# get MI scores for each component

mi_scores = make_mi_scores(X_pca, y, discrete_features=False)
mi_scores


\# Show dataframe sorted by PC3
idx = X_pca["PC3"].sort_values(ascending=False).index
cols = ["make", "body_style", "horsepower", "curb_weight"]
df.loc[idx, cols]

\#express the contrast
df["sports_or_wagon"] = X.curb_weight / X.horsepower
sns.regplot(x="sports_or_wagon", y='price', data=df, order=2);

---

Exercises
```
# Setup feedback system
from learntools.core import binder
binder.bind(globals())
from learntools.feature_engineering_new.ex5 import *

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
from sklearn.decomposition import PCA
from sklearn.feature_selection import mutual_info_regression
from sklearn.model_selection import cross_val_score
from xgboost import XGBRegressor

# Set Matplotlib defaults
plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)


def apply_pca(X, standardize=True):
    # Standardize
    if standardize:
        X = (X - X.mean(axis=0)) / X.std(axis=0)
    # Create principal components
    pca = PCA()
    X_pca = pca.fit_transform(X)
    # Convert to dataframe
    component_names = [f"PC{i+1}" for i in range(X_pca.shape[1])]
    X_pca = pd.DataFrame(X_pca, columns=component_names)
    # Create loadings
    loadings = pd.DataFrame(
        pca.components_.T,  # transpose the matrix of loadings
        columns=component_names,  # so the columns are the principal components
        index=X.columns,  # and the rows are the original features
    )
    return pca, X_pca, loadings


def plot_variance(pca, width=8, dpi=100):
    # Create figure
    fig, axs = plt.subplots(1, 2)
    n = pca.n_components_
    grid = np.arange(1, n + 1)
    # Explained variance
    evr = pca.explained_variance_ratio_
    axs[0].bar(grid, evr)
    axs[0].set(
        xlabel="Component", title="% Explained Variance", ylim=(0.0, 1.0)
    )
    # Cumulative Variance
    cv = np.cumsum(evr)
    axs[1].plot(np.r_[0, grid], np.r_[0, cv], "o-")
    axs[1].set(
        xlabel="Component", title="% Cumulative Variance", ylim=(0.0, 1.0)
    )
    # Set up figure
    fig.set(figwidth=8, dpi=100)
    return axs


def make_mi_scores(X, y):
    X = X.copy()
    for colname in X.select_dtypes(["object", "category"]):
        X[colname], _ = X[colname].factorize()
    # All discrete features should now have integer dtypes
    discrete_features = [pd.api.types.is_integer_dtype(t) for t in X.dtypes]
    mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features, random_state=0)
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    mi_scores = mi_scores.sort_values(ascending=False)
    return mi_scores


def score_dataset(X, y, model=XGBRegressor()):
    # Label encoding for categoricals
    for colname in X.select_dtypes(["category", "object"]):
        X[colname], _ = X[colname].factorize()
    # Metric for Housing competition is RMSLE (Root Mean Squared Log Error)
    score = cross_val_score(
        model, X, y, cv=5, scoring="neg_mean_squared_log_error",
    )
    score = -1 * score.mean()
    score = np.sqrt(score)
    return score


df = pd.read_csv("../input/fe-course-data/ames.csv")
```

-show some features correl with Saleprice
```
features = [
    "GarageArea",
    "YearRemodAdd",
    "TotalBsmtSF",
    "GrLivArea",
]

print("Correlation with SalePrice:\n")
print(df[features].corrwith(df.SalePrice))
```


--> use PCA to untangle structural correl + suggest relatiuonships
```
y = X.pop("SalePrice")
X = X.loc[:, features]

# `apply_pca`, defined above, reproduces the code from the tutorial
pca, X_pca, loadings = apply_pca(X)
print(loadings)
```

--> 2 possible choices for joining the best ranking feature
\# join all of the pca columns
```python
X = X.join(X_pca)
```

\# create Custom features
```python
X["Feature1"] = X.GrLivArea + X.TotalBsmtSF
X["Feature2"] = X.YearRemodAdd * X.TotalBsmtSF
```

## [Target-encoding](https://www.kaggle.com/code/ryanholbrook/target-encoding)

- used in categorical features
- encode as numbers as in one-hot or label encoding
	- difference is in use of target to create encoding
```
import pandas as pd
autos = pd.read_csv("../input/fe-course-data/autos.csv")
```
--> Target encoding --> replace feature categ with number derived from target
	-simple and effective version: group aggregation like mean, in lesson 3:
		bin counting or mean encoding (likelihood encoding, imapct encode and leave-on-out encoding)

```
autos["make_encoded"] = autos.groupby("make")["price"].transform("mean")
autos[["make", "price", "make_encoded"]].head(10)
```

--> smoothing
	- blend in-category average with overall average
	- rare categories --> less weight
	- missing categories --> overall avg

```
encoding = weight * in_category + (1 - weight) * overall
```

 - weight is between 0 and 1
	 - weight = n / (n + m)
		n = number of times category occurs in data
		m = smoothing factor --> large values gives more weight to overall estimate
			bigger value if bigger variation
		ex: chevrolet = 0.6 * 6000.00 + 0.4 * 13285.03
	- use bigger smoothing factor when average prices are not stable

use cases for target encoding:
	high cardinality features --> One hot would generate lots of columns
	Domain-motivated features --> target encoding may reveal features usefulness even if it scored poorly in solo metric


Example - MovieLens1M:
	[dataset](https://www.kaggle.com/grouplens/movielens-20m-dataset)
	1Million movie ratings
	
```
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
import warnings

plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)
warnings.filterwarnings('ignore')

df = pd.read_csv("../input/fe-course-data/movielens1m.csv")
df = df.astype(np.uint8, errors='ignore') # reduce memory footprint
print("Number of Unique Zipcodes: {}".format(df["Zipcode"].nunique()))
```
---

\# Zipcode feature has 3000 categories --> good candidate for target encoding
\# create a 25% split to train target encoder
```
X = df.copy()
y = X.pop('Rating')

X_encode = X.sample(frac=0.25)
y_encode = y[X_encode.index]
X_pretrain = X.drop(X_encode.index)
y_train = y[X_pretrain.index]
```

--------

category_encoders package in scikit-learn-contrib implements an m-estimate encoder, which we'll use to encode our Zipcode feature. 

```Python
from category_encoders import MEstimateEncoder

\# Create the encoder instance. Choose m to control noise.
encoder = MEstimateEncoder(cols=["Zipcode"], m=5.0)

\# Fit the encoder on the encoding split.
encoder.fit(X_encode, y_encode)

\# Encode the Zipcode column to create the final training data
X_train = encoder.transform(X_pretrain)

```

compare encoded values to the target:

```
plt.figure(dpi=90)
ax = sns.distplot(y, kde=False, norm_hist=True)
ax = sns.kdeplot(X_train.Zipcode, color='r', ax=ax)
ax.set_xlabel("Rating")
ax.legend(labels=['Zipcode', 'Rating']);
```

-----

exercises:
```
# Setup feedback system
from learntools.core import binder
binder.bind(globals())
from learntools.feature_engineering_new.ex6 import *

import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
import warnings
from category_encoders import MEstimateEncoder
from sklearn.model_selection import cross_val_score
from xgboost import XGBRegressor

# Set Matplotlib defaults
plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)
warnings.filterwarnings('ignore')


def score_dataset(X, y, model=XGBRegressor()):
    # Label encoding for categoricals
    for colname in X.select_dtypes(["category", "object"]):
        X[colname], _ = X[colname].factorize()
    # Metric for Housing competition is RMSLE (Root Mean Squared Log Error)
    score = cross_val_score(
        model, X, y, cv=5, scoring="neg_mean_squared_log_error",
    )
    score = -1 * score.mean()
    score = np.sqrt(score)
    return score


df = pd.read_csv("../input/fe-course-data/ames.csv")
```

which features to apply target encoding to? ( catgeoricla with large number fo cats)

run this cell to check:
```
df.select_dtypes(["object"]).nunique()
```

1) select categories:  Neighborhood, Exterior1st, Exterior2nd, MSSubClass

check how many times a category occurs in the dataset:
are there many rare categories? ( b)

```
df["Neighborhood"].value_counts()
```

--> apply target encoding at feature of choice:
 avoid overfitting by using only a fraction ( 20% ) of training  data for encoding
 
```
# Encoding split
X_encode = df.sample(frac=0.20, random_state=0)
y_encode = X_encode.pop("SalePrice")

# Training split
X_pretrain = df.drop(X_encode.index)
y_train = X_pretrain.pop("SalePrice")
```

2) Apply M-estimate Encoding

```
# YOUR CODE HERE: Create the MEstimateEncoder
# Choose a set of features to encode and a value for m

from category_encoders import MEstimateEncoder

# Create the encoder instance. Choose m to control noise.
encoder = MEstimateEncoder(cols=['Neighborhood', 'Exterior1st', 'Exterior2nd', 'MSSubClass'], m=3.0)


# Fit the encoder on the encoding split
encoder.fit(X_encode, y_encode)

# Encode the training split
X_train = encoder.transform(X_pretrain, y_train)


# Check your answer
q_2.check()
```

check how encoded feat compares to the target:

```
feature = encoder.cols

plt.figure(dpi=90)
ax = sns.distplot(y_train, kde=True, hist=False)
ax = sns.distplot(X_train[feature], color='r', ax=ax, hist=True, kde=False, norm_hist=True)
ax.set_xlabel("SalePrice");
```

--> now get a score for encoded target and encodding score

```
X = df.copy()
y = X.pop("SalePrice")
score_base = score_dataset(X, y)
score_new = score_dataset(X_train, y_train)

print(f"Baseline Score: {score_base:.4f} RMSLE")
print(f"Score with Encoding: {score_new:.4f} RMSLE")
```


--> now lets see overfitting with target encoding --> lets encode target as a count(0,1,2,3,4,5,6,...)

```
# Try experimenting with the smoothing parameter m
# Try 0, 1, 5, 50
m = 0

X = df.copy()
y = X.pop('SalePrice')

# Create an uninformative feature
X["Count"] = range(len(X))
X["Count"][1] = 0  # actually need one duplicate value to circumvent error-checking in MEstimateEncoder

# fit and transform on the same dataset
encoder = MEstimateEncoder(cols="Count", m=m)
X = encoder.fit_transform(X, y)

# Results
score =  score_dataset(X, y)
print(f"Score: {score:.4f} RMSLE")
```

--> what a neat distribution:

```
plt.figure(dpi=90)
ax = sns.distplot(y, kde=True, hist=False)
ax = sns.distplot(X["Count"], color='r', ax=ax, hist=True, kde=False, norm_hist=True)
ax.set_xlabel("SalePrice");
```


3) Overfitting with target encoders
How XGBoost got an almost pérfect score?

Count is essentially a perfect copy of the target --> turn a meaningless feat into perfect feat
--> training of XGBoost on same set used to train encoder.
--> lesson learned: use separate sets for trainning encoder and training model

