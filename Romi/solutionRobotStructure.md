## Robot Structure Solutions
The *Constants* file can end up getting very crowded so it's a good idea to group the constants under the appropriate subsystem as much as possible.  To do that we can create a subclass within the Constants file.  In our case, we've called this *DriveConstants*.   Update the Constants file with the following code.  You can cut and paste the two lines from the Drivetrain class.  You must also change the constant from `private` to `public`. 

    public final class Constants {
        public final class DriveConstants {
            public static final double kCountsPerRevolution = 1440.0;
            public static final double kWheelDiameterInch = 2.75591; // 70 mm
        }
    }    

Now go to the Drivetrain class and comment out the two lines that you just copied.  Reference the new constants in the `setDistancePerPulse` method in the Drivetrain constructor. You'll be prompted to import the *DriveConstants* class that you created in the *Constants* file.

    m_leftEncoder.setDistancePerPulse((Math.PI * DriveConstants.kWheelDiameterInch) / DriveConstants.kCountsPerRevolution);
        m_rightEncoder.setDistancePerPulse((Math.PI * DriveConstants.kWheelDiameterInch) / DriveConstants.kCountsPerRevolution);
    
### Quiz Answers
