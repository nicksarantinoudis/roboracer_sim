# roboracer_sim
An open-source RoboRacer simulator utilizing ROS2, Gazebo and RViz. 

This simulator utilizes the new Gazebo, ROS2 and RViz to create a simulation 
interface for the RoboRacer vehicle (formerly F1-Tenth). These are the main
components in this repository: 

1. The simulator interface, launching both Gazebo and RViz, spawning the vehicle 
model into a test world and the RViz interface visualizing the simulated sensors 
installed in the vehicle.

2. A visualization tool using RViz that can visualize either physical or simulated 
data in real time or through ROS bags.

3. A mapping tool that creates a map utilizing lidar scans either in real time 
or from recorded data in ROS bag formats, both from physical or simulated data.

4. A tool that can turn the created maps into 3D models.

In addition under `roboracer_description/models/roboracer/meshes` you can find all 
the 3D models used to accurately visualize the model in Gazebo simulator, while under
`rosbags` two ROS bags, one recorded during physical testing and the other through the 
simulator are provided in order to test the provided software. 

## Requirements
1. Ubuntu 22.04.5 LTS
2. ROS2 Humble Hawksbill
3. Don't forget to `source /opt/ros/humble/setup.bash`

## Installation

1. Create your workspace folder
2. Create a src folder
3. Run `colcon build` on the empty folder to initialize
5. Clone the repository into the src folder
6. Run `rosdep update`
7. Run `rosdep install --from-paths src -i -y`
8. Run `colcon build`
9. Run `source install/setup.bash` after the succesfull build

Note: Depending on the state of your initial ROS 2 installation, additional packages might be missing. Based on feedback, you may specifically need to install the Gazebo bridge and ignition development libraries: `sudo apt install ros-humble-ros-gz libignition-gazebo6-dev libignition-common4-dev`

If any other packages are flagged as missing during your build, please install them via `sudo apt install ros-humble-<package-name>`

## Simulator 

In order to launch the simulator and the RViz visualization, use the following command:  
`ros2 launch roboracer_bringup roboracer.launch.py`. 
This command launches Gazebo and RViz with a testing environment simulating Unmanned Systems and Robotics Lab testing area, infused with obstacles.

![gazebo_rviz](https://github.com/user-attachments/assets/19e09e51-f1ea-4481-80de-7703a5ea80b3)

In addtion, two more environments can be launched; a) Using `ros2 launch roboracer_bringup roboracer_mcnair.launch.py`
launches Gazebo and RViz within the corridors of McNair Aerospace Center while b) using `ros2 launch roboracer_bringup roboracer_levine.launch.py`
launches Gazebo and RViz within the corridors of Levine Hall, a typical map used in RoboRacer labs.

## Visualization
In order to run the visualizer use the command `ros2 launch roboracer_visualization roboracer_vizualization.launch.py`
You can use it with sensor data either streaming in from the physical or the simulated system or with a pre-recorded ROS bag.
Depending on the type of data you are using, you may need to adjust the visualized topic from the RViz interface.

In case of a ROS bag, use `ros2 bag play "filename_of_unzip_rosbag_folder"` to play the data. 
![physical_rviz_start](https://github.com/user-attachments/assets/d159aed6-7c52-4bc2-be54-0ca12a698780)

## Mapping
Mapping utilizes the slam_toolbox and requires multiple modules to be running at the same time. 

When data stream from physical sensors `ros2 launch slam_toolbox roboracer_offline_mapping.launch.py` needs
to be used, otherwise when they come from Gazebo virtual sensors `ros2 launch slam_toolbox roboracer_offline_mapping_sim_data.launch.py` needs
to be used. 

In order to visualize the mapping process `ros2 launch slam_toolbox roboracer_slam_rviz.launch.py` has to be launched (requires a second terminal, directed at the workspace 
and `source install/setup.bash` run). 
Remember that when data are pre-recorded the ROS bag needs to be played using `ros2 bag play "filename_of_unzip_rosbag_folder."`.
Through the interface (as seen below) you can save the map in `.pgm` format, in order to used it later for the 3D model rebuild. Map are saved 
under the main workspace folder. 

![Screenshot from 2025-05-04 15-38-16](https://github.com/user-attachments/assets/b1c916ac-5367-4440-8c67-c33cb9114a91)

## Map to Gazebo
There is the capability to use map2gazebo tool to build a 3D model of a map to use it as a world on Gazebo. This is an offline 
process and requires the existence of a map in .pgm format created as mentioned above. 

In order to convert a map to a 3D model, you should run `python3 src/roboracer_sim/map2gazebo/map2gazebo/map2gazebo_offline.py --map_dir "filename.pgm"`
The outcome would be a .stl file under the same folder.

![Screenshot from 2025-05-11 17-55-40](https://github.com/user-attachments/assets/6ee84a9d-9321-47b1-86dc-639da65ecd9b)
