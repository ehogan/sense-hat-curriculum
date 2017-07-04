---
title: Making Sense of the Weather
description: Compare Sense HAT data with data from Met Office DataPoint
notes: "Making Sense of the Weather - notes.md"
layout: project
new: true
...

# Introduction { .intro}

In this project you will compare the data from the temperature and humidity
sensors on the Sense HAT with site-specific temperature and humidity data from
Met Office DataPoint (http://www.metoffice.gov.uk/datapoint). Then you will
display colours corresponding to the conditions on the Sense HAT LED matrix.

You will be writing code in the Python programming language, which you may have
learnt in the Python module (https://codeclubprojects.org/en-GB/python).

# Step 1: Displaying colours { .activity}

First let's show colours using the LED Matrix on the Sense HAT. The colours
we are interested in are red and blue.

To set the colour of an individual LED we need to say how much red, green and
blue it should have from 0 to 255.

## Activity Checklist { .check}

+ Open a new Python 3 IDLE session.
+ Select `File` > `New File` to open a new file and save it as
  `temperature.py`. 
+ Add the code below to set up the Sense HAT. If you are using the Sense HAT
  emulator, replace `sense_hat` in the code below with `sense_emu`.

```python
from sense_hat import SenseHat

sense = SenseHat()
sense.clear()
```

+ Add the code below to set up a variable for the colour red and then turn all
  the pixels red using `sense.clear(R)`. 

```python
R = [255, 0, 0]

sense.clear(R)
```

+ Run your script by selecting `Run` > `Run Module` or pressing `F5`. The Sense
  HAT LED Matrix should turn red.

+ Blue is next. Add a new variable for the colour blue and change
  `sense.clear()` to use this new variable. Your code should now look like the
  code below.

```python
R = [255, 0, 0]
B = [0, 0, 255]

sense.clear(B)
```

+ Test your script again by pressing `F5`. The Sense HAT LED Matrix should turn
  blue. 

# Step 2: Reading the sensor data { .activity}

The Sense HAT has a range of sensors that provide real world data on a
Raspberry Pi computer.

The temperature sensor reports the temperature around the sensor.

## Activity Checklist { .check}

+ Let's read from the temperature sensor and print out the result. Add the code
  below to the bottom of your script.
   
```python
print(sense.temperature)
```

+ Test your script. What temperature is the Sense HAT temperature sensor
  reporting?

# Step 3: Reading the latest forecast from Met Office DataPoint { .activity}

Met Office DataPoint provides site-specific weather forecasts. First we need to
set up Met Office DataPoint. To use Met Office DataPoint you will need an API
key. You can find this in `/home/pi/api_key.txt`.

## Activity Checklist { .check}

+ Add the code below to the top of your script but below the line containing
  `import SenseHat`.

+ Replace `aaaa-bbbb-cccc-dddd` with your API key.

```python
from datapointbasic import locationforecast

api_key = 'aaaa-bbbb-cccc-dddd'

horsham = locationforecast('Horsham', api_key)
```

+ Let's get the latest temperature for Horsham. Add a new print statement to
  the bottom of your script to print the temperature from the weather forecast
  for Horsham.

```python
print(horsham.now.temperature)
```

+ Test your script. What temperature is the weather forecast for Horsham
  reporting?

# Step 4: Showing the conditions { .activity}

## Activity Checklist { .check}

+ Now we can show whether it is hotter or cooler inside compared to outside.
  Add the code below to the bottom of your script.

```python
if sense.temperature < horsham.now.temperature:
    sense.clear(B)
else:
    sense.clear(R)
```

+ Test your script. If the Sense HAT LED Matrix is blue, that means it's cooler
  inside compared to outside. Red means it's warmer. Which are you seeing?
 
## Challenge 1: Measure humidity { .challenge}

The humidity sensor on the Sense HAT reports the amount of moisture in the air.

Save a copy of your script as `humidity.py` and change it so that it records
humidity instead of temperature. Try just changing the word `temperature`
everywhere you see it to `humidity` and see what happens.

Adjust the colours accordingly (let's say blue if it's more humid inside,
yellow if it's less). Remember to set a new colour variable like we did before
whenever using a new colour. You can look up RGB colours at
https://trinket.io/docs/colors.

## Challenge 2: Use a different location { .challenge}

Save another copy of `temperature.py` as `hometown.py` and adapt it to compare
the temperature from the Sense HAT to the temperature from the forecast for a
different location, for example your hometown. If you get an error with the
location name, ask a member of Met Office staff for help.

Now try comparing the temperature from the forecast in your hometown with the
temperature from the forecast from Horsham that we found earlier. Do this by
setting separate variables for the two locations.

Where is warmer?
