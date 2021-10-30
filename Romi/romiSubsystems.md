# <a name="top"></a>Subsystems

Subsystems are the basic units of functionally for our robot, such as drive trains and mechanical arms.  They encapsulate low-level hardware objects (motor controllers, sensors, etc) and provide methods that can be used by Commands.  We represent subsystems in code by using [Objects](../Programming/objects). Objects are composed of [Data Structures](../Programming/dataStructures) and [Procedures](../Programming/procedures), as explained in [Introduction to Programming](../Programming/introProgramming). You should learn those concepts before we look at the subsystems that are on the Romi.  

 For this module the majority of the code implementation can be found in the [Subsystems](https://docs.wpilib.org/en/latest/docs/software/commandbased/subsystems.html) section of the FRC Documentation.  

![Subsystems](../images/Romi/Romi.012.jpeg)

## DriveTrain Subsystem
The Romi uses a drive train called a [Differential Drive](https://docs.wpilib.org/en/stable/docs/software/actuators/wpi-drive-classes.html#using-the-differentialdrive-class-to-control-differential-drive-robots). There are three types of Differential [Drive Train Modes](https://docs.wpilib.org/en/stable/docs/software/actuators/wpi-drive-classes.html#drive-modes) that can be implemented. The Romi will make use of at least two of them. To understand what type of maneuvers are possible using a Differential Drive robots you can look at the [Robot Kinematics](../Concepts/Dynamics/kinematics) module. The *DifferentialDrive* class takes the left and right motors as parameters that are wrapped in the *PWMSpeedController* class.  The primary task of the *DifferentialDrive* class is to convert a single speed (unicycle model) into speed for the left and right side of the chassis.

![Differential Drive](../images/Romi/Romi.038.jpeg)

The primary job of the *Drivetrain* subsystem is to send speed commands to its motors.  This is done in the `arcadeDrive()` method where we pass in the required translational and rotational speed.  The *DifferentialDrive* object will take care of controlling the speed to the left and right motors based on the kinematics of the drivetrain type. 

    public void arcadeDrive(double xaxisSpeed, double zaxisRotate) {
        m_diffDrive.arcadeDrive(xaxisSpeed, zaxisRotate);
      }

Other procedures in the Drivetrain class will take care of resetting and reading the wheel encoders.  It'll also translate the wheel encoder values into distances, as explained in the [Pose Estimation](../Concepts/OptimalEstimation/odometry) module.

## RomiGyro Subsystem
The RomiGyro subsystem reads values from its gyro in order to perform [Pose Estimation](../Concepts/OptimalEstimation/odomety). The raw data that comes from gyros is very complex and difficult to intepret.  The RomiGyro subsystem translates the data into simple angles and rates-of-turn that are much easier to understand.

## Subsystems Lab
There are three tasks for this lab:

- Modify Drivetrain to change inches to meters.
- Create a method to get the current heading of the robot.
- Update the RomiGyro to make use of an Interface.

### Change Inches to Meters
This is an exercise to change the distance from inches to meters.  [solution](solutionInchMeters)

### <a name="heading"></a>Create Heading Method
In future modules we're going to need to get the current heading of the Drivetrain.  This heading is obtained from the Gyro that is defined as a subsystem of the Drivetrain as indicated above.

The first is to understand which of the three angles represent the robot's heading.  From our discussion on [Position and Orientation](../Concepts/OptimalEstimation/geometry) we can see that the heading is represented by the Z-axis.  To make sure that we remember that let's create a wrapper around the Z-axis.

Create the heading:

    public double getHeading() {
      return m_gyro.getRotation2d().getDegrees();
    }

Also, the gyro on the Romi shows continuous angles and does not reset when it reaches 360 degrees.  In order for our PID controller to work we need to reset the angle to zero degrees when it passes 360 or -360 degrees.  The new `getHeading()` method is shown below.

    public double getHeading() {
      double angle = getGyroAngleZ();
      double rotations = Math.round(angle/360);
      double heading = angle - (rotations*360);
      return heading;
    }

We also need to be able to reset the heading:

    public void zeroHeading() {
      m_gyro.reset();
    }


### Add Interface to RomiGyro
Have the *RomiGyro* class implement Gyro:

    import edu.wpi.first.wpilibj.interfaces.Gyro;

    public class RomiGyro implements Gyro {
      ...

We are now required to implement all of the methods in the interface that we haven't already implemented.  These can be placed at the end of the file:

    @Override
    public void close() throws Exception {
      if (m_gyroSimDevice != null) {
        m_gyroSimDevice.close();
      }
    }

    @Override
    public void calibrate() {
      // no-op
    }

    @Override
    public double getAngle() {
      return getAngleZ();
    }

    @Override
    public double getRate() {
      return getRateZ();
    }

You'll need to create an object variable `m_gyroSimDevice` placed before the constructor.

    private SimDevice m_gyroSimDevice;

## References
- FRC Documentation - [Subsystems](https://docs.wpilib.org/en/latest/docs/software/commandbased/subsystems.html)

- FRC Documentation - [Differential Drive Robots](https://docs.wpilib.org/en/stable/docs/software/actuators/wpi-drive-classes.html)

- QUT Robot Academy [Measuring Motion](https://robotacademy.net.au/masterclass/measuring-motion/)

<h3><span style="float:left">
<a href="romiJoysticks">Previous</a></span>
<span style="float:right">
<a href="romiCommands">Next</a></span></h3>