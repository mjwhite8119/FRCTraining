# <a name="code"></a>Lesson 1 - Basic Robot Structure
There are four basic components that you'll need to create a program for an FRC robot.  Each component is in a separate file.  

The Main.java file is the starting point for the entire program and calls the Robot class to start building the robot.  You should never need to change this file.

The Robot.java file defines the Robot class 

![Robot Structure](../images/Romi/Romi.002.jpeg)

Rename the class `RomiDriveTrain` to just `DriveTrain`.  After renaming VSCode will prompt you to refactor.  This will find all references to the `RomiDriveTrain` and change them to `DriveTrain`.

## Create the ArcadeDrive Command
Create a new command called ArcadeDrive.

    import java.util.function.Supplier;

Add the suppliers

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
## Add the Joystick
In the `RobotContainer` class create the Joystick object:

    private final Joystick m_controller = new Joystick(0);

Now we'll create a function in the `RobotContainer` class that we'll use the joystick to control the robot:

    public Command getArcadeDriveCommand() {
        return new ArcadeDrive(
            m_drivetrain, () -> -m_controller.getRawAxis(1), () -> m_controller.getRawAxis(2));
      }


<h3><span style="float:left">
<a href="romiExampleCode">Previous</a></span>
<span style="float:right">
<a href="romiCode2">Next</a></span></h3>
