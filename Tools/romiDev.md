# <a name="code"></a>Romi Development Environment
Our primary development environment is going to be the [Romi Robot Kit for FIRST](https://www.pololu.com/product/4022).  The Romi robot is a robot base that can be used by FRC teams preparing for competitions. The kit includes an Arduino compatible 32U4 Control Board and a Raspberry Pi together with software that is maintained by WPILib.

The control board features two H-bridge motor drivers and is designed to connect to the encoders on the included motors to allow closed-loop motor control. It also includes a powerful 5 V switching step-down regulator that can supply up to 2 A continuously, along with a versatile power switching and distribution circuit. A 3-axis accelerometer and gyro enable a Romi 32U4 robot to make inertial measurements, estimate its orientation, and detect external forces. Three on-board pushbuttons offer a convenient interface for user input, while indicator LEDs, a buzzer, and a connector for an optional LCD allow the robot to provide feedback.

![Development Environment](../images/Romi/Romi.002.jpeg)

In order to develop programs for the Romi you have to use and IDE, most commonly VSCode.  The code is compiled and executed on your development laptop and uses the WPILib simulation framework to communicate with the Romi robot.  The gamepad will therefore have to synced with you laptop in order to work with the Romi.  The gamepad can be connected to your laptop via BlueTooth.

The code must be run on an 32U4 development board, which is an embedded Arduino based microcontroller with built-in WiFi.  For the development environment (IDE) we'll be using VSCode.  This is the IDE most commonly used by <i>First Robotics</i> teams.  In order to install code onto the 32U4 microcontoller you have to install the PlatformIO plugin for VSCode. Information about the PlatformIO plugin can be found here:

[Getting Started with PlatformIO](https://dronebotworkshop.com/platformio/)

[How To Install PlatformIO ](https://www.youtube.com/watch?v=5edPOlQQKmo)

## Robot Simulator
Explain the simulator.

![Simulator](../images/Romi/Romi.008.jpeg)

Here's the documentation for the [Robot Simulator](https://docs.wpilib.org/en/stable/docs/software/wpilib-tools/robot-simulation/introduction.html)

Make sure that desktop support is enabled.

## Shuffleboard

![Shuffleboard](../images/Romi/Romi.009.jpeg)

## Raspberry Pi Software
![Development Environment](../images/Romi/Romi.003.jpeg)



<h3>
<span style="float:right">
<a href="romiExample">Next</a></span></h3>