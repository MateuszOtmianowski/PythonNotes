# PythonNotes

General:
- use "for index,a in enumerate(areas)" to get elements from a list with corresponding indexes, for dictionaries use dict.items();
- to open files open('file_name.csv','r') function is used, it take two arguments: file name and read mode, the function creates object of a File class; 
- File objects have a read() method that returns a string representation of the text in a file, it is method so it is used as file.read();
- split() method turns a string into a list of strings, the method takes a string input corresponding to the delimiter, or separator. This delimiter determines how the string is split into elements in a list;
- csv module is useful for importing csv files, use then data=list(csv.reader(open('file_name.csv','r')))
- list comprehension: apple_prices_doubled=[2*apple_price for apple_price in apple_prices] <- it doubles every apple price in the apple_prices list and creates the list out of it;
- to find the biggest value in a list it is safer to assign value None to the comparison variable then for example 0 as in following example: 
        max_value = None
        for i in values:
            if max_value is None or i > max_value:
            max_value = i
- Comparing a value to None will usually cause an error. When the Python interpreter evaluates a Boolean statement that contains or, like 'max_value is None or i > max_value', it will evaluate the statements in order. If the first statement is True, it won't evaluate the second statement. This is to save time, since if one statement is True, the whole or conditional is True.
- Scientific notation is a way to condense how very large or very precise numbers are displayed. We can represent 100 in scientific notation as 1e+02. The e+02 indicates that we should multiply what comes before it by 10 ^ 2(10 to the power 2, or 10 squared). This results in 1 * 100, or 100. Thus, 1.98600000e+03 is actually 1.986 * 10 ^ 3, or 1986. 1000000000000000 can be written as 1e+15;

Visualisation:
- pyplot is used for data visualisation, it is a part of matplotlib package;
- to import it use: import matplotlib.pyplot as plt;
- plt.plot(x,y) is used for a line plot, you must then, as a general rule, use plt.show() to display the plot;
- plt.scattter(x,y) is used for scatter plots;
- plt.xscale('log') changes x-axis to logarithimc scale;
- plt.hist(x) creates histogram, the default number of bins is 10, you can change this value with the bins argument;
- plt.clf() cleans plot;
- plt.xlabel() sets label for a x-axis, y-axis use ylabel();
- plt.title() creates a title for a plot;
- plt.yticks([0,1,2], ["one","two","three"]) sets step on a y-axis, second argument sets names of ticks;
- plt.scatter(gdp_cap, life_exp, s = pop) s argument stands for size of dots, additional arguments include c for color, and alpha for transparency (as in ggplot value from 0 to 1);
- plt.grid() creates grid lines;
- Seaborn is a Python library supported by Stanford University that enables you to create beautiful, presentation-ready data visualizations. If seaborn is imported into enviroment it overrides default styles. To import it use 'import seaborn as sns';
- .distplot() is equivalent of .hist() from matplotlib, set kde parameter to False to generate standard, binned histogram;
- When working with Seaborn plots, we recommend using sns.plt.show() instead of plt.show() to display the plot;
- API reference for Seaborn can be found here: https://stanford.edu/~mwaskom/software/seaborn/api.html#style-frontend;
- Instead of comparing relationships between variables by generating one chart for each combination of variables we're exploring, we can use a Seaborn pairplot() to automatically visualize all combinations of variables from columns in a DataFrame;

Dictionaries:
- dictionary.keys() gets keys from a dictionary;
- del(dictionary['key']) deletes given key;

Pandas:
- the DataFrame is one of Pandas' most important data structures. It's basically a way to store tabular data, where you can label the rows and the columns;
- use 'import pandas as pd' to import;
- data_frame.head() returns first 5 rows, n arguments specifies how many rows will be displayed;
- you can use the shape attribute to understand the dimensions of the DataFrame. The shape attribute returns a tuple of integers representing the number of rows followed by the number of columns;
- data frame can be created from the dictionary with variables defined in different keyes ex. 'year':[x,x,x,x,x], 'pop':[x,x,x,x,x], use pd.DataFrame(my_dict) for transformation;
- 'df.index=row_labels' sets row labels to names specified in custom row_labels, DO NOT use () after the index;
- pd.read_csv(file_name) reads in csv file, index_col argument is used to specify which column in the CSV file should be used as a row label;
- columns can be selected as pandas series with single brackets ex. df['col'] or as a data frame with double brackets i.e. df[['col']];
- rows can be selected as a slice with df[0:3], only as integer values corresponding to rows, naming rows by index (df[1,2,3]) does not work;
- for more advanced filtering use loc and iloc, the basic difference between the two is that in loc we use column names, and in iloc column indexes;
- df.loc[['X1','X2']] selects columns x1 and x2 as a data frame;
- cars.loc[['RU','MOR'],['country','drives_right']] selects rows RU i MOR, and columns 'country' and 'drives_right' from cars data frame;
- print(cars.loc[:, ['X1']]) prints all rows and column X1 as a data frame, more columns can be specified alongside X1; 
- numpy can be used to filter values in columns, you must create boolean panadas series to do it, ex. df[df['col1']>100];
- cars[np.logical_and(cars['cars_per_cap']>100,cars['cars_per_cap']<500)];
- looping through pandas data frame is done with "for lab, row in brics.iterrows():";
- for lab, row in cars.iterrows():
    cars.loc[lab,"COUNTRY"]=row['country'].upper() <- creates new column (upper letter version of country column), cars['COUNTRY']=cars['country'].apply(str.upper) is equivalent and more efficient;
- While there are many ways to normalize data, one of the simplest ways is to divide all of the values in a column by that column's maximum value. This way, all of the columns will range from 0 to 1. To calculate the maximum value of a column, use the Series method max();
- The pivot_table method borrows it's name from pivot tables in Excel and it works in a similar way, ex. titanic_survival.pivot_table(index="pclass", values="survived", aggfunc=np.mean) or titanic_survival.pivot_table(index="pclass", values=["age", "survived"], aggfunc=np.mean);
- Using the 'dropna' method will drop any rows that contain missing values. We can use the subset argument to only drop rows if certain columns have missing value ex. new_titanic_survival = titanic_survival.dropna(subset=["age", "sex"]);
- .iloc works by position (row/column number), .loc instead addresses rows and columns by index, not position, i.e. if you delete some rows, loc will be returning rows by their original indexes;
- reset_index() method recalculates indexes so they begin from 0, useful if index numbers are distored by for example 'dropna' method, The drop keyword argument specifies whether or not to make a dataframe column with the index values. If True, it won't, if False, it will. We'll almost always want to set it to True;
- By default, .apply() will iterate through each column in a dataframe, and perform a function on it. The column will be passed into the function. The result from the function will be combined with all of the other results, and placed into a new series ex. titanic_survival.apply(function). By passing in the axis argument, we can use the .apply() method to iterate over rows instead of columns ex. titanic_survival.apply(function, axis=1);
- use item() method to get given element from data frame, useful for comparisons. ex. all_ages[all_ages['Major']==m]['Unemployment_rate'].item();
- value_counts() method returns object containing counts of unique values ex. recent_grads['Major'].value_counts(), you can use index to get the categories, ex. recent_grads['Major'].value_counts().index;
- Reindexing is the Pandas way of modifying the alignment between labels (index) and the data (values). The reindex() method allows you to specify an alternate ordering of the labels (index) for a Series object. This method takes in a list of strings corresponding to the order of labels you'd like for that Series object;
- Pandas comes with a sort_index() method, which returns a Series sorted by the index, and a sort_values() method method, which returns a Series sorted by the values;
- There are many cases where you want to transform an entire column in a dataset, since a column is really a vector of values. Series objects have powerful support for vectorized operations, which enable you to run computations over an entire column incredibly quickly. Since Pandas builds on top of NumPy, it takes advantage of NumPy's vectorizaton capabilities which generates incredibly optimized, low level C code (C is another programming language) to loop over the values instead. Using a for loop to iterate over the values in a Series object to run item-wise computations is much slower, especially for larger datasets. You can use any of the standard Python arithmetic operators (+, -, *, and /) to transform every value in a Series object. For example, if we wanted to transform the Rotten Tomatoes scores from a 0 to 100 point scale to a 0 to 10 scale, we can use the Python / division operator to divide the Series by 10: 'series_custom/10' and we'll get back a new Series object with each value divided by 10. We can even use NumPy functions to transform and run calculations over Series objects: '# Add each value with each other
np.add(series_custom, series_custom)
# Apply sine function to each value
np.sin(series_custom)
# Return the highest value (will return a single value not a Series)
np.max(series_custom)'. The values in a Series object are treated as an ndarray, the core data type in NumPy. Applying some NumPy functions will return a new Series object while others will return just a single value. NumPy's documentation gives you a good sense of the return value for each function. If a particular NumPy function usually returns an ndarray, it will instead return a Series object when applied to a Series;
- The DataFrame object contains a set_index() method that allows you to pass in the name of the column you'd like Pandas to use as the index for the DataFrame. Pandas, by default, will return a new DataFrame that is indexed by the values in the specified column and will drop that column from the DataFrame. The set_index() method contains a few parameters to tweak this behavior: inplace: if set to True, will set the index to the current DataFrame instead of returning a new one; drop: if set to False, will keep the column you specified for the index in the DataFrame;
- apply for rows in df rt_mt_means=rt_mt_user.apply(lambda x: np.mean(x), axis=1);

Numpy boolean operators:
- the operational operators like < and >= work with Numpy arrays out of the box. Unfortunately, this is not true for the boolean operators and, or, and not. To use these operators with Numpy, you will need np.logical_and(), np.logical_or() and np.logical_not();
- ex. logical_and(my_house<11,your_house<11);
- to iterate through 1D numpy array use "for x in my_array:", for 2D numpy array "for x in np.nditer(my_array):";

Data analysis:
- titanic['Age'].fillna(titanic['Age'].median()) <- replaces nans with median for the column;
- .unique() returns unique values;

re module and regular expressions:
- The special character "." is used to indicate that any character can be put in its place;
- We can use "^" to match the start of a string and "$" to match the end of string. "^a" will match all strings that start with "a". "a$" will match all strings that end with "a";
- With re.search(regex, string), we can check if string is a match for regex. If it is, it will return a match object. If it isn't, it will return None;
- the regular expression "[bcr]at" would be matched by strings with the substrings "bat", "cat", and "rat", but nothing else. We indicate that the first character in the regular expression can be either a "b", "c" or "r";
- In regular expressions, escaping a character means indicating that you don't want the character to do anything special, and that it should be treated as any other character would be. We use "\" (backslash) to escape characters in regular expressions;
- To combine regular expressions, we use the "|" character. For example, "cat|dog" would be matched by "catfish" and "hotdog", since both these strings match either "cat" or "dog";
- The re module provides a sub() method that takes the following parameters (in the following order): 1. pattern - The regular expression to match, 2. repl    - The string to replace the matched substring with, 3. string  - The string in which we would like to replace occurrences of the pattern with repl. So, if we were to call re.sub("yo", "hello", "yo world"), the function will replace "yo" with "hello" in "yo world", producing the result "hello world". The sub() function simply returns the original string if pattern is not found;
- years could be searched as follows "[0-9][0-9][0-9][0-9]";
- using curly brackets ("{" and "}"), we can indicate that a pattern should repeat. If we were matching any 4-digit number, we could repeat the pattern "[0-9]" 4 times by writing "[0-9]{4}";
- findall() returns a list of substrings that match the provided regular expression. re.findall("[a-z]", "abc123") would return ["a", "b", "c"], since those are the substrings that match the regular expression;

##'time' module
- The time module deals primarily with Unix timestamps. A Unix timestamp is a simple floating point value, with no explicit mention of day, month, or year. This floating point value represents the number of seconds that have passed since the epoch. The epoch is the first second of the year 1970. So, a timestamp of 0.0 would represent the epoch, and a timestamp of 60.0 would represent one minute after the epoch. Any date after 1970 can be represented this way;
- To get the Unix timestamp for the current time, we use the time() function within the time module;
- We can convert a timestamp to a more human-readable form using the gmtime() function within the time module. The gmtime() function takes a timestamp as an argument, and returns an instance of the struct_time class. Each struct_time instance has some properties that represent the current time. The following integer values are just a few of these properties:
        - tm_year: The year of the timestamp
        - tm_mon: The month of the timestamp (1-12)
        - tm_mday: The day in the month of the timestamp (1-31)
        - tm_hour: The hour of the timestamp (0-23)
        - tm_min: The minute of the timestamp (0-59)
- the time module deals primarily with timestamps in UTC. The datetime module has better support for working extensively with dates. With datetime, it is easier to work with different time zones and perform arithmetic (adding days, for example) on dates;
- The datetime module contains a datetime class to represent points in time. datetime instances look similar to struct_time instances, and have the following properties: year, month, day, hour, minute, second, microsecond. To get the datetime instance representation of the current time, the datetime class has a now() class method. Class methods are called on the class itself, so we would write datetime.datetime.now() to create a datetime instance representing the current time. The first datetime is the module, .datetime is the class, and .now() is the class method;
- We know how to represent dates, but we'd also like to perform arithmetic on dates. Since adding a day, week, month, etc. to a date can be tedious to do from scratch, the datetime module provides the timedelta class. We can create an instance of the timedelta class that represents a span of time. Then we can add or subtract it from instances of the datetime class ex. diff = datetime.timedelta(weeks = 3, days = 2);
- strftime() takes a formatted string as its input. Format strings contain special indicators, usually preceded by a "%" character, that indicate where a certain value should go. march3 = datetime.datetime(year = 2010, month = 3, day = 3) /n pretty_march3 = march3.strftime("%b %d, %Y") /n
- Just as we can convert a datetime object into a formatted string, we can also convert a formatted string into a datetime object. The datetime class (datetime.datetime) contains a class method called strptime() which takes two arguments: the date string (e.g. "Mar 03, 2010"), the format string (e.g. "%b %d, %Y") ex. datetime.datetime.strptime("Mar 03, 2010", "%b %d, %Y");
- datetime.datetime.fromtimestamp() is used to convert the Unix timestamp to a datetime;

Numpy:
- to read in dataset use genfromtxt(), we need to pass a keyword argument called delimiter that indicates what character is the delimiter ex. np.genfromtxt('world_alcohol.csv',delimiter=','), use dtype argument to specify data type, use 'U75' for diverse data types, additionally setting 'skip_header' will skip the first row;
- we can directly construct arrays from lists using the array() method;
- we can use the shape property on arrays to figure out how many elements are in an array. For vectors, the shape property contains a tuple with 1 element. A tuple is a kind of list where the elements can't be changed;
- Each value in a NumPy array has to have the same data type. You can check the data type of a NumPy array using the dtype property;
- indexing arrays is done in the [row, column] format, the colon by itself : specifies that the entirety of a single dimension should be selected. Think of the colon as selecting from the first element in a dimension up to and including the last element;
- these two statements are equivalent world_alcohol[world_alcohol[:,3]=='Wine',3]='Grog' and world_alcohol[world_alcohol=='Wine']='Grog';
- We can convert the data type of an array using the astype() method. Here's an example: vector = numpy.array(["1", "2", "3"]) /n
vector = vector.astype(float);
- NumPy has a few built-in methods that operate on arrays, ex. sum(), mean(), max(). With a matrix, we have to specify an additional keyword argument axis. The axis dictates which dimension we perform the operation on. 1 means that we want to perform the operation on each row, and 0 means on each column;
