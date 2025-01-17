### Meta
2025-01-17 11:24
**Tags:** [[python]] [[py_projects]] [[py_data_visualization]]
**Status:** #completed 

### Mapping Global Datasets: GeoJSON Format
In this section, we’ll download a dataset representing all the earthquakes that have occurred in the world during the previous month. Then, we’ll make a map showing the location of these earthquakes and how significant each one was. Because the data is stored in the GeoJSON format, we’ll work with it using the `json` module. Using Plotly’s `scatter_geo()` plot, we’ll create visualizations that clearly show the global distribution of earthquakes.


#### Examining GeoJSON Data
The *eq_data_1_day_m1.geojson* file is very dense and hard to read. It’s formatted more for machines than humans, but it contains some dictionaries, as well as info that we’re interested in, such as magnitude and locations.

The `json` module provides a variety of tools for exploring and working with JSON data. Some of these tools will help us reformat the file so we can look at the raw data more easily before we work with it programatically.

We’ll start by loading the data and displaying it in a format that’s easier to read. This is a long data file, so instead of printing it, we’ll rewrite the data to a new file. Then we can open that file and scroll back and forth through the data more easily:
```Python title:eq_explore_data.py
from pathlib import Path
import json

# Read data as a string and convert to a Python object.
path = Path('eq-data/eq_data_1_day_m1.geojson')
contents = path.read_text()
all_eq_data = json.loads(contents)

# Create a more readable version of the data file.
path = Path('eq_data/readable_eq_data.geojson')
readable_contents = json.dumps(all_eq_data, indent=4)
path.write_text(readable_contents)
```

When opening the file *readable_eq_data.json*, here’s the first part we see:
```JSON title:eq_explore_data.geojson
{
    "type": "FeatureCollection",
    "metadata": {
        "generated": 1649052296000,
        "url": "https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/1.0_day.geojson",
        "title": "USGS Magnitude 1.0+ Earthquakes, Past Day",
        "status": 200,
        "api": "1.10.3",
        "count": 160
    },
    "features": [
	--snip--
```

The first part of the file includes a section with the key `"metadata"`. This tells us when the data file was generated and where we can find the data online. It also gives us a human-readable title and the number of earthquakes included in this file. In this 24-hour period, `160` earthquakes were recorded.

This GeoJSON file has a structure that’s helpful for location-based data. The information is stored in a list associated with the key `"features"`. Because this file contains earthquake data, the data is in list form where every item in the list corresponds to a single earthquake. This structure might look confusing, but it’s quite powerful. It allows geologists to store as much information as they need to in a dictionary about each earthquake, and then stuff all those dictionaries into one big list.

Let’s look at a single earthquake:
```JSON title:readable_eq_data.geojson
	--snip--
	        {
            "type": "Feature",
            "properties": {
                "mag": 1.6,
                --snip--
                "title": "M 1.6 - 27 km NNW of Susitna, Alaska"
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -150.7585,
                    61.7591,
                    56.3
                ]
            },
            "id": "ak0224bju1jx"
        },
```

The key `"properties"` contains a lot of information about each earthquake. We’re mainly interested in the magnitude of each earthquake, associated with the key `"mag"`. We’re also interested in the `"title"` of each event, which provides a nice summary of its magnitude and location.

The key `"geometry"` helps us understand where the earthquake occurred. We’ll need this information to map each event. We can find the longitude and the latitude for each earthquake in a list associated with the key `"coordinates"`.

**Note:** When we talk about locations, we often say the location’s latitude first, followed by its longitude. This convention probably arose because humans discovered latitude long before we developed the concept of longitude. However, many geospatial frameworks list the longitude first and then the latitude, because this corresponds to the (x, y) convention we use in mathematical representations. The GeoJSON format follows the (longitude, latitude) convention. If you use a different framework, it’s important to learn what convention that framework follows.

#### Making a List of All Earthquakes
First, we’ll make a list that contains all the information about every earthquake that occurred.
```Python title:eq_explore_data.py
from pathlib import Path
import json

# Read data as a string and convert to a Python object.
path = Path('eq_data/eq_data_1_day_m1.geojson')
contents = path.read_text()
all_eq_data = json.loads(contents)

# Examine all earthquakes in the dataset.
all_eq_dicts = all_eq_data['features']
print(len(all_eq_dicts))

"""
160
"""
```

We take the data associated with the key `'features'` in the `all_eq_data` dictionary, and assign it to `all_eq_dicts`. We know this file contains records of 160 earthquakes, and the output verifies that we’ve captured all the earthquakes in the file.

#### Extracting Magnitudes
We can loop through the list containing data about each earthquake, and extract any information we want. Let’s pull out the magnitude of each earthquake:
```Python title:eq_explore_data.py
--snip--
all_eq_dicts = all_eq_data['features']

mags = []
for eq_dict in all_eq_dicts:
	mag = eq_dict['properties']['mag']
	mags.append(mag)

print(mags[:10])

"""
[1.6, 1.6, 2.2, 3.7, 2.92000008, 1.4, 4.6, 4.5, 1.9, 1.8]
"""
```

#### Extracting Location Data
The location data for each earthquake is stored under the key `"geometry"`. Inside the geometry dictionary is a `"coordinates"` key, and the first two values in this list are the longitude and latitude.
```Python title:eq_explore_data.py
--snip--
all_eq_dicts = all_eq_data['features']

mags, lons, lats = [], [], []
for eq_dict in all_eq_dicts:
	mag = eq_dict['properties']['mag']
	lon = eq_dict['geometry']['coordinates'][0]
	lat = eq_dict['geometry']['coordinates'][1]
	mags.append(mag)
	lons.append(lon)
	lats.append(lat)

print(mags[:10])
print(lons[:5])
print(lats[:5])

"""
[1.6, 1.6, 2.2, 3.7, 2.92000008, 1.4, 4.6, 4.5, 1.9, 1.8]
[-150.7585, -153.4716, -148.7531, -159.6267, -155.248336791992]
[61.7591, 59.3152, 63.1633, 54.5612, 18.7551670074463]
"""
```

#### Building a World Map
Using the information we’ve pulled so far, we can build a simple world map. Although it won’t look presentable yet, we want to make sure the information is displayed correctly before focusing on style and presentation issues. Here’s the initial map:
```Python title:eq_world_map.py
from pathlib import Path
import json

import plotly.express as px

--snip--
for eq_dict in all_eq_dicts:
	--snip--

title = 'Global Earthquakes'
fig = px.scatter_geo(lat=lats, lon=lons, title=title)
fig.show()
```

#### Representing Magnitudes
A map of earthquake activity should show the magnitude of each earthquake. We can also include more data, now that we know the data is being plotted correctly.
```Python title:eq_world_map.py
--snip--
# Read data as a string and convert to a Python object.
path = Path('eq-data/eq_data_30_day-m1.geojson')
contents = path.read_text()
--snip--

title = 'Global Earhquakes'
fig = px.scatter_geo(lat=lats, lon=lons, size=mags, title=title)
fig.show()
```

#### Customizing Marker Colors
We can use Plotly’s color scales to customize each marker’s colors, according to the severity of the corresponding earthquake. We’ll also use a different projection for the base map.
```Python title:eq_world_map.py
--snip--
fig = px.scatter_geo(lat=lats, lon=lons, size=mags, title=title,
					color = mags,
					color_continuous_scale='Viridis',
					labels={'color':'Magnitude'},
					projection='natural_earth',
					)
fig.show()
```

#### Adding Hover Text
To finish this map, we’ll add some informative text that appears when you hover over the marker representing an earthquake. In addition to showing the longitude and latitude, which appear by default, we’ll show the magnitude and provide a description of the approximate location as well.

To make this change, we must pull a little more data from the file:
```Python title:eq_world_map.py
--snipp--
mags, lons, lats, eq_titles = [], [], [], []
	--snip--
	eq_title = eq_dict['properties']['title']
	mags.append(mag)
	--snip--
	eq_titles.append(eq_title)

title = 'Global Earthquakes'
fig = px.scatter_geo(lat=lats, lon=lons, size=mags, title=title,
					--snip--
					projection='natural earth',
					hover_name=eq_titles,
					)
fig.show()
```