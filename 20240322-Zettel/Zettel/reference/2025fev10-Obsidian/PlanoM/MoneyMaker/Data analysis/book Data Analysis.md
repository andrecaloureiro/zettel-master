
### Author: Fabio Nelli
#### cap3: Numpy Library
- the ndarray:
	- N-dimensional array). 
	- This object is a multidimensional homogeneous array with a predetermined number of items: 
		* homogeneous because virtually all the items in it are of the same type and the same size. each ndarray is associated with only one type of dtype. 
		* The number of the dimensions and items in an array is defined by its **shape**, 
		* a tuple of N-positive integers that specifies the **size** for each dimension. 
		* The dimensions are defined as **axes** 
		* and the number of axes as **rank**.

a = np.array([1, 2, 3])
	-type(a)
	- a.dtype
	- >>> a.ndim 1 >>> a.size 3 >>> a.shape (3,)

- ndarray accepts
	- list or list of lists
	- tuples and its sequences
	- interconnected lists and tuples

- Intrinsic Creation of an Array:
	- np.zeros((3, 3))
	- np.ones((3, 3))
	- np.arange(0, 12, 3)
		- .reshape(3, 4)
	- np.linspace(0,10,5)
	- np.random.random((3,3)



#### cap2: Intro to Python World
 - Data structures:
	 - List
	 - Set
	 - Strings
	 - Tuples
	 - Dictionary
		 - for key, value in dict.items(): 
			 - ... print(key,value)
	 - Deque
	 - Heap

- Functional Programming
	- map(function, list)
	- filter(function, list)
	- reduce(function, list)
	- lambda
	- list comprehension

- Python IDES
	- Spyder
	- Eclipse ( pyDev)
	- Sublime
	- Liclipse
	- NinjaIDE
	- KomodoIDE


#### cap 1: Intro 
![[Attachments/Pasted image 20220222171541.png]]


![[Attachments/Pasted image 20220222171912.png]]

- Open Data:
	- DataHub (http://datahub.io/dataset) • 
	- World Health Organization (http://www.who.int/research/en/) 
	-  Data.gov (http://data.gov) • 
	- European Union Open Data Portal (http://open-data.europa.eu/ en/data/) • 
	- Amazon Web Service public datasets (http://aws.amazon.com/ datasets) • 
	- Facebook Graph (http://developers.facebook.com/docs/graph-api)
	- Healthdata.gov (http://www.healthdata.gov) • 
	- Google Trends (http://www.google.com/trends/explore) • 
	- Google Finance (https://www.google.com/finance) • 
	- Google Books Ngrams (http://storage.googleapis.com/books/ ngrams/books/datasetsv2.html) • 
	- Machine Learning Repository (http://archive.ics.uci.edu/ml/) 
	- As an idea of open data sources available online, you can look at the LOD cloud diagram (http://lod-cloud.net),
	- 