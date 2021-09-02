# <a name="code"></a>Romi Development Environment
This section explains the development environment that we'll be using for the programming tutorials.

![Development Environment](../images/Romi/Romi.002.jpeg)

## Hardware Platform
Our primary hardware platform is going to be the [Romi Robot Kit for FIRST](https://www.pololu.com/product/4022).  The Romi robot is a robot base that can be used by FRC teams preparing for competitions. The kit includes an Arduino compatible 32U4 Control Board and a Raspberry Pi together with software that is maintained by WPILib.

The control board features two H-bridge motor drivers and is designed to connect to the encoders on the included motors to allow closed-loop motor control. It also includes a 5 volt switching step-down regulator that can supply up to 2 Amps continuously, along with a power switching and distribution circuit. A 3-axis accelerometer and gyro enable a Romi 32U4 robot to make inertial measurements, estimate its orientation, and detect external forces. Three on-board pushbuttons offer an interface for user input, while indicator LEDs, a buzzer, and a connector for an optional LCD allow the robot to provide feedback.

When we move onto the Vision section of the tutorials we'll also make use of a Raspberry Pi camera.

## Software Development IDE

In order to develop programs for the Romi you have to use and IDE.  The most commonly used IDE for FRC is [VSCode](https://code.visualstudio.com/).  The code is compiled and executed on your development laptop.  You'll also need to connect a game controller to your laptop in order to work with the Romi.

## Robot Simulator
 Communication with the Romi is done via the [WPILib Simulation](https://docs.wpilib.org/en/latest/docs/software/wpilib-tools/robot-simulation/index.html) framework to communicate with the Romi robot.  We'll learn a lot more about the Robot Simulator shortly.

![Simulator](../images/Romi/Romi.008.jpeg)

You'll need to make sure that desktop support is enabled to use the Simulator.  This is normally done when you first create your project although it can also be enabled later.

## Shuffleboard

![Shuffleboard](../images/Romi/Romi.009.jpeg)

## Raspberry Pi Software
![Development Environment](../images/Romi/Romi.003.jpeg)



<h3>
<span style="float:right">
<a href="romiExample">Next</a></span></h3>