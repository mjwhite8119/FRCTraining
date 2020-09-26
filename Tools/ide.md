# <a name="ide"></a>Development Environment Setup
The code must be run on an ESP32 NodeMCU development board, which is an embedded Arduino based microcontroller with built-in WiFi.  For the development environment (IDE) we'll be using VSCode.  This is the IDE most commonly used by <i>First Robotics</i> teams.  In order to install code onto the ESP32 microcontoller you have to install the PlatformIO plugin for VSCode. The PlatformIO plugin install is explained in this [YouTube video](https://www.youtube.com/watch?v=5edPOlQQKmo)

Once you have the PlatformIO plugin installed the FRCRobot code can be cloned from Github following these instructions:
- From VSCode go to `View->Command Palette`.
- Type in `git clone` ,which will bring up a text box.
- Put in https://github.com/mjwhite8119/FRCRobot1.git and press enter.
- You'll then be prompted to enter a directory location on your local machine in which to store the project.
- Finally, open the project in VSCode.

Edit file connectWiFi.h to add your WiFi SSID and password.

Open a terminal and type the command:

 `run -vv -e esp32dev -t uploadfs`
 
This is required to load the HTML and CSS files into the ESP32 SPIFFS file system. 

<h3><span style="float:left">
<a href="trainingRobot">Previous</a></span>
<span style="float:right">
<a href="bom">Next</a></span></h3>