Amazon offers services for the sale of things. 
It is required to create a dictionary `dict: actions`, where keys will be names of keys from both __TASK 2.1 and TASK 2.2__. 
The values in this dictionary will be references to functions that perform actions on their keys in the `FeatureTransformation` class.

_ANSWER_:

![alt tag](images/Picture1.png)

### Task 3
Implement the `DataParser` class, whose constructor takes two values:
* `path_to_json`
* `number_of_lines` - the number of lines to read from the file.

Write a code in the `data_processing.py` module.

#### Task 3.1
Implement the `get_data_iterator(...)` method, which takes the same parameters as the constructor.
In the body of the method, you need to check for the existence of the passed file path. 
If such a path does not exist, then an Exception should be raised with the message __("Incorrect path")__.
If the path exists, this method should be able to open a json file and read information from line by line. 
In this case, each line must be returned by the yield statement, thereby you implement an iterator function.

#### Task 3.2
Implement an method-iterator that accepts a dictionary from json and name of key.
If a given key contains nesting in the dictionary, for example, a non-empty list then on its basis you need to create a set of new dictionaries that differ only in the value in the passed key containing nesting and return one at a time by the yield statement.
If the given key is not in the dictionary, then it is required to return the original dictionary with the yield statement.

__EXAMPLE__:

_FROM_
![alt tag](images/Picture2.png)

_TO_
![alt tag](images/Picture3.png)


#### Task 3.3
Implement the `upload_data(...)` method, that takes the key for the method-iterator from __TASK 3.2__ as well as a list of keys whose values ​​you want to update (to methods __FROM TASKS 2__). 
In the body of the method you need to create a loop based on the iterator method __(TASK 3.1)__ passing in the attributes initialized in the class constructor.

Then create a nested loop based on the method-iterator  __(TASK 3.2)__ passing in the read lines from the outer loop, as well as the key used to get rid of nested data.
Inside this loop you need to create another one by iterating over the list of keys from the second argument of the `upload_data` method.
If the key is in the dictionary, then convert his value based on the key / values ​​of the `actions` dictionary.
Otherwise, this line will remain unchanged.

Each line must be iteratively added to a class attribute.
The method shouldn't return anything it only writes to the attribute.


#### Task 3.4
Implement the `to_DF()` method, which translates the content of the attribute created by method from __(TASK 3.3)__ to the pandas DataFrame.

__PROMPT:__ you can use the `pandas.DataFrame.to_dict` method.


#### Task 3.5
Implement the `save_data()` method, which takes the name of the file where you want to save the converted data from __(TASK 3.4)__.
In this case, if the name and format of the file for saving is not specified, then by default the data should be saved in __"data.json"__.
This method must support saving in the __"json"__, __"csv"__, __"pickle"__ formats.