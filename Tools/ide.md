# <a name="ide"></a>Development Environment Setup
The code must be run on an ESP32 NodeMCU development board, which is an embedded Arduino based microcontroller with built-in WiFi.  For the development environment (IDE) we'll be using VSCode.  This is the IDE most commonly used by <i>First Robotics</i> teams.  In order to install code onto the ESP32 microcontoller you have to install the PlatformIO plugin for VSCode. The PlatformIO plugin install is explained in this [YouTube video](https://www.youtube.com/watch?v=5edPOlQQKmo)

Once you have the PlatformIO plugin installed the FRCRobot code can be cloned from Github following these instructions:
- From VSCode go to `View->Command Palette`.
- Type in `git clone` ,which will bring up a text box.
- Put in https://github.com/mjwhite8119/FRCRobot.git and press enter.
- You'll then be prompted to enter a directory location on your local machine in which to store the project.  Call it <i>FRCRobot</i>.
- Finally, click the button to open the project in VSCode.

## Connecting the Robot to your WiFi
Under the `include` directory of the project you will find a file called <i>connectWiFi</i>.h.  Open this file and locate the following lines:

`// inline const char* ssid = "SSID";`

`// inline const char* password = "PASSWORD";`

Uncomment these lines and add your WiFi SSID and password.  When you start the robot your WiFi router will assign it an IP address which will be displayed on the OLED display.  You will need this address to open the web page used as the controller. 

## Compile and Upload Code to the ESP32
Connect a UBS cable from your computer to the ESP32.  Click the upload `->` link in the status bar at the bottom of VSCode to compile and upload. If the upload fails to start you may have to press the <i>BOOT</i> button on the ESP32 microcontroller until the upload starts.

![Task Bar](../images/FRCRobot/FRCRobot.009.jpeg)

You're all done!  You don't need to read the next section unless you want to change how the robots' web page controller looks and functions.

## Updating HTML and CSS Files
The ESP32 contains a Serial Peripheral Interface Flash File System (SPIFFS). SPIFFS is a lightweight filesystem created for microcontrollers with a flash memory chip.  For our project we use this flash memory to store the HTML and CSS files that are used by the controller.  If you want to make any changes to these files then you would need to reload them into the ESP32 flash memory.  This does not happen when you do a normal code upload, which goes into program memory.  You must use a special command to upload into SPIFFS.

Open a terminal and type the command:

 `run -vv -e esp32dev -t uploadfs`
 
All of the files that are in the <i>data</i> directory will be uploaded. 

<h3><span style="float:left">
<a href="trainingRobot">Previous</a></span>
<span style="float:right">
<a href="bom">Next</a></span></h3>