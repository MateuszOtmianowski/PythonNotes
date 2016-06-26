# PythonNotes

Visualisation:
- pyplot is used for data visualisation, it is a part of matplotlib package;
- to import it use: import matplotlib.pyplot as plt;
- plt.plot(x,y) is used for a line plot, you must then, as a general rule, use plt.show() to display the plot;
- plt.scattter(x,y) is used for scatter plots;
- plt.xscale('log') changes x-axis to logarithimc scale;
- plt.hist(x) creates histogram, a default number of bins is 10, you can change this value you can specify bins argument;
- plt.clf() cleans plot;
- plt.xlabel() sets label for a x-axis, y-axis use ylabel();
- plt.title() creates a title for a plot;
- plt.yticks([0,1,2], ["one","two","three"]) sets step on a y-axis, second argument sets names of ticks;
- plt.scatter(gdp_cap, life_exp, s = pop) s argument stands for size of dots, additional arguments include c for color, and alpha for transparency (as in ggplot value from 0 to 1);
- plt.grid() creates grid lines;

Dictionaries:
- dictionary.keys() gets keys from a dictionary;
- del(dictionary['key']) deletes given key;

Pandas:
- the DataFrame is one of Pandas' most important data structures. It's basically a way to store tabular data, where you can label the rows and the columns;
- import pandas as pd it does what it says ;);
- data frame can be created from the dictionary with variables defined in different keyes ex. 'year':[xxxxx], 'pop':[xxxx], use pd.DataFrame(my_dict) for transformation;
- cars.index=row_labels sets row labels to names specified in row_labels, DO NOT use () after the index;
- pd.read_csv(file_name) reads in csv file, index_col argument is used to specify which column in the CSV file should be used as a row label;
- columns can be selected as pandas series with single brackets ex. df['col'] or as a data frame with double brackets i.e. df[['col']];
- rows can be selected as a slice with df[0:3], only as integer values corresponding to rows, also naming rows by index (df[1,2,3]) does not work;
- for more advanced filtering use loc and iloc, the basic difference between the two is that in loc we use column names, and in iloc column indexes;
- df.loc[['X1','X2']] selects columns x1 and x2 as a data frame;
- cars.loc[['RU','MOR'],['country','drives_right']] selects rows RU i MOR, and columns 'country' and 'drives_right' from cars data frame;
- print(cars.loc[:, ['X1']]) prints all rows and column X1 as a data frame, more columns can be specified alongside X1; 
- numpy can be used to filter values in columns, you must create boolean panas series to do it, ex. df[df['col1'>100]];
- cars[np.logical_and(cars['cars_per_cap']>100,cars['cars_per_cap']<500)];

Numpy boolean operators:
- the operational operators like < and >= work with Numpy arrays out of the box. Unfortunately, this is not true for the boolean operators and, or, and not. To use these operators with Numpy, you will need np.logical_and(), np.logical_or() and np.logical_not();
- ex. logical_and(my_house<11,your_house<11);
- 

