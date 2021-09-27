# <a name="code"></a>Joystick Controllers
A joystick/gamepad can be connected to your laptop via a USB port or Bluetooth.  The WPI Library provides all of the necessary software to interface with XBox, PS3/4, or Logitech game controllers.

![Joysticks](../images/Romi/Romi.032.jpeg)

In the `RobotContainer` class create the Joystick object:

    private final Joystick m_controller = new Joystick(0);

Configure joystick buttons to run commands.

## Slew Rate Filter

<h3><span style="float:left">
<a href="romiStructure">Previous</a></span>
<span style="float:right">
<a href="romiSubsystem">Next</a></span></h3>