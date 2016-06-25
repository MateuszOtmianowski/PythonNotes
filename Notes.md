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
- 
