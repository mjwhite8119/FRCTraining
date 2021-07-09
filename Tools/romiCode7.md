# <a name="code"></a>Programming Servos

The following diagram shows you how to connect the servos to the Romi's GPIO pins. The power connections for the GPIO channels are initially left unconnected, but should be hooked into the Romi’s on-board 5V supply by using a jumper to connect the 5V pin to the power bus. Additionally, if more power than the Romi can provide is needed, the user can provide their own 5V power supply and connect it directly to power bus and ground pins.

Connect the servos to EXT3 and EXT4 as shown in the diagram.  The ground wire (black or brown) goes towards the outside of the board. Then go to the **Romi** section of the Romi Web UI and ensure that the ports are set to PWM.

![Servo Configuration](../images/Romi/Romi.004.jpeg)

The servos are controlled via buttons on the gamepad.  Your WPI based program runs on the laptop and launches the Robot Simulator tool.  The simulator communicates with the NodeJS application that runs on the Raspberry Pi. This application passes requests onto the microcontroller to control the GPIO ports that the servos are connected to.

![Servo Control](../images/Romi/Romi.006.jpeg)

The following sections explain the how to create the java classes that your WPI program needs to control the servos.

## Create the RomiServo Subsystem
This class will use the Servo base class provided by the WPI library.

    import edu.wpi.first.wpilibj.Servo;

Create a method to reset the servo position.

    // Reset position to resting state
      public void reset() {
        m_liftPos = 0.5;
        m_tiltPos = 0.5;
        
        m_lift.set(m_liftPos);
        m_tilt.set(m_tiltPos);
      }

Implement tilt motor position

    /** 
      * Increment tilt motor position
      * 
      * @param delta Amount to change motor position
      */
      public void incrementTilt(double delta) {
        m_tiltPos = saturateLimit(m_tiltPos + delta, Constants.Servo.TILT_MIN, Constants.Servo.TILT_MAX);
        m_tilt.set(m_tiltPos);
      }

## Create ServoCommand
This command will use a joystick to control the RomiServo subsystem. 

    import frc.robot.subsystems.RomiServo;
    import edu.wpi.first.wpilibj.Joystick;

As always, the subsystem is added as a command requirement.

    public ServoCommand(RomiServo romi_servo, Joystick joystick) {
    m_servo = romi_servo;
    m_joystick = joystick;

    addRequirements(romi_servo);
  }

Code used to move the servos using the joystick.

    public void execute() {

    if(m_joystick.getRawButton(Constants.Joystick.TOPLEFT)) {
      m_servo.incrementLift(-Constants.Servo.SERVO_INCREMENT);
      System.out.println("Lift -" );
    }
    if(m_joystick.getRawButton(Constants.Joystick.TOPRIGHT)) {
      m_servo.incrementLift(Constants.Servo.SERVO_INCREMENT);
      System.out.println("Lift +" );
    }
    if(m_joystick.getRawButton(Constants.Joystick.BOTTOMLEFT)) {
      m_servo.incrementTilt(Constants.Servo.SERVO_INCREMENT);
      System.out.println("Tilt +" );
    }
    if(m_joystick.getRawButton(Constants.Joystick.BOTTOMRIGHT)) {
      m_servo.incrementTilt(-Constants.Servo.SERVO_INCREMENT);
      System.out.println("Tilt -" );
    }
  }

## Add Servo to the RobotContainer.
Now that we have a Servo subsystem and command we need to add it to the robot structure via the **RobotContainer** class.  We first need to import it, so open the RobotContainer.java file and the import near the top.

    import frc.robot.subsystems.RomiServo;

Create a varible to point to the RomiServo class.

    private final RomiServo m_servo = new RomiServo();

Inside the **configureButtonBindings()** method create a default command for the servo.  Remember that the default command is run whenever there is no other command using the subsystem.  The joystick will be used to control the servo so that also needs to passed to the **ServoCommand**.

    m_servo.setDefaultCommand( new ServoCommand(m_servo, m_controller));



<h3><span style="float:left">
<a href="romiCode6">Previous</a></span>
