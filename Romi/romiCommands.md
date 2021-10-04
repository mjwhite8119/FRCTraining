# <a name="code"></a>Commands
Commands define high-level robot actions or behaviors that utilize the methods defined by the subsystems. Before looking at the commands that are implemented on the Romi you should be very familiar with [Procedures](../Programming/procedures) and [State Machines](../Programming/stateMachines) from the programming sections.  You should also review the FRC Documentation on [Commands](https://docs.wpilib.org/en/latest/docs/software/commandbased/commands.html) before continuing.

A command is a simple state machine that is either *Initializing*, *Executing*, *Ending*, or *Idle*. Users write code specifying which action should be taken in each state.  Commands run when scheduled or in response to buttons being pressed on a gamepad or from [Shuffleboard](../Tools/shuffleboard). Each command has code in its `execute()` method to move it further along towards its goal and a method `isFinished()` that determines if the command has reached the goal. The `execute()` and `isFinished()` methods are called repeatedly.

![Commands](../images/Romi/Romi.015.jpeg)

## The DriveDistance Command
Let's take a look at the *DriveDistance* command to see how this all works. This command is used to drive the robot for a specified distance.  This is where [Parameters](https://www.w3schools.com/java/java_methods_param.asp) are very useful since we can decide how far to drive when the program runs.  This command demonstrates the classic [State Machine](../Programming/stateMachines) programming paradigm where we have an **Initialization Step** `initialize()` followed the **Next Step** `execute()` and an **Input Update** that repeatedly calls `execute()` until that threshold is met `isFinished()` and transititions it to the next major state `end()`.  After this state the command becomes *Idle*.

        public DriveDistance(double speed, double inches, Drivetrain drive) {
            m_distance = inches;
            m_speed = speed;
            m_drive = drive;
            addRequirements(drive);
        }

        // Called when the command is initially scheduled.
        public void initialize() {
            m_drive.arcadeDrive(0, 0);
            m_drive.resetEncoders();
        }

        // Called every time the scheduler runs while the command is scheduled.
        public void execute() {
            m_drive.arcadeDrive(m_speed, 0);
        }

        // Called once the command ends or is interrupted.
        public void end(boolean interrupted) {
            m_drive.arcadeDrive(0, 0);
        }

        // Returns true when the command should end.
        public boolean isFinished() {
            // Compare distance travelled from start to desired distance
            return Math.abs(m_drive.getAverageDistanceInch()) >= m_distance;
        }


## ArcadeDrive Command
The *ArcadeDrive* command is a simple command that will drive the robot using  values provided by the joysticks. The values are passed in as parameters with a variable type is called a *Supplier*, which is an interface used for [Functional Programming Paradigm](https://en.wikipedia.org/wiki/Functional_programming).  This is a more complex programming concept that we won't cover here.  This parameter type needs to be imported and defined before use.

    import java.util.function.Supplier;

    private final Supplier<Double> m_xaxisSpeedSupplier;
    private final Supplier<Double> m_zaxisRotateSupplier;

The constructor looks like this with the values for linear and angular speed together with the Drivetrain subsystem.

    public ArcadeDrive(
      Drivetrain subsystem,
      Supplier<Double> xaxisSpeedSupplier,
      Supplier<Double> zaxisRotateSupplier) {
        m_drivetrain = subsystem;
        m_xaxisSpeedSupplier = xaxisSpeedSupplier;
        m_zaxisRotateSupplier = zaxisRotateSuppplier;
        addRequirements(subsystem);
    }

The `execute()` method calls the Drivetrain subsystem to activate the motors.

    public void execute() {
      m_drivetrain.arcadeDrive(m_xaxisSpeedSupplier.get(),m_zaxisRotateSupplier.get());
    }

The `isFinished()` method always returns false meaning this command never
completes on it's own. The reason we do this is that this command will be set as the default command for the subsystem. This means that whenever the subsystem is not running another command, it will run this command. If any other command is scheduled it will interrupt this command, then return to this command when the other command completes. 

    public boolean isFinished() {
        return false;
    }

The `setDefaultCommand()` method sets the default Command of the subsystem. The default command will be automatically scheduled when no other commands are scheduled that require the subsystem.  The following statement is called in the *RobotContainer* class.

    m_drivetrain.setDefaultCommand(getArcadeDriveCommand());

## Use the Joystick
The Joystick object is created in the *RobotContainer* class.

    private final Joystick m_controller = new Joystick(0);

A method is created in the class that uses the joystick to control the robot:

    public Command getArcadeDriveCommand() {
        return new ArcadeDrive(
            m_drivetrain, () -> -m_controller.getRawAxis(1), () -> m_controller.getRawAxis(2));
    }

## The CommandScheduler
Runs the Scheduler.  This is responsible for polling buttons, adding newly-scheduled commands, running already-scheduled commands, removing finished or interrupted commands, and running the subsystem `periodic()` methods.  This must be called from the robot's `periodic()` block in order for anything in the Command-based framework to work.

For more details see [The Command Scheduler](https://docs.wpilib.org/en/latest/docs/software/commandbased/command-scheduler.html) documentation.

## References

- FRC Documentation - [Command Based Programming](https://docs.wpilib.org/en/latest/docs/software/commandbased/index.html)

- FRC Documentation - [The Command Scheduler](https://docs.wpilib.org/en/latest/docs/software/commandbased/command-scheduler.html)

- [Amazon Example](https://s3.amazonaws.com/screensteps_live/exported/Wpilib/2078/2286/Command_based_programming.pdf?1478686718)

<h3><span style="float:left">
<a href="romiSubsystems">Previous</a></span>
<span style="float:right">
<a href="romiCommandGroups">Next</a></span></h3>