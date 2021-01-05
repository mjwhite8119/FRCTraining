# <a name="code"></a>Lesson Plan Overview

This section gives an overview of each lesson in this course and is meant to give you a map of where we are going.  A key component of any mobile robot is its <i>Odometry</i> system.  Odometry involves counting wheel rotations to create an estimate of the position of the robot on the field.  To count wheel rotations we use encoders that are connected to each wheel of the robot.  The following diagrams show the progression of lessons.  Each new piece of functionality is highlighted in orange.

The first lesson creates the **Basic Robot Structure** that will be used throughout the course. Each lesson will build on this basic structure to add more functionality. Basic commands are sent to the robot to make it move for a certain period of time.

The second lesson enables the speed of the motors to be controlled using **PWM** signals that are sent to each wheel.  In this lesson you'll see how changing the PWM signal effects the power sent to the motor and therefore the speed.   

![Lessons 1 & 2](../images/FRCRobot/FRCRobot.020.jpeg)

Adding **Wheel Encoders** to our robot is done in lesson 3. These will enable us to more precisely control the velocity and position of the robot in future lessons.  The OLED display will show the number of encoder pulses that are recorded per second.

Now that we have wheel encoders we can **Control the Velocity** of the robot, which we do in lesson 4.  We can tell the robot what velocity to travel at instead of sending power commands. A conversion from velocity values to PWM values is the main feature of this code update. The OLED will now display the robots' velocity instead of the number of encoder pulses.

![Lessons 3 & 4](../images/FRCRobot/FRCRobot.021.jpeg)

Lesson 5 sets up a **PID Loop** to control each individual motor so as the robot will travel in a straight line. Each motor is different and requires a different power level to produce a desired speed.  The PID loop is designed to take care of this.

Lesson 6 brings a **Gyro** into our robot system.  A gyro is used to keep track of the orientation of the robot.  Since our robot only operates in a 2D plane we only need to know one of the three orientation values.  For wheeled robots the orientation is also referred to as the heading.

![Lessons 5 & 6](../images/FRCRobot/FRCRobot.022.jpeg)

When we get to lesson 7 we'll have all the pieces that we need to setup our **Odometry** system. Odometry involves using sensors to estimate the position of the robot on the field.  To describe the data coming from our odometry we introduce the concept of a <i>Pose</i>. This is a data structure that holds the robots' position and orientation.

![Lessons 7](../images/FRCRobot/FRCRobot.023.jpeg)

So that's the plan. The code is installed on a small Arduino based training robot that uses an ESP32 microcontroller.  

<h3><span style="float:left">
<a href="trainingRobot">Previous</a></span>
<span style="float:right">
<a href="code1">Next</a></span></h3>