# Wolf-Bot
Set of scripts and instructions to setup and use Wolf Robot from VEEROBOT

## Install Ubuntu [from](https://ubuntu.com/#download). Depending on the platform, you may select the version
### For Wolf, select Ubuntu 20.04.x LTS (Focal Fossa) version
### Install ROS Noetic on Ubuntu [from](https://github.com/VEEROBOT/ROS-tools)

Follow the instructions in ```https://github.com/VEEROBOT/ROS-tools``` to install ROS Noetic on Ubuntu Platform. Once installed, test basic scripts mentioned in the link to test if ROS is installed and working correctly. 

## Optional / Not Required - Install Arduino sofware on Ubuntu Focal for ROS.
### Download and Install Arduino [from](https://www.arduino.cc/en/software)
### Extract and go to directory
```
sudo chmod +x install.sh
sudo ./install.sh
```
### Install ESP32 for Arduino. Wolf uses ESP32 as the base controller. In Preferences, add:
```https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json```
### Install ESP32 packages from Arduino IDE -> Tools -> Board -> Board Manager -> ESP32
### Install the ROS libraries in Arduino IDE
```
cd <sketchbook>/libraries/		# as shown under preferences
cd /libraries
rm -rf ros_lib
source ~/catkin_ws/devel/setup.bash
rosrun rosserial_arduino make_libraries.py .
```

## Install ROS Serial libraries
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



