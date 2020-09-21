## <a name="code"></a>Code Description
A diagram of the major code components for FRCRobot1 is shown below. The main program unit calls utility functions to connect to WiFi and bring up a Web Server on it's IP address.  The IP address and WiFi connection status is shown on an OLED display.  The Web Server is used to interact with the robot.

The main program creates a <i>Robot</i> class that is composed of a <i>DriveTrain</i> with a left and right <i>Wheel</i>.  Each wheel has it's own <i>DCMotor</i>.  This sets up a differential drive configuration for the robot.

![Robot Model](../images/FRCRobot/FRCRobot.001.jpeg)

This first program implements some very basic functionality.  You can move the robot forward and backward, and have it turn left or right. Because two motors are never the same the robot will most likely not move in a straight line.  This can only be solved by using wheel encoders and a PID loop. This will be implemented in the next code levels.

<h3><span style="float:left">
<a href="build">Previous</a></span>
