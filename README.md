# Step-by-step guide of installing the package arduino_robot_arm :

## Step 1: Prerequisites

![image](https://github.com/ItsRawanMoha/Arduino_Robot_Arm_ROS/assets/156599594/aa71eb86-a641-4b56-b591-8752bedb9f74)

Make sure you have ROS installed on your system. If not, you can follow the instructions provided in the previous section to install ROS.

### - Creating a workspace for catkin

<img src="https://github.com/ItsRawanMoha/Arduino_Robot_Arm_ROS/blob/main/image.png" alt="Alt text" width="550" height="350"> 

This tutorial assumes that you have installed catkin and sourced your environment. If you installed catkin via apt-get for ROS melodic, your command would look like this:
```
$ source /opt/ros/melodic/setup.bash
```
Let's create and build a catkin workspace:
```
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/
$ catkin_make
```
The catkin_make command is a convenience tool for working with catkin workspaces. Running it the first time in your workspace, it will create a CMakeLists.txt link in your 'src' folder.

Additionally, if you look in your current directory you should now have a 'build' and 'devel' folder. Inside the 'devel' folder you can see that there are now several setup.*sh files. Sourcing any of these files will overlay this workspace on top of your environment. To understand more about this see the general catkin documentation: catkin. Before continuing source your new setup.*sh file:
```
$ source devel/setup.bash
```

```
$ echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```

## Step 2: Installing the package arduino_robot_arm
![image](https://github.com/ItsRawanMoha/Arduino_Robot_Arm_ROS/assets/156599594/25cd471d-75f5-44dd-9cf3-37b865753456)

1-  Add the “arduino_robot_arm” package to “src” folder

```
 $ cd ~/catkin_ws/src
```
```
 $ sudo apt install git
```
```
 $ git clone https://github.com/smart-methods/arduino_robot_arm 
```

2-  Install all the dependencies 

```
 $ cd ~/catkin_ws
```
```
 $ rosdep install --from-paths src --ignore-src -r -y
```
```
 $ sudo apt-get install ros-melodic-moveit
```
```
 $ sudo apt-get install ros-melodic-joint-state-publisher ros-melodic-joint-state-publisher-gui
```
```
 $ sudo apt-get install ros-melodic-gazebo-ros-control joint-state-publisher
```
```
 $ sudo apt-get install ros-melodic-ros-controllers ros-melodic-ros-control
```

3- Compile the package
```
$ catkin_make
```

<img src="https://github.com/ItsRawanMoha/Arduino_Robot_Arm_ROS/blob/main/image%20(22).png" alt="Alt text" width="400" height="400"> 

## Step 3: Controlling the motors

```
$ roslaunch robot_arm_pkg check_motors.launch
```


![screen-gif](https://github.com/ItsRawanMoha/Arduino_Robot_Arm_ROS/blob/main/Controlling%20the%20motors.gif)


## Step 4: Controlling the motors joint_state_publisher

```
$ rqt_graph
```

<img src="https://github.com/ItsRawanMoha/Arduino_Robot_Arm_ROS/blob/main/rqt_graph.png" alt="Alt text" width="400" height="400"> 


## Step 5: Controlling the motors joint_state_publisher

```
$ rostopic echo /joint_states
```

![screen-gif](https://github.com/ItsRawanMoha/Arduino_Robot_Arm_ROS/blob/main/Controlling%20the%20motors%20JointstatePublisher.gif)


## Step 6: Controlling the motors in simulation

```
$ roslaunch robot_arm_pkg check_motors.launch
```
```
$ roslaunch robot_arm_pkg check_motors_gazebo.launch
```
```
$ rosrun robot_arm_pkg joint_states_to_gazebo.py
```

- You may need to change the permission 

```
 $ cd catkin/src/arduino_robot_arm/robot_arm_pkg/scripts
```
```
 $ sudo chmod +x joint_states_to_gazebo.py
```

![screen-gif](https://github.com/ItsRawanMoha/Arduino_Robot_Arm_ROS/blob/main/Controlling%20the%20motors%20in%20simulation.gif)


That's it! You have successfully installed the arduino_robot_arm package and can now use it in your ROS projects. 
