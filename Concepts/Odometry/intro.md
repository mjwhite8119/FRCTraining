## Robot Odometry

Odometry involves using sensors on the robot to create an estimate of the position of the robot on the field. In FRC, these sensors are typically encoders to measure position together with a gyro to measure robots' heading. It's important to understand the difference between odometry and kinematics; kinematics deals with movement so we are concerned with speeds, odometry deals with position so we are looking at distance.  

The following diagram shows our objective.  The FRC field is our <i>Global Frame</i>.  We want to know what our **X** and **Y** position is relative to the global frame where the **X** position is represented by the length of the field and the **Y** position is represented by its width.  What we're using here is the <i>Cartesian Coordinate System</i> that you may be familiar with from Algebra.

We also need to know what our heading is, which is represented by the angle between the 𝒙 axis of our coordinate system and the current heading angle of the robot.

![Global Frame](../../images/FRCKinematics&Odometry/FRCKinematics&Odometry.009.jpeg)

So what algorithm is required to compute the robots' odometry?  We can implement this by the following three steps that will require input from the encoders and the gyro (IMU). Remember that our robot code runs in a loop which means that these three steps will execute over and over at about 20 times per second. Each iteration of the loop we will call a <i>time step</i>.

![Odometry Calculation](../../images/FRCKinematics&Odometry/FRCKinematics&Odometry.010.jpeg)

The encoders will send the total linear distance that has been covered by each wheel since the was robot started, or the wheel encoders were reset.  The linear distance is calculated as shown in the following diagram.  **Step 1** of our algorithm will take the total distance covered by the left and right wheel and compute the <i>delta distance</i> travelled by each wheel since the last <i>time step</i>.

![Encoder Position](../../images/FRCKinematics&Odometry/FRCKinematics&Odometry.011.jpeg)

In **step 2** we calculate the distance travelled by the chassis of the robot since the last time step.  This is done by simply taking the delta distance travelled by each wheel and averaging them.  

**Step 3** is where the real work is done to compute our odometry.  From the internal reference frame of the robot it can only travel in the direction parallel to its wheels.  It cannot travel instantainously sideways so in effect the robot has only one direction, which we'll call 𝒙.  However, within the global frame, the FRC field, it can assume a position in both the **X** and **Y** directions.  In order to calculate this we make use of the trigonomic <i>Sine</i> and <i>Cosine</i> functions.  To compute the **X** position we multiple the distance travelled by the <i>Sin</i> of the current heading angle.  The **Y** position is computed using the <i>Cos</i> of the current heading angle.

It's important that this calculation is done based on the change in heading since the last time step. That's why we go to the trouble of computing the delta distance travelled instead of using the total distance.  Consider that the heading will most likely be changing continuouly during our journey.  If we computed the position based solely on our current heading then the calculation would be way off.

![Translation Calculation](../../images/FRCKinematics&Odometry/FRCKinematics&Odometry.012.jpeg)

<h3><span style="float:left">
<a href="../Kinematics/intro">Previous</a></span>
<span style="float:right">
<a href="../Motion/intro">Next</a></span></h3>