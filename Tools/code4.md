# <a name="code"></a>Lesson 4 - Open Loop Velocity Control
Up to this point we have been using PWM signals to directly power the motors. To simplify our motion control commands it would be better to send a velocity value between -1 and +1, where -1 is full speed backwards and +1 is full speed forward. This gives us a smooth transition of velocity values which are easy to understand and hides the messy details of the PWM signals. 

Another lesson objective is to begin to understand <i>Control Systems</i>.  Control systems are used extensively in robotics.

## Open Loop vs Closed Loop Control
There are two main control system mechanisms, <i>Open Loop</i> and <i>Closed Loop</i>.  For an open loop system you just set an input control signal and let it go. There's no adjustment along the way. The system doesn't self correct itself.  The only way to change the signal is through manual input. This is the system that we've been using so far to control our robot. We set a PWM value for the motor and that same PWM value remains until the system times out.  We'll continue to use the open loop system in this lesson.  

An <i>Open Loop</i> verses <i>Closed Loop</i> system is shown below.  The closed loop system takes input from it's sensors and uses that information to adjust the control signal to the motor.  In the next lesson we'll switch to a closed loop system. 

![Open Loop Control](../images/FRCRobot/FRCRobot.010.jpeg)

## Wheel Velocity Proportional Values
So instead of sending a PWM signal to the motors we just want to send a value between -1 and +1.  Where +1 is full speed forward and -1 is full speed backward. From the perspective of the controller that will look like this:

![Lesson 4 Controller](../images/FRCRobot/FRCRobot.012.jpeg)

As you can see, we no longer need the <i>Backward</i> buttons since we can set the speed to a negative value. In fact, we need fewer and fewer buttons for each lesson.  Why is this important?  We have reduced our control input to a single velocity command <i>Move</i>, and we can get the robot to go wherever we want by feeding it a continuous stream of these velocity command values for each wheel. 

The <i>DCMotor</i> model is very similar to that of lesson 3.  The difference is that we pass in the velocity value instead of the PWM. The motor still wants PWM signals so the velocity value has to be converted to a PWM value, this is done in the `setSpeed()` function. 

![DCMotor](../images/FRCRobot/FRCRobot.015.jpeg)

## Drivetrain Characterization

There is one thing that needs to be taken into consideration while doing the conversion from a speed value to PWM.  The motor won't start to turn until a minimum PWM value has been reached. Therefore, we'll need to add this value before we apportion our speed control values....

![Wheel Speed Chart](../images/FRCRobot/FRCRobot.018.jpeg)

## Calculating Velocity

Instead of outputting the number of pulses per second to the OLED, we're now going to display the speed of our robot in meters per/second.  To do this we'll need to get the diameter of our wheels so that we can calculate the linear distance travelled for each wheel rotation.  This process is shown in the following diagram.

![Wheel Linear Distance](../images/Kinematics&Odometry/Kinematics&Odometry.004.jpeg)

Once we know the distance for each wheel rotation we can figure out how the robot travels for each encoder pulse.  We can then then multiple this value by the number of encoder pulses per second to get the average velocity per second of the robot.  This is summarized in the following illustration.

![Wheel Velocity](../images/Kinematics&Odometry/Kinematics&Odometry.005.jpeg)

<h3><span style="float:left">
<a href="code3">Previous</a></span>
<span style="float:right">
<a href="code5">Next</a></span></h3>