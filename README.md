# Indoor_Location_Tracking

I am making attempts to get absolute position in an indoor environment. In these initial attempts, I am using mathematical trilateration in order to locate position based on WiFi access points. We first scan for wifi access points given known location. Then, locate positions the of access points given signal strength at the locations. Finally, with a map of wifi points, we can use live scans to find a live location.

Reading: https://en.wikipedia.org/wiki/Trilateration

## What's Here

There are multiple Jupyter Notebook (.ipynb) files containing Python scripts. These files are described in more detail in ```files.docx``` . In essence, the three files ```Locate_APs.ipynb```, ```Reverse_Trilaterate.ipynb```, and ```Wifi_Trilateration.ipynb``` work as a data collection, processing, and testing flow. If all works, the final file will be able to make guesses at a user's location given a significant amount of wifi access points in an area. There is a folder ```Data``` that contains .csv outputs from my initial tests.

## Running the files

Pre-requisite: be able to run jupyter notebooks. Be able to run python packages like time, csv, numpy, pandas, and pywifi.

Pre-requisite: be in a location with many wifi access points. The more devices the better results.

### Locate_APs.ipynb

Run this file first. The user will need to input their locaiton on an X, Y, Z grid. This coordinate system is imaginary to the user's application, but is VERY important to logically define. For my tests, I centered myself at the end of a university hallway, then used 1 foot incriments for the coordinate system. After each time the user inputs location, the program will scan all WiFi Access Points in the area, and save current locaiton, MAC address, and signal strength to a .csv file for later analysis. 

### Reverse_Trilaterate.ipynb

This file is run second. This is a short program that will take in the output from Locate_APs.ipynb, and then calculate positions of the accesss points using trilateration off the signal strengths as distance. A new CSV is created with MAC address and estimated absolute location for each access point. Note: The current implementaion uses signal strength (dBm) as a proxy for distance. A more proper future program needs to convert signal strength to a true distance in feet.

### Wifi_Trilateration.ipynb

The final file in the data flow. This takes in the output from Reverse_Trilaterate.ipynb, and then allows a user to scan wifi when they press a button. The current status of the wifi nodes is then used to locate the user's current position.

## Current Notes

The program is not perfect. The mapping does not throw the access points within true locations of our coordinate system. This is due to a variety of factors from signal noise to mapping accuracy. Luckily, the results are moderatly consistent. Standing in one spot will give a consistent estimated location +/- roughly 3 feet. This isn't amazing, but shows a proof of concept for the project.

In the future this project will be developed further. First, I want to add that signal strength to true distance conversion. Hopefully that gives more accurate estimates of access point locations. Additionally, I hope performing more precise mapping in the inital steps will improve overall accuracy. Long term goals could be to scan bluetooth beacons and use IMU devices for more precision during movement.