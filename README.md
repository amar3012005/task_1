# TASK-1: Autonomous Navigation with Turtlebot3 in Gazebo using ROS 2 Default Planners
### follow the package structure:
#### my_turtlebot3_world/
####├── launch/house.launch.py
####├── worlds/house.world
####|-- maps/house_map.yaml
####├── package.xml
####└── setup.py

## Detailed Instructions
### 1. Setup Gazebo and RViz Environment
#### - install ros2-humble
#### - install NAV2 AND TURTLEBOT3
#####   sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup
#####   sudo apt install ros-humble-turtlebot3*
### 2. A CUSTOM PKG INSIDE THE WORKSPACE.
#####   ros2 pkg create --build-type ament_python my_turtlebot3_world
####   WORLD AND LAUNCH DIRECTORIES
####   copy and paste the .world and .launch.py files in the /install/task_1/share/task_1 .
####   copy and paste .world  and .launch.py files in the default turtlebot3_gazebo
#####  cp turtlebot3_gazebo/worlds/house.world ~/ros2_ws/src/task_1/worlds/
#####  cp turtlebot3_gazebo/launch/house.launch.py ~/ros2_ws/src/task_1/launch/
#####  finish package : colcon buld
#####  source install/setup.bash
### 3. NOW TO Make the robot move in the environment AND START MAPPING
#### RUN THE TURTLEBOT3 CUSTOM WORLD IN GAZEBO : ros2 launch task_1 house.launch.py
#### RUN THE TURTLEBOT3 TELEOP : ros2 run turtlebot3_teleop teleop_keyboard  
#### EXECUTE RVIZ : ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True 
### 4.Once mapping is Finished
#### SAVE THE MAP: ros2 run nav2_map_server map_saver_cli -f /task_1/maps/house_map

### 5.fix dds issue with Nav2

##### in param file  sudo gedit /opt/ros/humble/share/turtlebot3_navigation2/param/waffle.yaml

##### change the following parameter as 

#### $$$ robot_model_type----change differential to nav2_amcl::DifferentialMotionModel $$$

### 6.EXECUTING AUTONOMOUS NAVIGATION.
#### ros2 launch task_1 house.launch.py
#### ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=/task_1/maps/house_map.yaml
