### Meta
2025-01-15 12:37
**Tags:** [[python]] [[py_projects]] [[py_data_visualization]]
**Status:** #completed 

### Rolling Dice with Plotly
In this section, we’ll use Plotly to produce interactive visualizations. Plotly is particularly useful when you’re creating visualizations that will be displayed in a browser, because the visualizations will scale automatically to fit the viewer’s screen.

In this project, we’ll analyze the results of rolling dice. When you roll one regular, six-sided die, you have an equal chance of rolling any of the numbers from 1 through 6. However, when you use two dice, you’re more likely to roll certain numbers than others. We’ll try to determine which numbers are most likely to occur by generating a dataset that represents rolling dice. Then, we’ll plot the results of a large number of rolls to determine which results are more likely than others.

This work helps model games involving dice, but the core ideas also apply to games that involve chance of any kind, such as card games. It also relates to many real-world situations where randomness plays a significant factor.

#### Installing Plotly
Install Plotly using pip, just as you did for Matplotlib.
```Bash title:example.sh
python -m pip install --user plotly
python -m pip install --user pandas
```

Plotly Express depends on *pandas*, a library  for working efficiently with data, so we must install it as well.

#### Creating the Die Class
We’ll create the following `Die` class to simulate the roll of one die:
```Python title:die.py
from random import randint

class Die:
	"""A class representing a single die."""

	def __init__(self, num_sides=6):
		"""Assume a six-sided die."""
		self.num_sides = num_sides

	def roll(self):
		"""Return a random value between 1 and number of sides."""
		return randint(1, self.num_sides)
```

#### Rolling the die
Before creating a visualization based on the `Die` class, let’s roll a D6, print the results, and check that the results look reasonable:
```Python title:die_visual.py
from die import Die

# Create a D6.
die = Die()

# Make some rolls, and store results in a list.
results = []
for roll_num in range(100):
	result = die.roll()
	results.append(result)

print(results)
```

#### Analyzing the Results
We’ll analyze the results of rolling one D6 by counting how many times we roll each number:
```Python title:die_visual.py
--snip--
# Make some rolls, and store results in a list.
results = []
for roll_num in range(1000):
	results = die.roll()
	results.append(result)

# Analyze the results.
frequencies = []
poss_results = range(1, die.num_sides+1)
for value in poss_results:
	frequency = results.count(value)
	frequencies.append(frequency)

print(frequencies)
```

These results look reasonable: we see six frequencies, one for each possible number when you roll a D6. We also see that no frequency is significantly higher than any other.

#### Making a Histogram
Now that we have the data we want, we can generate a visualization in just a couple of lines of code using Plotly Express:
```Python title:die_visual.py
import plotly.express as px

from die import Die
--snip--

for value in poss_results:
	frequency = results.count(value)
	frequencies.append(frequency)

# Visualize the results.
fig = px.bar(x=poss_results, y=frequencies)
fig.show()
```

#### Customizing the Plot
Now that we know we have the correct kind of plot and our data is being represented accurately, we can focus on adding the appropriate labels and styles for the chart.

The first way to customize a plot with Plotly is to use some optional parameters in the initial call that generates the plot, in this case, `px.bar()`. Here’s how to add an overall title and a label for each axis:
```Python title:die_visual.py
--snip--
title = "Results of Rolling one D6 1,000 Times"
labels = {'x': 'Result', 'y': 'Frequency of Results'}
fig = px.bar(x=poss_results, y=frequencies, title=title, labels=labels)
fig.show()
```

We first define the title that we want, here assigned to title. To define axis labels, we write a dictionary. They keys in the dict refer to the labels we want to customize, and the values are the custom labels we want to use. Here we give the *x*-axis the label `Result` and the *y*-axis the label `Frequency of Result`. The call `px.bar()` now includes the optional arguments `title` and `labels`.

#### Rolling Two Dice
Rolling two dice results in larger numbers and a different distribution of results. Let’s modify our code to create two D6 dice to simulate the way we roll a pair of dice. Save a copy of *die_visual.py* as *dice_visual.py*.
```Python title:dice_visual.py
import plotly.express as px

from die import Die

# Create two D6 dice.
die_1 = Die()
die_2 = Die()

# Make some rolls, and store results in a list.
results = []
for roll_num in range(1000):
	result = die_1.roll() + die_2.roll()
	results.append(results)

# Analyze the results.
frequencies = []
max_result = die_1.num_sides + die_2.num_sides
poss_results = range(2, max_result+1)
for value in poss_results:
	frequency = results.count(value)
	frequencies.append(frequency)

# Visualize the results.
title = "Results of Rolling Two D6 Dice 1,000 Times"
labels = {'x': 'Result', 'y': 'Frequency of Result'}
fig = px.bar(x=poss_results, y = frequencies, title=title, labels=labels)
fig.show()
```

#### Further customizations
Now that there are 11 bars, the default layout settings for the *x*-axis leave some of the bars unlabeled. While the default settings work well for most visualizations, this chart would look better with all of the bars labeled.

Plotly has an `update_layout()` method that can be used to make a wide variety of updates to a figure after it’s been created.
```Python title:dice_visual.py
--snip--
fig = px.bar(x=poss_results, y=frequencies, title=title, labels=labels)

# Further customize chart.
fig.update_layout(xaxis_dtick=1)

fig.show()
```

`xaxis_dtick` specifies the distance between tick marks on the *x*-axis, which we set to `1`.

#### Rolling Dice of Different Sizes
Let’s create a six-sided die and a ten-sided die, and see what happens when we roll them 50,000 times.
```Python title:dice_visual_d6d10.py
import plotly.express as px

from die import Die

# Create a D6 and a D10.
die_1 = Die()
die_2 = Die(10)

# Make some rolls, and store results in a list.
results = []
for roll_num in range(50_000):
	result = die_1.roll() + die_2.roll()
	results.append(result)

# Analyze the results.
--snip--

# Visualize the results.
title = "Results of Rolling a D6 and a D10 50,000 Times"
labels = {'x': 'Result', 'y': 'Frequency of Result'}
--snip--
```

#### Saving Figures
When you have a figure you like, you can always save the chart as HTML file through your browser, or programatically, with the `fig.write_html()` method.