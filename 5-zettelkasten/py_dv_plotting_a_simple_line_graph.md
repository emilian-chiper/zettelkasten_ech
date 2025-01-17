### Meta
2025-01-06 11:36
**Tags:** [[python]] [[py_projects]] [[py_data_visualization]]
**Status:** #completed 

### Plotting a Simple Line Graph
Let’s plot a simple line graph using Matplotlib and then customize it to createa more informative data visualization. We’ll use the square number sequence 1, 4, 9, 16, and 25 as the data for the graph.

To make a simple line graph, specify the numbers you want to work with and let Matplotlib do the rest:
```Python title:mpl_squares.py
import matplotliub.pyplot as plt

squares = [1, 4, 9, 16, 25]

fig, ax = plt.subplots()
ax.plot(squares)

plt.show()
```

We first import the `pyplot` module and assign it the alias `plt`. The module contains a number of functions that help generate charts and plots.
We then create a list of `squares` to hold the data that we’ll plot. Then we call the `sublplots()` function, which can generate one or more plots in the same figure. The variable `fig` represents the entire *figure*, which is the collection of plots that are generated. The variable `ax` represents a single plot in the figure;' this is the variable we’ll use most of the time when defining and customizing a single plot.
We then use the `plot()` method, which tries to plot the data it’s given in a meaningful way. The function `plt.show()` opens Matplotlib’s viewer and displays the plot.

**Note**: On Linux, install a GUI library as follows:
```BASH title:example.sh
sudo apt install python3-tk
```

Then change the script:
```Python title:mpl_squares.py
import matplotlib
matplotlib.use('TkAgg')  # Use TkAgg for interactive plots
import matplotlib.pyplot as plt

squares = [1, 4, 9, 16, 25]

fig, ax = plt.subplots()
ax.plot(squares)

plt.show()
```

#### Changing the Label Type and Line Thickness
We’ll use a few of the available customization options to improve this plot’s readability. We’ll ad a title and labeling the axes:
```Python title:mpl_squares.py
import matplotlib
matplotlib.use('TkAgg')  # Use TkAgg for interactive plots
import matplotlib.pyplot as plt

squares = [1, 4, 9, 16, 25]

fig, ax = plt.subplots()
ax.plot(squares, linewidth=3)

# Set chart title and label axes.
ax.set_title("Square Numbers", fontsize=24)
ax.set_xlabel("Value", fontsize=14)
ax.set_ylabel("Square of Value", fontsize=14)

# Set size of tick labels.
ax.tick_params(labelsize=14)

plt.show()
```

The `linewidth` parameter controls the thickness of the line that `plot()` generates. Once a plot has been generated, there are many methods available to modify the plot before it’s presented. The `set_title()` method sets an overall title for the chart. The `fontsize` parameters, which appear repeatedly throughout the code, control the size of the text in various elements of the chart.

The `set_xlabel()` and `set_ylabel()` methods allow you to set a title for each of the axes, and the method `tick_params()` styles the tick marks. Here `tick_params()` sets the font size of the tick mark labels to 14 on both axes.

#### Correcting the Plot
Now that we can read the chart better, we can see that the data is not plotted correctly. Notice at the end of the graph that the square of `4.0` is shown as `25`.

When you give `plot()` a single sequence of numbers, it assumes the first data point corresponds to an *x*-value of `0`, but our first point corresponds to an *x*-value of `1`. We can override the default behavior by giving `plot()` both the input and the output values used to calculate the squares:
```Python title:mpl_squares.py
--snip--
import matplotlib.pyplot as plt

input_values = [1, 2, 3, 4, 5]
squares = [1, 4, 9, 16, 25]

fig, ax = plt.subplots()
ax.plot(input_values, squares, linewidth=3)

# Set chart title and label axes.
--snip--
```

#### Using Built-in Styles
Matplotlib has a number of predefined styles available. These contain a variety of default settings for background colors, grid lines, line widths, fonts, font sizes, and more.

To use any of the styles:
```Python title:mpl_squares.py
--snip--
squares = [1, 4, 9, 16, 25]

plt.style.use('seaborn-v0_8-notebook')
fig, ax = plt.subplots()
```

#### Plotting and Styling Individual Points with `scatter()`
Sometimes, it’s useful to plot and style individual points based on certain characteristics. For example, you might plot small values in one color and larger values in a different color. You could also plot a large dataset with one set of styling options and then emphasize individual points by re-plotting them with different options.

To plot a single point, pass a single *x*- and *y*-vlaues of the point to `scatter()`:
```Python title:scatter_squares.py
import matplotlib
matplotlib.use('TkAgg') 
import matplotlib.pyplot as plt

plt.style.use('seaborn-v0_8-notebook')
fig, ax = plt.subplots()
ax.scatter(2, 4)

plt.show()
```

Let’s style the output to make it more interesting. We’ll add a title, label the axes, and make sure all the text is large enough to read:
```Python title:scatter_squares.py
import matplotlib
matplotlib.use('TkAgg') 
import matplotlib.pyplot as plt

plt.style.use('seaborn-v0_8-notebook')
fig, ax = plt.subplots()
ax.scatter(2, 4, s=200)

# Set chart title and label axes.
ax.set_title("Square Numbers", fontsize=24)
ax.set_xlabel("Value", fontsize=14)
ax.set_ylabel("Square of Value", fontsize=14)

# Set size of tick labels.
ax.tick_params(labelsize=14)

plt.show()
```

#### Plotting a Series of Points with `scatter()`
To plot a series of points, we can pass `scatter()` separate lists of *x*- and *y*-values, like so:
```Python title:scatter_squares.py
import matplotlib
matplotlib.use('TkAgg') 
import matplotlib.pyplot as plt

x_values = [1, 2, 3, 4, 5]
y_values = [1, 4, 9, 16, 25]

plt.style.use('Solarize-Light2')
fig, ax = plt.subplots()
ax.scatter(x_values, y_values, s=100)

# Set chart title and label axes.
--snip--
```

The `x_values` list contains the numbers to be squared, and the `y_values` contains the square of each number. When these are passed to `scatter()`, Matplotlib reads one value from each list as it plots each point. The plotted points become (1, 1), (2, 4), (3, 9), (4, 16), (5, 25).

#### Calculating Data Automatically
Writing lists by hand can be inefficient, especially when we have many points. Rather than writing out each value, let’s use a loop to do the calculations for us. Here’s how this would look with 1,000 points:
```Python title:scatter_squares.py
import matplotlib
matplotlib.use('TkAgg') 
import matplotlib.pyplot as plt

x_values = range(1, 1001)
y_values = [x**2 for x in x_values]

plt.style.use('Solarize-Light2')
fig, ax = plt.subplots()
ax.scatter(x_values, y_values, s=10)

# Set chart title and label axes.
--snip--

# Set range for each axis.
ax.axis([0, 1100, 0, 1_100_000])

plt.show()
```

We start with a range of *x*-values containing the numbers 1 through 1,000. Next, a list comprehension generates the *y*-values by looping through the *x*-values (`for x in x_values`), squaring each number (`x**2`), and assigning the results to `y_values`. We then pass the input and output lists to `scatters()`. Because this is a large dataset, we use a smaller point size.

Before showing the plot, we use the `axis()` method to specify the range of each axis. The `axis()` method requires four values: the minimum and maximum values for the *x*-axis and the *y*-axis. Here, we run the *x*-axis from 0 to 1,100 and the *y*-axis from 0 to 1,100,000.

#### Customizing Tick Labels
When the numbers on an axis get large enough, Matplotlib defaults to scientific notation for tick labels. This is usually a good thing, because larger numbers in plain notation take up a lot of unnecessary space on a visualization.

Almost every element of a chart is customizable, so you can tell Matplotlib to keep using plain notation if you prefer:
```Python title:scatter_squares.py
--snip--
# Set the range for each axis.
ax.axis[0, 1100, 0, 1_100_000]
ax.ticklabel_format(style='plain')

plt.show()
```

The `ticklabel_format()` method allows you to override the default tick label style for any plot.

#### Defining Custom Colors
To change the colors of the points, pass the argument `color` to `scatter()` with the name of a color to use in quotation marks, as shown here:
```Python title:scatter_squares.py
ax.scatter(x_values, y_values, color='red', s=10)
```

You can also define custom colors using the RGB color model. To define a color, pass the `color` argument a tuple with three float values (one each for red, green, and blue, in that order), using values between 0 and 1. For example, the following line creates a plot with light-green dots:
```Python title:scatter_squares.py
ax.scatter(x_values, y_values, color=(0, 0.8, 0), s=10)
```

Values closer to 0 produce darker colors, and values closer to 1 produce lighter colors.

#### Using a Colormap
A *colormap* is a sequence of colors in a gradient that moves from a starting to an ending color. In visualizations, colormaps are used to emphasize the patterns in data. For example, you might make low values a light color and high values a darker color. Using a colormap ensures that all points in the visualizations vary smoothly and accurately along a well-designed color scale.

The `pyplot` module includes a set of built-in colormaps. To use one, you must specify how `pyplot` should assign a color to each point in the dataset, like so:
```Python title:scatter_squares.py
--snip-
plt.style.use('Solarize-Light2')
fig, ax = plt.subplots()
ax.scatter(x_values, y_values, c=y_values, cmap=plt.cm.Blues, s=10)

# Set chart title and label axes.
--snip--
```

The `c` argument is similar to `color`, but it’s used to associate a sequence of values with a color mapping. We pass the list of *y*-values to `c`, and then tell `pyplot` which colormap to use with the `cmap` argument. This code colors the points with lower *y*-values light blue and the points with higher *y*-values dark blue.

#### Saving Your Plots Automatically
If you want to save the plot to a file, use the command bellow instead of `plt.show()`:
```Python title:example.py
plt.savefig('squares_plot.png', bbox_inches='tight')
```