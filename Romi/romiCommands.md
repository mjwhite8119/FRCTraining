# <a name="code"></a>Commands
Commands define high-level robot actions or behaviors that utilize the methods defined by the subsystems. Before looking at the commands that are implemented on the Romi you should be very familiar with [Procedures](../Programming/procedures) and [State Machines](../Programming/stateMachines) from the programming sections.  You should also review the FRC Documentation on [Commands](https://docs.wpilib.org/en/latest/docs/software/commandbased/commands.html) before continuing.

A command is a simple state machine that is either initializing, executing, ending, or idle. Users write code specifying which action should be taken in each state. Subsystems are used by the CommandScheduler resource management system to ensure multiple robot actions are not "fighting" over the same hardware resource. Commands that use a subsystem should include that subsystem in their `getRequirements()` method.

![Commands](../images/Romi/Romi.015.jpeg)

## The CommandScheduler
Runs the Scheduler.  This is responsible for polling buttons, adding newly-scheduled commands, running already-scheduled commands, removing finished or interrupted commands, and running the subsystem `periodic()` methods.  This must be called from the robot's `periodic()` block in order for anything in the Command-based framework to work.

For more details see [The Command Scheduler](https://docs.wpilib.org/en/latest/docs/software/commandbased/command-scheduler.html) documentation.

## Default Commands
The **setDefaultCommand( )** method sets the default Command of the subsystem. The default command will be automatically scheduled when no other commands are scheduled that require the subsystem. Default commands should generally not end on their own, i.e. their Command **isFinished()** method should always return false. Will automatically register this subsystem with the CommandScheduler

## ArcadeDrive Command
Create a new command called **ArcadeDrive**.  In the VSCode file menu right click on the **commands** folder and select "Create a new class/command".  Enter the name of the command in the box.  This will give you a template for creating your new command. 

    import java.util.function.Supplier;

Add the variables that will accept the parameters passed in from the game controller. The variable type is called a *Supplier*, which is an interface used for [Functional Programming Paradigm](https://en.wikipedia.org/wiki/Functional_programming).  This is a more complex programming concept that we won't cover here.

    private final Supplier<Double> m_xaxisSpeedSupplier;
    private final Supplier<Double> m_zaxisRotateSupplier;

Pass the parameters to the ArcadeDrive constructor.  The completed constructor should look like this:

    public ArcadeDrive(
      Drivetrain subsystem,
      Supplier<Double> xaxisSpeedSupplier,
      Supplier<Double> zaxisRotateSuppplier) {
        m_drivetrain = subsystem;
        m_xaxisSpeedSupplier = xaxisSpeedSupplier;
        m_zaxisRotateSupplier = zaxisRotateSuppplier;
        addRequirements(subsystem);
    }

Update the execute() method:

    public void execute() {
      m_drivetrain.arcadeDrive(m_xaxisSpeedSupplier.get(),m_zaxisRotateSupplier.get());
    }

## Use the Joystick
In the `RobotContainer` class create the Joystick object:

    private final Joystick m_controller = new Joystick(0);

Now we'll create a function in the `RobotContainer` class that we'll use the joystick to control the robot:

    public Command getArcadeDriveCommand() {
        return new ArcadeDrive(
            m_drivetrain, () -> -m_controller.getRawAxis(1), () -> m_controller.getRawAxis(2));
      }

## The DriveDistance Command
Another command in the Romi example code is used to drive the robot for a specified distance.  This is where [Parameters](https://www.w3schools.com/java/java_methods_param.asp) are very useful since we can decide how far to drive when the program runs.  This command demonstrates the classic [State Machine](../Programming/stateMachines) programming paradigm where we have an **Initialization Step** `initialize()` followed the **Next Step** `execute()` and an **Input Update** that repeatedly calls `execute()` until that threshold is met `isFinished()` and transititions it to the next major state `end()`.

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


## References

- FRC Documentation - [Command Based Programming](https://docs.wpilib.org/en/latest/docs/software/commandbased/index.html)

- FRC Documentation - [The Command Scheduler](https://docs.wpilib.org/en/latest/docs/software/commandbased/command-scheduler.html)

- [Amazon Example](https://s3.amazonaws.com/screensteps_live/exported/Wpilib/2078/2286/Command_based_programming.pdf?1478686718)

<h3><span style="float:left">
<a href="romiSubsystems">Previous</a></span>
<span style="float:right">
<a href="romiCommandGroups">Next</a></span></h3>