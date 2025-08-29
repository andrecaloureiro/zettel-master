https://www.kaggle.com/residentmario/creating-reading-and-writing
import pandas as pd

example dataframe:
	pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]})
	pd.DataFrame({'Bob': ['I liked it.', 'It was awful.'], 
              'Sue': ['Pretty good.', 'Bland.']},
             index=['Product A', 'Product B'])

Example Series:
	pd.Series([1, 2, 3, 4, 5])
	pd.Series([30, 35, 40], index=['2015 Sales', '2016 Sales', '2017 Sales'], name='Product A')


reading nd checking data files:
	wine_reviews = pd.read_csv("../input/wine-reviews/winemag-data-130k-v2.csv",index_col=0 )
	wine_reviews.shape
	wine_reviews.head()
	wine_reviews.tail()
	
writing csv to a file:
	animals.to_csv('cows_and_goats.csv')
	
https://www.kaggle.com/residentmario/indexing-selecting-assigning


using loc and iloc:
	reviews.iloc[:, 0] # get 1st column

label based selection with loc:
	reviews.loc[0, 'country'] # get 1st entry of ountry column 

index manipulation:
	reviews.set_index("title")

conditional selection:
	reviews.country == 'Italy'
	reviews.loc[reviews.country == 'Italy']
	reviews.loc[(reviews.country == 'Italy') & (reviews.points >= 90)]
	reviews.loc[(reviews.country == 'Italy') | (reviews.points >= 90)]
	reviews.loc[reviews.country.isin(['Italy', 'France'])]
	reviews.loc[reviews.price.notnull()]

assign new column?:
	reviews['critic'] = 'everyone'

```python
reviews.description.iloc[:10]
= reviews.loc[:9, "description"]
= reviews.description.loc[:9,'description']
```

https://www.kaggle.com/residentmario/summary-functions-and-maps

summaries:
	reviews.points.describe()
	reviews.points.mean()
	reviews.taster_name.unique()
	reviews.taster_name.value_counts()
	bargain_idx = (reviews.points / reviews.price).idxmax()
		idxmin()

Maps
	reviews.points.map(lambda p: p - review_points_mean)
	---
	def remean_points(row):
	    row.points = row.points - review_points_mean
	    return row
	
   - reviews.apply(remean_points, axis='columns')
---
	
https://www.kaggle.com/residentmario/grouping-and-sorting
-->: group the data
Groupwise analysis:
	We can replicate what `value_counts()` does by doing the following:
		reviews.groupby('points').points.count()
	 one way of selecting the name of the first wine reviewed from each winery in the dataset:
		reviews.groupby('winery').apply(lambda df: df.title.iloc[0])
	how we would pick out the best wine by country _and_ province::
		reviews.groupby(['country', 'province']).apply(lambda df: df.loc[df.points.idxmax()])
	generate simple stats summary of the dataset:
		reviews.groupby(['country']).price.agg([len, min, max])

Multi-indexes:
	- https://pandas.pydata.org/pandas-docs/stable/advanced.html
	- reset back to single index:
		- countries_reviewed.reset_index()

Sorting:
	- countries_reviewed.sort_values(by='len') --> ascending by default
	- countries_reviewed.sort_values(by='len', ascending=False)
	- sort back by index:
		- countries_reviewed.sort_index()
	- sort by more than one column:
		- countries_reviewed.sort_values(by=['country', 'len'])
	
		
	
	



https://www.kaggle.com/residentmario/data-types-and-missing-values
Data type:
reviews.dtype

data type transformation
reviews.points.astype('float64')

missing data: --> not a number (float64) NaN
	isnull()
	notnull()

filling missing data:
	fillna -- >reviews.region_2.fillna("Unknown")
	backfill strategy--> fill nAn with first non null that appears after missing record
	reviews.taster_twitter_handle.replace("@kerinokeefe", "@kerino")


https://www.kaggle.com/residentmario/renaming-and-combining
change index or column names:
	reviews.rename(columns={'points': 'score'})
	reviews.rename(index={0: 'firstEntry', 1: 'secondEntry'})

change the attribute name ofd index and column:
	reviews.rename_axis("wines", axis='rows').rename_axis("fields", axis='columns')

combining DataFrames:
	concat() --> pd.concat([canadian_youtube, british_youtube])
		needs to have same fields
	join() --> horizontal stack
	left.join(right, lsuffix='_CAN', rsuffix='_UK')
		


	

	
	