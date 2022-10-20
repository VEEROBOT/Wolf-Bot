# Wolf-Bot
Set of scripts and instructions to setup and use Wolf Robot from VEEROBOT
# Joystick Mode
* Press PS key to turn on remote
* Wait for the indicator LED's to stop blinking. Once a single LED is on, it means robot binding to joystick is done
* Use select key to change mode from Normal, Mecanum, Autonomous mode. The last LED indicates settings mode.
* Settings mode is only required for first connection. See Wolf user manual to understand settings. 
* Max speed is limited to 1 meters / second. Use the left buttons to control maximum speed of the robot
* Joystick control and ROS control is mutually exclusive. ROS Commands has priority over Joystick commands. 

# ROS Mode
## Install Ubuntu 
* Install Ubuntu from [Ubuntu Website](https://ubuntu.com/#download). Depending on the platform, you may select the version
* For Wolf, select Ubuntu 20.04.x LTS (Focal Fossa) version
* Follow the instructions on the page [https://github.com/VEEROBOT/ROS-tools](https://github.com/VEEROBOT/ROS-tools) to install ROS Noetic on Ubuntu Platform. <br />Once installed, test basic scripts mentioned there to test if ROS is installed and working correctly. 

## Optional / Not Required - Install Arduino sofware on Ubuntu Focal for ROS.
* Download and Install Arduino from this [link](https://www.arduino.cc/en/software)<br />
* Extract and go to directory<br />
```
sudo chmod +x install.sh
sudo ./install.sh
```
## Install ESP32 for Arduino. Wolf uses ESP32 as the base controller. In Preferences, add:
```https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json```
* Install ESP32 packages from Arduino IDE -> Tools -> Board -> Board Manager -> ESP32
* Install the the latest version of ESP32 libraries
* Install ROS Library for Arduino IDE
```
cd <sketchbook>/libraries/		# as shown under preferences
cd /libraries
rm -rf ros_lib
source ~/catkin_ws/devel/setup.bash
rosrun rosserial_arduino make_libraries.py .
```
## Install ROS Serial libraries for Arduino
```
sudo apt-get install ros-noetic-rosserial-arduino
sudo apt-get install ros-noetic-rosserial
# sudo apt-get install ros-noetic-rosserial-python  # For serial wired connection

cd catkin_ws/src/   #Goto catkin workspace installed from the script
git clone https://github.com/ros-drivers/rosserial.git
cd ..
catkin_make --only-pkg-with-deps rosserial
catkin_make install
```
## Running basic Scripts from ROS Command Prompt
* Start ROS Master by typing ```roscore```
* View the list of ros nodes ```rosnode list```
* View the list of ros topics ```rostopic list```
* View information on specific topic ```rostopic info <topicname>```
* View published data on specific topic ```rostopic echo <topicname>```
* Find any specific file on Ubuntu ```sudo find . -name <filename>```

## Running Wolf Commands from ROS Command Prompt by sending command velocity (cmd_vel)
* Start ROS Master by typing ```roscore```
* Type ```rosrun rosserial_python serial_node.py tcp``` to connect to Wolf
* cmd_vel is limited to -0.5 to +0.5. This means the max velocity of robot is 0.5 meters / second. 
* To open teleop twist keyboard (if installed): ```rosrun teleop_twist_keyboard teleop_twist_keyboard.py```
* Too see any error messages or information from Wolf ```rqt_console```
* Latching Command to run Wolf. Copy Paste does not work. Type till "linear, press tab. Now use left and right arrow keys to edit parameters. -r is the number of commands sent to Wolf. -r10 is send the below command at 10Hz. Only use Linear x and Angular z for normal drive. For mecanum, use Linear x, Linear y and Angular z. 
```
rostopic pub /cmd_vel geometry_msgs/Twist "linear:
	x: 0.25												
	y: 0.0
	z: 0.0
angular:
	x: 0.0
	y: 0.0
	z: 0.25" - r10	
```
* Single Velocity Command:
```
rostopic pub /cmd_vel geometry_msgs/Twist "{ linear: {x: 0.5} }" -r 3
rostopic pub /cmd_vel geometry_msgs/Twist "{ angular: {z: 0.5} }" -r 5
```
* Send cmd_vel to Wolf using a graphical interface : ```rosrun rqt_robot_steering rqt_robot_steering```

## Toggle Commands from ROS Command Prompt
* Pin 5 is connected to a buzzer and below command can be used to toggle the status of buzzer pin
```
rostopic pub toggle_buzzer std_msgs/Empty
```

## Updating Firmware
* Wolf has a wired serial connection that can be used to upgrade the base controller firmware. 
*  --- Will be updated soon ----
