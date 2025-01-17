### Meta
2025-01-16 11:40
**Tags:** [[python]] [[py_projects]] [[py_data_visualization]]
**Status:** #pending 

### The CSV File Format
One simple way to store data in a text file is to write the data as a series of values separated by commas, called *comma-seperated values*. The resulting files are *CSV* files. For example, here’s a chunk of weather data in CSV format:
```CSV title:example.csv
"USW00025333","SITKA AIRPORT, AK US","2021-01-01",,"44","40"
```

This is an excerpt of weather data from Jan 1, 2021, in Sitka, Alaska. It includes the day’s high and low temperatures, as well as a number of other measurements from that day. CSV files can be tedious for humans to read, but programs can process and extract information from them quickly and accurately.

#### Parsing the CSV File Headers
Python’s `csv` module in the standard library parses the lines in a csv file and allows us to quickly extract the values we’re interested in. Let’s start with the first line of the file, which contains a series of headers for the data. The headers tell us what kind of information the data holds:
```Python title:sitka_highs.py
from pathlib import Path
import csv

path = Path('weather_data/sitka_weather_07-2021_simple.csv')
lines = path.read_text().splitlines()

reader = csv.reader(lines)
header_row = next(reader)
print(header_row)
```

We first import `Path` and the `csv` module. We then build a `Path` object that looks in the `weather_data` directory, pointing to the specific weather data file we want to work with. We read the file and chain the `splitlines()` method to get a list of all lines in the file, which we assign to `lines`.

Next, we build a `reader` object. This can be used to parse each line in the file. To make a reader object, call the function `csv.reader()` and pass it the list of lines from the CSV file.

When given a `reader` object, the `next()` function returns the next line in the file, starting from the beginning of the file. Here we call `next()` only once, so we get the first line of the file, which contains the file headers. We assign the data that’s returned to `header_row`, which contains weather-related headers that tell us what information each line of data holds:
```Bash title:output.sh
['STATION', 'NAME', 'DATE', 'TAVG', 'TMAX', 'TMIN']
```

The `reader` object processes the first line of comma-separated values in the file and stores each value as an item in a list. The header `STATION` represents the code for the weather station that recorded this data. The position of this header tells us that the first value in each line will be the weather station code. The `NAME` header indicates that the second value in each line is the name of the weather station that made the recording. The rest of the headers specify what kinds of information were recorded in each reading. The data we’re most interested in for now are the date (`DATE`), the high temperature (`TMAX`), and the low temperature (`TMIN`).

#### Printing the Headers and Their Positions
To make it easier to understand the file header data, let’s print each header and its position in the list.
```Python title:sitka_highs.py
--snip--
reader = csv.reader(lines)
header_row = next(reader)

for index, column_header in enumerate(header_row):
	print(index, column_header)

"""
0 STATION
1 NAME
2 DATE
3 TAVG
4 TMAX
5 TMIN
"""
```

The `enumerate()` function returns both the index of each item and the value of each item as you loop through a list.

#### Extracting and Reading Data
Now that we know which columns of data we need, let’s read in some of it. First, we’ll read in the high temperature for each day:
```Python title:sitka_highs.py
--snip--
reader = csv.reader(lines)
header_row = next(reader)

# Extract high temperatures.
highs = [int(row[4]) for row in reader]

print(highs)
```

#### Plotting Data in a Temperature Chart
To visualize the temperature data we have, we’ll first create a simple plot of the daily highs using Matplotlib, as shown here:
```Python title:sitka_highs.py
from pathlib import Path
import csv

import matplotlib.pyplot as plt

path = Path('weather_data/sitka_weather_07-2021_simple.csv')
lines = path.read_text().splitlines()
	--snip--

# Plot the high temperatures.
plt.style.use('seaborn')
fig, ax = plt.subplots
ax.plot(highs, color='red')

# Format plot.
ax.set_title("Daily High Temperatures, July 2021", fontsize=24)
ax.set_xlabel('', fontsize=16)
ax.set_ylabel("Temperature (F)", fontisze=16)
ax.tick_params(labels=16)

plt.show()
```

#### The datetime Module
Let’s add dates to our graph to make it more useful. The first date from the weather data file is in the second row of the file. The data will be read in as a string, so we need a way to convert the string `"2021-07-01"` to an object representing this date. We can do that using the `strptime()` method from the `datetime` module.

#### Plotting Dates
We can improve our plot by extracting dates for the daily high temperature readings, and using them on the *x*-axis:
```Python title:sitka_highs.py
from pathlib import Path
import csv
from datetime import datetime

--snip--
header_row = next(reader)

# Extract dates and high temperatures.
dates, highs = [], []
for row in reader:
	current_date = datetime.strptime(row[2], '%Y-%m-%d')
	high = int(row[4])
	dates.append(current_date)
	dates.append(high)

# Plot the high temperatures.
plt.style.use('seaborn')
fig, ax = plt.subplots()
ax.plot(dates, highs, color='red')

# Format plot.
ax.set_title("Daily High Temperatures, July 2021", fontsize=24)
ax.set_xlabel('', fontsize=16)
fig.autofmt_xdate()
ax.set_ylabel("Temperature (F)", fontsize=16)
ax.tick_params(labelsize=16)

plt.show()

```

The call to `fig.autofmt_xdate()` draws teh date labels diagonally to prevent them from overlapping.

#### Plotting a Longer Timeframe
With our graph set up, let’s include additional data to get a more complete picture of the weather in Stika in 2021.
```Python title:sitka_highs.py
--snip--
path = Path('weather_data/sitka_weather_2021_simple.csv')
lines = path.read_text().splitlines()
--snip--
# Format plot.
ax.set_title("Daily High Temperatures, 2021", fontsize=24)
ax.set_xlabel('', fontsize=16)
--snip--
```

#### Plotting a Second Data Series
We can make our graph even more useful by including the low temperatures We must extract them from the data file and then add them to the graph.
```Python title:sitka_highs.py
--snip--
reader = csv.reader(lines)
header_row = next(reader)

# Extract dates, and high and low temperatures.
dates, highs, lows = [], [], []
for row in reader:
	current_date = datetime.strptime(row[2], '%Y-%m-%d')
	high = int(row[4])
	low = int(row[5])
	dates.append(current_date)
	highs.append(high)
	lows.append(low)

# Plot the high and low temperatures.
--snip--
ax.plot(dates, highs, color='red')
ax.plot(dates, lows, color='blue')

# Format plot.
ax.set_title("Daily High and Low Temperatures, 2021", fontsize=24)
--snip--
```

#### Shading an Area in the Chart
Having added two data series, we can now examine the range of temperatures for each day. As a finishing touch to the graph, we’ll use shading to show the range between each day’s high and low temperatures. To do so, we’ll use the `fill_between()` method, which takes a series of *x*-values and two series of *y*-values and fills the space between the two series of *y*-values:
```Python title:sitka_highs.py
--snip--
# Plot the high and low temperatures.
--snip--
fig, ax = plt.subplots()
ax.plot(dates, highs, color='red', alpha=0.5)
ax.plot(dates, lows, color='blue', alpha=0.5)
ax.fill_between(dates, highs, lows, facecolor='blue', alpha=0.1)
--snip--
```

#### Error Checking
1234