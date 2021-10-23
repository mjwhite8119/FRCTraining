# Motion Control PID
In this lesson we're going to add a new command that'll give us more control over how the robot moves.  The subject of Motion Control is part of a larger disipline called [Control Systems Engineering](https://en.wikipedia.org/wiki/Control_engineering). We'll just touch the surface of that disipline here but for a more in-depth explaination refer to [Classical Control](../Concepts/Control/classicalControl) section.

One of the key Control Systems algorithms is the **PID Controller**, so we'll start with that and see how it can be put it into Commands used by our robot. Finally, we'll learn some basics about tuning a PID Controllers.  

In this section we'll create some new commands that we'll test from the *AutonomousDistance* group command.

- *DriveDistancePID* that will drive the robot in a straight line.

- *TurnDegreesPID* that will allow the robot to turn to a specified angle.  

After that, we'll create two commands to move the robot more smoothly to the desired setpoints, and is an example of a methodology called **Motion Profiling**.

- *DriveDistanceProfiled* that will use a Trapezoid Profile trajectory to drive the robot in a straight line.

- *TurnDegreesProfiled* that will use a Trapezoid Profile trajectory to turn the robot.

## PID Controller
Before looking at the PID controller supplied by the WPI library, it would be useful to get an understanding of what PID control is by watching the [PID Introduction Video by WPI](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/pid-video.html). A schematic of WPIlib PIDController is below with a detailed explaination found in the [Introduction to PID](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/introduction-to-pid.html) section of the FRC® documentation.

![PID Controller](../images/Romi/Romi.042.jpeg)

## The DriveDistancePID Command
Under the commands folder right click and select "Create a new class/command".  The select **PIDCommand** from the drop down.

![Commands](../images/Romi/Romi.041.jpeg)

The first thing we need is the **PIDController** class that simply specifies what the P, I, and D values are.  Since these values are constants they should be put in the *Constants* file.  The *PIDController* class is where all of the work is done and was explained in the previous section.

We add the *Drivetrain* as a requirement and tell the command what distance we want to drive.  This distance becomes the **setpoint** for the PID controller.  These two parameters are passed in when the *DriveDistancePID* constructor is called and the Command object is created.

The **measurementSource** and **output** setup a looping arrangement which moves the robot towards the **setpoint**.  In our case, the measurement source are the encoders and the output is sent to the motors in order to move the robot. Once the setpoint is reached the command will finish.

![PID Command](../images/Romi/Romi.047.jpeg)

The full constructor for our **DriveDistancePID** command is listed below.

    public DriveDistancePID(double targetDistance, Drivetrain drive) {
        super(
            // The controller that the command will use
            new PIDController(DriveConstants.kDistanceP, 
                              DriveConstants.kDistanceI, 
                              DriveConstants.kDistanceD),
            // This should return the measurement
            drive::getAverageDistanceInch,
            // This should return the setpoint (can also be a constant)
            targetDistance,
            // This uses the output
            output -> {
              // Use the output here
              drive.steer(output/10);
            },
            // Use addRequirements() here to declare subsystem dependencies.
            drive);
        
        // Configure additional PID options by calling `getController` here.
        getController().setTolerance(DriveConstants.kDistanceToleranceInch,
                                    DriveConstants.kVelocityToleranceInchPerS);
      }

The `setTolerance()` method sets the position and velocity error which is considered tolerable for use with the setpoint. For more details on what we've just done read the [PID Control through PIDSubsystems and PIDCommands](https://docs.wpilib.org/en/latest/docs/software/commandbased/pid-subsystems-commands.html#) section of the FRC® documentation.

## Profiled PID Controller

A major difference between a standard *PIDController* and a *ProfiledPIDController* is that the actual setpoint of the control loop is not directly specified by the user. Rather, the user specifies a goal position or state, and the setpoint for the controller is computed automatically from the generated motion profile between the current state and the goal. 

![PID Command](../images/Romi/Romi.043.jpeg)

The specified goal value is not necessarily the current setpoint of the loop - rather, it is the eventual setpoint once the generated profile terminates.

A common FRC® controls solution is to pair a [Trapezoidal Motion Profile](../Concepts/timeMotion#TrapezoidProfile) to generate setpoints with a PID controller for tracking the setpoint.

## The DriveDistanceProfiled Command
With the *DriveDistancePID* command there's no way of avoiding the sudden accelerations and changes in velocity at the beginning of the move, which makes it difficult to tune the PID controller to arrive at the setpoint.  It would be better if we can move more smoothly to the setpoint by gradually accelerating and decelerating at the beginning and end of the movement. To facilitate this, WPILib includes its own *ProfiledPIDController* class. Let's see if we can improve upon the results of the *DriveDistancePID* command.  

Under the commands folder right click and select "Create a new class/command".  The select **ProfiledPIDCommand** from the drop down.

![Commands](../images/Romi/Romi.041.jpeg)

Instead of using the *PIDController* class we'll use the *ProfiledPIDController* that we just looked at.  This class specifies P, I, and D values together with velocity and acceleration constraints.  For now we'll set these constraints to 1.5 and 2.0 respectively.  You'll find out how we got these values when you learn about **Robot Characterization** in the next section.

We'll again add the *Drivetrain* and *targetDistance* parameters to the constructor.  However, this time the targetDistance will be passed into the ProfiledPIDController as a *TrapezoidProfile.state*.  We'll use the encoders as the measurement source as we did in the last command.

![PID Command](../images/Romi/Romi.048.jpeg)

### Tuning the PID Controller
To get the PID controller to perform properly it will will most likely need to be tuned.  The [Tuning a PID Controller](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/tuning-pid-controller.html) documentation gives some information on the process.

To tune the PID controller you will need to start Shuffleboard. The PID Controller parameters *setpoint, P, I*, and *D* can be found under LiveWindow.  You can pull these onto the *Drive* tab if you wish.  We would want to change the PID values from Shuffleboard and see the results without restarting our program.  To do this we will add in the Network Tables instance and table to our program:

    private static NetworkTableInstance inst = NetworkTableInstance.getDefault();
    private static NetworkTable table = inst.getTable("Shuffleboard/Drivetrain");

Override the PID command's `initialize()` method to update the *P* and *D* parameters:

    public void initialize() {
      super.initialize();
      // Override PID parameters from Shuffleboard
      getController().setP(table.getEntry("kP").getDouble(1.0));
      getController().setD(table.getEntry("kD").getDouble(0.0));
    }

You can also override the `execute()` method to add Shuffleboard diagnostics.

    public void execute() {
      super.execute();
      SmartDashboard.putNumber("Pos. Error", getController().getPositionError());
      SmartDashboard.putBoolean("atGoal", getController().atGoal());
    }

View [Testing and Tuning PID Loops](https://docs.wpilib.org/en/stable/docs/software/wpilib-tools/shuffleboard/advanced-usage/shuffleboard-tuning-pid.html)

<!-- ## The TurnDegreesPID Command
Under the commands folder right click and select "Create a new class/command".  The select **PIDCommand** from the drop down.

![Commands](../images/Romi/Romi.041.jpeg)

The first thing we need is a **PID Controller** that simply specifies what the P, I, and D values are.  Since these values are constants they should be put in the *Constants* file.  The *PIDController* class is where all of the work is done and was explained in the previous section.

We add the *Drivetrain* as a requirement and tell the command what angle we want to rotate to.  This angle becomes the **setpoint** for the PID controller.  These two parameters are passed in when the *TurnToAngle* constructor is called and our command object is created.

The **measurementSource** and **output** setup a looping arrangement which moves the robot towards the **setpoint**.  In our case, the measurement source is a gyro and the output is sent to the motors in order to turn the robot. Once the setpoint is reached the command will finish.

![PID Command](../images/Romi/Romi.043.jpeg)

The full constructor for our **TurnToAngle** command is listed below.

    public class TurnToAngle extends PIDCommand {
    
      public TurnToAngle(double targetAngleDegrees, Drivetrain drive) {
        super(
            // The controller that the command will use
            new PIDController(DriveConstants.kTurnP, DriveConstants.kTurnI, DriveConstants.kTurnD),
            // This should get the measurement
            drive::getHeading,
            // This should return the setpoint (can also be a constant)
            targetAngleDegrees,
            // This uses the output
            output -> {
              // Use the output here
              drive.arcadeDrive(0, output);
            },
            drive);
          
      getController().enableContinuousInput(-180, 180);
      getController().setTolerance(DriveConstants.kTurnToleranceDeg,
                                  DriveConstants.kTurnRateToleranceDegPerS);
  }

 `setTolerance(5, 10)` sets the position and velocity error which is considered tolerable for use with the setpoint. For more details on what we've just done read the [PID Control through PIDSubsystems and PIDCommands](https://docs.wpilib.org/en/latest/docs/software/commandbased/pid-subsystems-commands.html#) section of the FRC® documentation. -->

### Setting up the Gyro    
There are a few of things we need to do in order to setup the gyro as a measurement source.  

The first is to understand which of the three angles represent the robot's heading.  From our discussion on robot [geometry](../Concepts/geometry) we can see that the heading is represented by the Z-axis.  To make sure that we remember that let's create a wrapper around the Z-axis.

    public double getHeading() {
        return getGyroAngleZ();
      }

Ensure that the gyro is calibrated, which is done on the Romi Website.  Follow the [IMU Calibration](https://docs.wpilib.org/en/stable/docs/romi-robot/web-ui.html#imu-calibration) instructions.

The gyro on the Romi shows continuous angles and does not reset when it reaches 360 degrees.  In order for our PID controller to work we need to reset the angle to zero degrees when it passes 360 or -360 degrees.

`enableContinuousInput(-180, 180)` Rather then using the max and min input range as constraints, it considers them to be the same point and automatically calculates the shortest route to the setpoint.

Lastly, we should reset the gyro angles each time we start the program.  This is done in the Drivetrain constructor where is calls its own `resetGyro()` method.


## The TurnToAngleProfiled Command
With the *TurnToAngle* command there's no way of avoiding the sudden accelerations and changes in velocity, which makes it difficult to tune the PID controller to arrive at the setpoint angle.  It would be better if we can move more smoothly to the setpoint by gradually accelerating and decelerating at the beginning and end of the movement.  A common FRC® controls solution is to pair a [Trapezoidal Motion Profile](../Concepts/timeMotion#TrapezoidProfile) to generate setpoints with a PID controller for tracking the setpoint. To facilitate this, WPILib includes its own *ProfiledPIDController* class.

A major difference between a standard *PIDController* and a *ProfiledPIDController* is that the actual setpoint of the control loop is not directly specified by the user. Rather, the user specifies a goal position or state, and the setpoint for the controller is computed automatically from the generated motion profile between the current state and the goal. 

![PID Command](../images/Romi/Romi.046.jpeg)

## References

- FRC Documentation - [PID Basics](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/index.html)

- FRC Documentation - [PID Control through PIDSubsystems and PIDCommands](https://docs.wpilib.org/en/latest/docs/software/commandbased/pid-subsystems-commands.html#)

- FRC Documentation - [Motion Profiling through TrapezoidProfileSubsystems and TrapezoidProfileCommands](https://docs.wpilib.org/en/latest/docs/software/commandbased/profile-subsystems-commands.html)

- FRC Documentation - [Combining Motion Profiling and PID in Command-Based](https://docs.wpilib.org/en/latest/docs/software/commandbased/profilepid-subsystems-commands.html)

- FRC  Documentation - [PID Control in WPILib](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/controllers/pidcontroller.html)

- Code Example - [BasicPID](https://github.com/mjwhite8119/romi-examples/tree/main/BasicPID)

<h3><span style="float:left">
<a href="romiShuffleboard">Previous</a></span>
<span style="float:right">
<a href="romiPathPlanning">Next</a></span></h3>