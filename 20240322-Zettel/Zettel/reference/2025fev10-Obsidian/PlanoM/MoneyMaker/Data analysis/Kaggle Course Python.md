https://www.kaggle.com/colinmorris/hello-python


https://www.kaggle.com/colinmorris/functions-and-getting-help

help()

docstrings to offer help in a funciotn:
	def least_difference(a, b, c):
	"""
	 Return the smallest difference between any two numbers
	 among a, b and c.
	least_difference(1, 5, -5)
	 4
	 """

default arguments:
	def greet(who="Colin"):
    print("Hello,", who)

supply functions as arguments to other functions:
	def mult_by_five(x):
    return 5 * x
	def call(fn, arg):
    """Call fn on arg"""
    return fn(arg)
	print(   call(mult_by_five, 1)

the max() funciton has a key= argument that can be used to supply a fucniotn


https://www.kaggle.com/colinmorris/booleans-and-conditionals

the expression:?
	True or True and False
	retuirns true --> and is evaluated before or

bool() function turns thinbgs into bool
	- true for all except 0 and "" ( empty string)

0 = false = ""


https://www.kaggle.com/colinmorris/lists

list function:
	- len(list)
	- sorted(list)]
	- sum(list)
	- max(list)
	- j.imag ( imaginary part of a number)

list methods
	- list.append('item') --> append an item to the end
	- list.pop() --> remove and return last element of a list
	- list.index('listItem') --> returns the index of an  item
		- you may use ```if listItem in list: list.index('listItem')```

tuples:
	the methodf `` floatNumber.as_integer_ratio()`` can  be used to return a tuple withg numerator and de3nomainator in form of a tuple 


https://www.kaggle.com/colinmorris/loops-and-list-comprehensions

for planet in planets:
    print(planet, end=' ') # print all on same line

range()
	for i in range(5):
    print("Doing important work. i =", i)

`while` loops

List compreension
	`squares = [n**2 for n in range(10)]`
	funciton example:
	`def count_negatives(nums):
	    `return len([num for num in nums if num < 0])`

any() function

https://www.kaggle.com/colinmorris/strings-and-dictionaries

String Syntax:
	x = 'Pluto is a planet'
	y = "Pluto is a planet"
	escape char : \''
	print('string goes here', end='')

strings as sequences:
	[char+'! ' for char in planet]
	strings are immutable

string methods:
	string.upper()
	string.lower()
	string.index(substring)
	string.startswith(substring)
	string.endswith(substring)

strings and lists:
	split() --> string_list_of_words = string.split(' ') --> default break on whitespace
	join() --> '/'.join([sub1, sub2, sub3])

Build strings with .format()
	"{}, will always be the {}th planet to me".format(sub1,sub2)
	number formatting:
		{:.2% } --> 2 decimasl + percent sign
		{:,} --> use comma to divide bloks of 3 numbers
	index reference:
		'string can be called with {0}st element and then {1}nd. again,{0}st element and then {1}nd '.format('1','2')

Dictionaires:
	map keys to values:
		numbers = {'one':1, ''two":2, 'three':3}
	adding elements:
		numbers['eleven'] = '11'

in operator checks if key is in dictionarire:
	'one' in numbers ---> True
--> using format on strings:
	https://pyformat.info/

methods for dictionaires:
	items() --> for word, number in numbers.items()
	keys() --> for word in numbers.keys()
	values() --> for numb in numbers.values()

https://www.kaggle.com/colinmorris/working-with-external-libraries



dir(var)
type(var)
help (var)

	
	
	