# <a name="code"></a>Basic Robot Structure
By this point you should have your development environment setup and have ensured that you can communicate with the Romi robot by running the [example program](romiExample).  It's now time to get down the serious work of learning how to program the robot.  We're going to start with an [Introduction to Programming](../Languages/Intro/introProgramming) where you'll get a high level overview of programming concepts.  Then we'll learn a little bit about [Robot Systems](../Concepts/RobotSystem/intro) so as you can understand what it is that you're programming. And after reading those two tutorial you'll be ready to see how the code of an FRC robot is constructed.  

There are four basic components that make up a program for an FRC robot.  The code for each component is in a separate file.  

![Robot Structure](../images/Romi/Romi.010.jpeg)

## The Main Class
The Main.java file is the starting point for the entire program and calls the Robot class to start building the robot.  You should never need to change this file.

## Robot Class
The Robot.java file defines the Robot class 

![Robot Class](../images/Romi/Romi.011.jpeg)

## RobotContainer Class

![RobotContainer Class](../images/Romi/Romi.014.jpeg)

The **setDefaultCommand( )** method sets the default Command of the subsystem. The default command will be automatically scheduled when no other commands are scheduled that require the subsystem. Default commands should generally not end on their own, i.e. their Command **isFinished()** method should always return false. Will automatically register this subsystem with the CommandScheduler

## The Constants File

This file provides a central location for defining constants.  Constants are values assigned to variables that do not change throughout the execution of the program.




Rename the class `RomiDriveTrain` to just `DriveTrain`.  After renaming VSCode will prompt you to refactor.  This will find all references to the `RomiDriveTrain` and change them to `DriveTrain`.




<h3><span style="float:left">
<a href="romiExampleCode">Previous</a></span>
<span style="float:right">
<a href="romiCode2">Next</a></span></h3>
