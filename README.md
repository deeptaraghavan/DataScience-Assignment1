# CS1656-A1
Assignment 1 for Introduction to Data Science
# Assignment #1: Python


### Description
This is the **first assignment** for Introduction to Data Science

### Goal
The goal of this assignment is to familiarize you with the Python programming language and also expose you to real data.

### What to do -- bike.py
You are asked to complete a Python program, called `bike_pitt.py` that will access live data from the [HealthyRidePGH website](https://healthyridepgh.com/) and provide answers to specific queries about shared bike availability in the Pittsburgh region.

The program conatins a class, `Bike`, that has three arguments in its constructor, `baseURL`, `station_info` and `station_status`. These arguments are used to define URLs for specific data feeds, namely information about individual stations and the status of every station. You can create an instance of the `Bike` class by calling its constructor with appropriate URL fragments, and call its methods to run the different parts of the assignment.

The class can be used like this:
```
instance = Bike(baseURL, '/station_information.json', '/station_status.json')
t_bikes = instance.total_bikes()
t_docks = instance.total_docks()
p_avail = instance.percent_avail(station_id)
c_stations = instance.closest_stations(latitude, longitude)
c_bike = instance.closest_bike(latitude, longitude)
s_bike_avail = instance.station_bike_avail(exact_latitude, exact_longitude)
```
where `baseURL` is the prefix URL of the source of the data, and it is typically https://api.nextbike.net/maps/gbfs/v1/nextbike_pp/en, although we will modify that during testing, in order to evaluate your submitted programs with static data. It is important for your program to work with ANY proper `baseURL`. Also, `station_id` is the ID of a particular station, `latitude` and `longitude` are spatial coordinates, and `exact_latitude` and `exact_longitude` are exact coordinates of a specific station.


### Data Feeds
Assume the baseURL parameter is stored in variable `baseURL`. We will use two data feeds from the HealthyRidePGH General Bikeshare Feed Specification (GBFS) data feed, as follows:
* **Station Information**: `station_infoURL = baseURL+'/station_information.json'`, which provides for each docking station: station_id, name, latitude
 and longtitude, and the total capacity (e.g., [https://api.nextbike.net/maps/gbfs/v1/nextbike_pp/en/station_information.json](https://api.nextbike.net/maps/gbfs/v1/nextbike_pp/en/station_information.json)).   

* **Station Status**: `station_statusURL = baseURL+'/station_status.json'`, which provides for each station_id how many bikes and how many docks are available at any given time (e.g., [https://api.nextbike.net/maps/gbfs/v1/nextbike_pp/en/station_status.json](https://api.nextbike.net/maps/gbfs/v1/nextbike_pp/en/station_status.json)).


You can find additional information about the GBFS specification at [https://github.com/NABSA/gbfs](https://github.com/NABSA/gbfs) and about all the available data feeds from HealthyRidePGH at [https://api.nextbike.net/maps/gbfs/v1/nextbike_pp/gbfs.json](https://api.nextbike.net/maps/gbfs/v1/nextbike_pp/gbfs.json).


### Method #1: Total bikes available
The method `total_bikes` will compute and return how many bikes are currently available over all stations in the entire HealthRidePGH network.

Sample invocation:
```
result = instance.total_bikes()
```

The variable `result` should have an **integer** value like `123`.

### Method #2: Total docks available
The method `total_docks` will compute and return how many docks are currently available over all stations in the entire HealthRidePGH network.

Sample invocation:
```
result = instance.total_docks()
```

The variable `result` should have an **integer** value like `123`.

### Method #3: Percentage of docks available in a specific station
The method `percent_avail` will compute and return how many docks are currently available for the specified station as a percentage over the total number of bikes and docks available. In this case, the station_id is given as a parameter.

Sample invocation:
```
result = instance.percent_avail(342885)
```

The variable `result` should have a **string** value like `76%`.

In our example, the num_bikes_available was 4, the num_docks_available was 13, so the percent available was 13/(4+13), i.e., 76%. You should appropriately round the percentage to be an integer. To simplify things, always round down (floor), i.e., return the highest integer that is not greater than the number you try to round. Also, keep in mind that the `%` sign follows the number without any spaces. Finally, if the station ID is invalid, the method should return an empty string.

### Method #4: Names of three closest HealthyRidePGH stations.
The method `closest_stations` will return the station_ids and the names of the three closest HealthyRidePGH stations based just on latitude and longtitude (of the stations and of the specified location). The first parameter is the latitude and the second parameter is the longtitude.

Sample invocation:
```
result = instance.closest_stations(40.444618, -79.954707)
```

The variable `result` should have a **dictionary** value of **strings** mapped to **integers** like `{342885: 'Schenley Dr at Schenley Plaza (Carnegie Library Main)', 342887: 'Fifth Ave & S Dithridge St', 342882: 'Fifth Ave & S Bouquet St'}`.

Note that in order to compute distances between two points, you must use the provided `distance()` method of the class. The `distance` method takes four arguments, `lat1`, `lon1`, `lat2` and `lon2` that correspond to two latitude-longitude coordinate pairs, and returns the distance between the two points.

### Method #5: Name of the closest HealthyRidePGH station with available bikes
The method `closest_bike` will return the station_id and the name of the closest HealthyRidePGH station that has available bikes, given a specific latitude and longitude. The first parameter is the latitude and the second parameter is the longitude.

Sample invocation:
```
result = instance.closest_bike(40.444618, -79.954707)
```

The variable `result` should have a **dictionary** value of **strings** mapped to **integers** like `{342887: 'Fifth Ave & S Dithridge St'}`. The dictionary must have a single item that corresponds to the closest station.


### Method #6: The number of bikes available at a bike station 
The method `station_bike_avail` will return the station_id and the number of bikes available at the station, given a specific latitude and longitude. The first parameter is the latitude and the second parameter is the longitude.

Sample invocation:
```
result = instance.station_bike_avail(40.444618, -79.954707)
```

The variable `result` should have a **dictionary** value of **integers** mapped to **integers** like `{342887: 4}`. The dictionary must have a single item that corresponds to the station with the exact coordinates. In this example, the result is the station with ID 342887 that has 4 bikes available. Also, if a station with the exact given coordinates doesn't exist, you must return an empty dictionary.


### Allowed Python Libraries (Updated)
You are allowed to use the following Python libraries (although a fraction of these will actually be needed):
```
argparse
collections
csv
json
glob
math
os
pandas
re
requests
string
sys
time
xml
```
If you would like to use any other libraries, you must ask permission within a maximum of one week after the assignment was released


### Important notes about grading
It is absolutely imperative that your python program:  
* runs without any syntax or other errors (using Python 3)  
* strictly adheres to the format specifications for input and output, as explained above.

Failure in any of the above will result in **severe** point loss.
