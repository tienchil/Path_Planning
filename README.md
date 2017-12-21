# Path Planning
---

## Summary

This project is the first one in Udacity's Self-Driving Car Nanodegree Term 3. The main goal of this project is to build a path planning program for vehicle to drive autonomously on highway simulator without collisions and speeding.


## Model Documentation

A simple path planning strategy is used in this project. Initially, when the vehicle does not have enough trajectory points, it will simply slowly accelerate to allow the the time for generating the first set of points.

To generate trajectory points, spline library is used to make a smooth path for the vehicle. The model takes a few points from previous trajectory and waypoints as input in spline. These points are transformed to car's coordinate system to make the calculation easier to reason. Then, by using the spline, the model is able to generate a smooth path for the vehicle. These generated points are transformed back to the map coordinate system before feeding into the simulator.

In order to avoid collisions, the vehicle will begin to slow down when it is too close (< 30m) to the car in front of it. Once it's too close, it will decide if changing the nearby lane is feasible. I use a simple counter to determine the decision of changing lanes. If other lanes have close vehicles, the counter will be penalized (more heavily if other vehicles are too close). Otherwise, The counter increases. Once the counter is increased to a certain number, it will flag changing lanes as a safe motion. 

This strategy enables the vehicle to change lanes safely in most cases. A few cases where other vehicles have random behaviour, or there is a traffice in every lane, this lane changing strategy is likely to fail.
