## <a name="code"></a>Basic Robot Structure
The first version that should be installed on the training robot is in branch <i>FRCRobot-version-1</i>. This code branch implements some very basic functionality.  You can move the robot forward and backward, and have it turn left or right. Because two motors are never the same the robot will most likely not move in a straight line.  This can only be solved by using wheel encoders and a PID loop, which will be implemented in a later code branch.

A diagram of the major code components for <i>FRCRobot-version-1</i> is shown below. The main program unit calls utility functions to connect to WiFi and bring up a Web Server on it's IP address.  The IP address and WiFi connection status is shown on an OLED display.  The Web Server is used to interact with the robot.

The main program creates a <i>Robot</i> class that is composed of a <i>DriveTrain</i> with a left and right <i>Wheel</i>.  Each wheel has it's own <i>DCMotor</i>.  This sets up a differential drive configuration for the robot.

![Robot Model](../images/FRCRobot/FRCRobot.001.jpeg)


<h3><span style="float:left">
<a href="trainingRobot">Previous</a></span>
<span style="float:right">
<a href="code2">Next</a></span></h3>
