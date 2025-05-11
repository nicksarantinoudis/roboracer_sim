# roboracer_sim
A new open-source RoboRacer simulator utilizing ROS2, Gazebo and RViz. 

This simulator utilizes the new Gazebo, ROS2 and RViz to create a simulation 
interface for the RoboRacer vehicle (formerly F1-Tenth). There are the following
main components build: 

1. The simulator interface, launching both Gazebo and RViz, spawning the vehicle 
model into a test world and the RViz interface visualizing the simulated sensors 
installed in the vehicle.

2. A visualization tool using RViz that can visualize either physical or simulated 
data in real time or through ROS bags.

3. A mapping tool that creates a map through the lidar reading either in real time 
or from recorded data in ROS bag formats, both from physical or simulated data.

4. A tool that can turn the created maps into 3D models.
