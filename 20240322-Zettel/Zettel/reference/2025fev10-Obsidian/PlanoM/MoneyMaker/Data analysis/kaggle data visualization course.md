https://www.kaggle.com/alexisbcook/hello-seaborn

import seaborn as sns

fifa_data = pd.read_csv(filepath, 
		index_col="Date", 
		parse_dates=True)


plt.figure(figsize=(16,6))
sns.lineplot(data=fifa_data)

https://www.kaggle.com/alexisbcook/line-charts
plt.title("Daily Global Streams of Popular Songs in 2017-2018")
sns.lineplot(data=spotify_data)

plot subsets (columns): 
sns.lineplot(data=spotify_data['Shape of You'], label="Shape of You")
sns.lineplot(data=spotify_data['Despacito'], label="Despacito")


https://www.kaggle.com/alexisbcook/bar-charts-and-heatmaps
bar chart:
sns.barplot(x=flight_data.index, y=flight_data['NK'])

Heatmap:
sns.heatmap(data=flight_data, annot=True)

https://www.kaggle.com/alexisbcook/scatter-plots

basic scatterplot:
sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'])

regression line scatterplot:
sns.regplot(x=insurance_data['bmi'], y=insurance_data['charges'])

color-coded scatterplot
sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'], hue=insurance_data['smoker']) # hue is categorical feature

regression line for each category group:
sns.lmplot(x="bmi", y="charges", hue="smoker", data=insurance_data)

swarm plot for category aggregation
sns.swarmplot(x=insurance_data['smoker'],
              y=insurance_data['charges'])       

https://www.kaggle.com/alexisbcook/distributions

Histograms:
sns.distplot(a=iris_data['Petal Length (cm)'], kde=False)
kde = false --> leaving out will make it slightly different

Density Plot:
sns.kdeplot(data=iris_data['Petal Length (cm)'], shade=True)
kde = kernel density estimate --> smoothed histogram

2d KDE plot:
--> 2d plot --> get tyo see likeliness of different combinations of x + y and density probabilitiues per axes
sns.jointplot(x=iris_data['Petal Length (cm)'], y=iris_data['Sepal Width (cm)'], kind="kde")

Color-coded plots: --> multiple histograms each with own color:
sns.distplot(a=iris_set_data['Petal Length (cm)'], label="Iris-setosa", kde=False)
sns.distplot(a=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", kde=False)
sns.distplot(a=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", kde=False)
plt.legend()

multiple KDE density plots:
sns.kdeplot(data=iris_set_data['Petal Length (cm)'], label="Iris-setosa", shade=True)
sns.kdeplot(data=iris_ver_data['Petal Length (cm)'], label="Iris-versicolor", shade=True)
sns.kdeplot(data=iris_vir_data['Petal Length (cm)'], label="Iris-virginica", shade=True)

https://www.kaggle.com/alexisbcook/choosing-plot-types-and-custom-styles

learned so far:
	![[Attachments/Pasted image 20220303205057.png]]

changins styles in seaborn:
sns.set_style("dark")
five different themes: (1)`"darkgrid"`, (2)`"whitegrid"`, (3)`"dark"`, (4)`"white"`, and (5)`"ticks"`

https://www.kaggle.com/alexisbcook/final-project
--> https://www.kaggle.com/fivethirtyeight/fivethirtyeight-comic-characters-dataset
--> choose your dataset at: https://www.kaggle.com/datasets


https://www.kaggle.com/alexisbcook/creating-your-own-notebooks
--> https://www.kaggle.com/code
import pandas as pd
pd.plotting.register_matplotlib_converters()
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
print("Setup Complete")
