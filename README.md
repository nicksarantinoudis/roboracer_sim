# roboracer_sim
A new open-source RoboRacer simulator utilizing ROS2, Gazebo and RViz. 

This simulator utilizes the new Gazebo, ROS2 and RViz to create a simulation 
interface for the RoboRacer vehicle (formerly F1-Tenth). These are the main
components in this repository: 

1. The simulator interface, launching both Gazebo and RViz, spawning the vehicle 
model into a test world and the RViz interface visualizing the simulated sensors 
installed in the vehicle.

2. A visualization tool using RViz that can visualize either physical or simulated 
data in real time or through ROS bags.

3. A mapping tool that creates a map through the lidar reading either in real time 
or from recorded data in ROS bag formats, both from physical or simulated data.

4. A tool that can turn the created maps into 3D models.

## Requirements
Ubuntu 22.04.5 LTS
ROS2 Humble Hawksbill

## Installation

1. Create your workspace folder
2. Create a src folder
3. Run `colcon build` on the empty folder to initialize
5. Clone the repository into the src folder
6. Run `rosdep update`
7. Run `rosdep install --from-paths src -i -y`
8. Run `colcon build`

### Simulator 

In order to launch the simulator and the RViz visualization, use the following command: 
`ros2 launch roboracer_bringup roboracer.launch.py`
