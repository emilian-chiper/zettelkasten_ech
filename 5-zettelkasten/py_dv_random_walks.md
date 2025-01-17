### Meta
2025-01-10 11:14
**Tags:** [[python]] [[py_projects]] [[py_data_visualization]]
**Status:** #completed

### Random Walks
In this section, we’ll use Python to generate data for a random walk and then use Matplotlib to create a visually appealing representation of that data. A *random walk* isa a path that’s determined by a series of simple decisions, each of which is left entirely to chance. You might imagine a random walk as the path a confused ant would take if it took every step in a random direction.

Random walks have practical applications in nature, physics, biology, chemistry, and economics. For example, a pollen grain floating ona drop of water moves across the surface of the water because it’s constantly pushed around by water molecules. Molecular motion in a water drop is random, so the path a pollen grain traces on the surface in a random walk. The code we’ll write next models many real-world situations.

#### Creating the RandomWalk Class
To create a random walk, we’ll create a `RandomWalk` class, which will make random decisions about which direction the walk should take. The class needs three attributes: one variable to track the number of points in the walk, and two lists to store the *x*- and *y*-coordinates of each point in the walk.

We’ll only need two methods for the `RandomWalk` class: the `__init__()` method and `fill_walk()`, which will calculate the points in the walk. Let’s start with the `__init__()` method:
```Python title:random_walk.py
from random import choice

class RandomWalk:
	"""A class to generate random walks."""

	def __init__(self, num_points=5000):
		"""Initialize attribues of a walk."""
		self.num_points = num_points

	# All walks start at (0, 0).
	self.x_values = [0]
	self.y_values = [0]
```

To make random decisions, we’ll store possible moves in a list and use the `choice()` function (from the `random` module) to decide which move to make each time a step is taken. We set the default number of points in a walk to `5000`, which is large enough to generate some interesting patterns but small enough to generate walks quickly. Then we make two lists to hold the *x*- and *y*- values, and we start each walk at the point (0, 0).

#### Choosing Directions
We’ll use the `fill_walk()` method to determine the full sequence of points in the walk. Add this method to *random_walk.py*:
```Python title:random_walk.py
	def fill_walk(self):
		"""Calculate all the points in the walk."""
		# Keep taking steps until the walk reaches the desired length.
		while len(self.x_values) < self.num_points:

			# Decide which direction to go, and how far to go.
			x_direction = choice([1, -1])
			x_distance = choice([0, 1, 2, 3, 4])
			x_step = x_direction * x_distance

			y_direction = choice[(1, -1)]
			y_distance = choice([0, 1, 2, 3, 4])
			y_step = y_direction * y_distance

			# Reject moves that go nowhere.
			if x_step == 0 and y_step == 0:
				continue

			# Calculate the new position.
			x = self.x_values[-1] + x_step
			y = self.y_values[-1] + y_step

			self.x_values.append(x)
			self.y_values.append(y)
```

We first set up a loop that runs until the walk is filled with the correct number of points. The main part of `fill_walk()` tells Python how to simulate four random decisions: Will the walk go right or left? How far will it go in that direction? Will it go up or down? How far will it go in that direction?

We use `choice([1, -1])` to choose a value for `x_direction`, which returns either `1` for movement to the right or `-1` for movement to the left. Next, `choice([0, 1, 2, 3, 4])` randomly selects a distance to move in that direction. We assign this value to `x_distance`. The inclusion of a `0` allows for the possibility of steps that have movement along only one axis.

We determine the length of each step in the *x*- and *y*-directions by multiplying the direction of movement by the distance chosen. A positive result for `x_step` means move to the right, a negative result means move to the left, and `0` means move vertically. A positive result for `y_step` means move up, negative means move down, and `0` means move horizontally. If the values of both `x_step` and `y_step` are `0`, the walk doesn’t go anywhere; when this happens, we continue the loop.

To get the next *x*-value for the walk, we add the value in `x_step` to the last value stored in `x_values` and do the same for the *y*-values. When we have the new point coordinates, we append them to `x_values` and `y_values`.

#### Plotting the Random Walk
Here’s the code to plot all the points in the walk:
```Python title:rw_visual.py
import matplotlib
matplotlib.use('TkAgg')  # Use TkAgg for interactive plots
import matplotlib.pyplot as plt

from random_walk import RandomWalk

# Make a random walk.
rw = RandomWalk()
rw.fill_walk()

# Plot the points in teh walk.
plt.style.use('classic')
fig, ax = plt.subplots()
ax.scatter(rw.x_values, rw.y_values, s=15)
ax.set_aspect('equal')
plt.show()
```

#### Generating Multiple Random Walks
Every random walk is different, and it’s fun to explore the various patterns that can be generated. One way to use the preceding code to make multiple walks without having to run the program several times is to wrap it in a `while` loop:
```Python title:rw_visual.py
--snip--

# Keep making new walks, as long as the program is active.
while True:
	# Make a random walk.
	--snip--
	plt.show

	keep_running = input("Make another walk? (y/n): ")
	if keep_running == 'n':
		break
```

This code generates a random walk, displays it in Matplotlib’s viewer, and pauses with the viewer open. When you close the viewer, you’ll be asked whether you want to generate another walk. If you gnerate a few walks, you should see some that stay near the starting point, some that wander off mostly in one direction, some that have this sections connecting larger groups of points, and many other kinds of walks. When you want to end the program, press N.

#### Styling the Walk.
In this section, we’ll customize our plots to emphasize the important characteristics of each walk and deemphasize distracting elements. To do so, we identify the characteristics we want to emphasize, such as where the walk began, where it ended, and the path taken. Next, we identify the characteristics to deemphasize, such as tick marks and labels. The result should be a simple visual representation that clearly communicates the path taken in each random walk.

##### Coloring the Points
We’ll use a colormap to show the order of the points in the walk, and remove the black outline from each dot so the color of the dots will be clearer. To color the points according to their position in the walk, we pass the `c` argument a list containing the position of each point. Because the points are plotted in order, this list just contains the numbers from 0 to 4,999:
```Python title:rw_visual.py
--snip--
while True:
	# Make a random walk.
	rw = RandomWalk()
	rw.fill_walk()

	# Plot the points in the walk.
	plt.style.use('classic')
	fig, ax = plt.subplots()
	point_numbers = range(rw.num_points)
	ax.scatter(rw.x_values, rw.y_values, c=points_number, cmap=plt.cm.Blues, edgecolors='none', s=15)
	ax.set_aspect('equal')
	plt.show()
	--snip--
```

##### Plotting the Starting and Ending Points
In addition to coloring the points to show their position along the walk, it would be useful to see exactly where each walk begins and ends. To do so, we can plot the first and last points individually after the main series has been plotted. We’ll make the end points larger and color them differently to make them stand out:
```Python title:rw_visual.py
--snip--
while True:
	--snip--
	ax.scatter(rw.x_values, rw.y_values, c=point_numbers, cmap=plt.cm.Blues, edgecolors='none', s=15)
	ax.set_aspect('equal')

	# Emphasize the first and last points.
	ax.scatter(0, 0, c='green', edgecolors='none', s=100)
	ax.scatter(rw.x_values[-1], rw.y_values[-1], c='red', edgecolors='none', s=100)

	plt.show()
	--snip--
```

To show the starting point, we plot the point (0, 0) in green and in larger size (`s=100`) than the rest of the points. to mark the end point, we plot the last *x*- and *y*-values in red with a size of `100` as well.

##### Cleaning Up the Axes
Let’s remove the axes in this plot so they don’t distract from the path of each walk.
```Python title:rw_visual.py
--snip--
while True:
	--snip--
	ax.scatter(rw.x_values[-1], rw.y_values[-1], c='red', edgecolors='none', s=100)

	# Remove the axes.
	ax.get_xaxis().set_visible(False)
	ax.get_yaxis().set_visible(False)

	plt.show()
	--snip--
```

To modify the axes, we use the `ax.get_xaxis()` and `ax.get_yaxis()` methods to get each axis, and then chain the `set_visible()` method to make each axis invisible. As you continue to work with visualizations, you’ll frequently see this chaining of methods to customize different aspects of a visualization.

##### Adding Plot Points
Let’s increase the number of points, to give us more data to work with. To do so, we increase the value of `num_points` when we make a `RandomWalk` instance and adjust the size of each dot when drawing the plot:
```Python title:rw_visual.py
--snip--
while True:
	# Make a random walk.
	rw = RandomWalk(50_000)
	rw.fill_walk()

	# Plot the points in the walk.
	plt.style.use('classic')
	fig, ax = plt.subplots()
	point_numbers = range(rw.num_points)
	ax.scatter(rw.x_values, rw.y_values, c=point_numbers, cmap=plt.cm.Blues, edgecolors='none', s=1)
	--snip--
```

##### Altering the Size to Fill the Screen
A visualization is much more effective at communicating patterns in data if it fits nicely on the screen. To make the plotting window better fit your screen, you can adjust the size of Matplotlib’s output. This is done in the `subplots()` call:
```Python title:rw_visual.py
fig, ax = plt.subplots(figsize=(15, 9))
```

When creating a plot, you can pass `subplots()` a `figsize` argument, which sets the size of the figure. The `figsize` parameter takes a tuple that tells Matplotlib the dimensions of the plotting window in inches.

Matplotlib assumes your screen resolution is 100 pixels per inch; if this code doesn’t give you an accurate plot size, adjust the numbers as necessary. Or, if you know your system’s resolution, you can pass `subplots()` the resolution using the `dpi` parameter:
```Python title:rw_visual.py
fig, ax = plt.subplots(figsize=(10, 6), dpi=128)
```

This should help make the most efficient use of the space available on the screen.