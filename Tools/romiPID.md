# <a name="code"></a>PID and Line Following
In this section we'll learn about PID control and use it to get the Romi to follow a line marked on the floor.  First we'll code our own simple controller so as we can learn about the basics of PID.  Then we'll implement the PID controller supplied by WPILib.  Before completing this section you should read the [PID Control documentation](https://docs.wpilib.org/en/latest/docs/software/commandbased/pid-subsystems-commands.html) provided by First Robotics.

Our PID command is going to look like the following diagram.  We'll set the **Proportional** part to be 0.015.  Why?  The center line is coming in from the camera and becomes our measurement source.  We need to keep the center line at x=75 so that's becomes the setpoint.  The output is the turn angle going to the left and right motors.  Every command must have a subsystem requirement and in this case it would be the drive train. 

![PID Command](../images/Romi/Romi.025.jpeg)

## Camera Code Update
Before we can implement the line following command we'll need a line to follow.  This is sent to us by the Camera Server that will send center line back to use via the Network Tables.

## Home Made PID Controller
As we have learned, the PID controller has three components.  However, we are only going to use the first one which is the **Proportional** part.  We'll put our controller in the `execute()` method of our command.

## WPILib PID Controller
Use the WPILib `PIDCommand` to control the motors to follow the line.

## References
[FRC Documentation - PID Control](https://docs.wpilib.org/en/latest/docs/software/commandbased/pid-subsystems-commands.html)

[FRC Documentation - Controllers](https://docs.wpilib.org/en/latest/docs/software/advanced-controls/controllers/index.html)

[Controls Engineering in FRC](https://file.tavsys.net/control/controls-engineering-in-frc.pdf)


<h3><span style="float:left">
<a href="romiVision">Previous</a></span>
<span style="float:right">
<a href="romiServos">Next</a></span></h3>