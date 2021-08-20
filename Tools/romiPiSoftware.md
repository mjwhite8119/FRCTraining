# <a name="code"></a>Romi Raspberry Pi Software
The following diagram and describes how the software is structured on the Romi.  The Romi uses a Raspberry Pi and an Arduino based 32U4 microcontroller.  The Raspberry Pi and Romi 32U4 boards are connected via the 40-pin connector, and communicate over I2C. The Romi firmware uses the [Pololu Raspberry Pi interface library for Arduino](https://github.com/pololu/pololu-rpi-slave-arduino-library) to facilitate board-to-board communication. Communication takes place over a "shared memory buffer" which both boards use to read and write to. 

The main entry point for the application is [src/index.ts](https://github.com/wpilibsuite/wpilib-ws-robot-romi/blob/main/src/index.ts). The file is fairly small and serves as a binding layer for the **WPILibWSRomiRobot** class (which is defined in [src/robot/romi-robot.ts](https://github.com/wpilibsuite/wpilib-ws-robot-romi/blob/main/src/robot/romi-robot.ts)) and the **WPILibWSRobotEndpoint** class (which is defined in the wpilib-ws-robot NPM package).

The wpilib-ws-robot package provides a wrapper around the guts of the WPILib WebSocket protocol, and allows developers to easily interface with other kinds of robots, simply by extending from the **WPILibWSRobotBase** class (also exposed by wpilib-ws-robot).

In the `src/romi-robot.ts` file, you can see how the defined class interacts with the Romi firmware over I2C.

This application depends on the **wpilib-ws-robot** package, which in turn depends on **node-wpilib-ws**. The node-wpilib-ws package contains the core classes that implement the WPILib WebSocket protocol, and the code can be found at its [repository](https://github.com/wpilibsuite/node-wpilib-ws).

![RaspberryPi Software](../images/Romi/Romi.003.jpeg)

## References 
[Romi Raspberry Pi - github](https://github.com/wpilibsuite/WPILibPi)

[Romi WPILib Suite - github](https://github.com/wpilibsuite/wpilib-ws-robot-romi)

[RaspberryPi/Arduino Interface - github](https://github.com/pololu/pololu-rpi-slave-arduino-library)

<h3><span style="float:left">
<a href="romi">Previous</a></span>
<span style="float:right">
<a href="romiFirmware">Next</a></span></h3>