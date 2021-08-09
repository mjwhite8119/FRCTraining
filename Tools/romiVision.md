# <a name="code"></a>Vision Programming
In this section we'll use the Raspberry Pi camera to control the robot.  You'll need to upload a program to the Raspberry Pi on the Romi in order to run the camera.  The camera program will make use of the open source software called [OpenCV](https://opencv.org/) and can be written in Java, Python, or C++.  In this lesson we'll use the Python programming language to write our camera program.  Why Python? Because most of the programming examples that you'll find online will use Python so if you run into any problems with your program chances you'll find the solution in Python.

![Camera Program Flow](../images/Romi/Romi.024.jpeg)




![Development Environment](../images/Romi/Romi.020.jpeg)

![Development Environment](../images/Romi/Romi.018.jpeg)

![Development Environment](../images/Romi/Romi.021.jpeg)

## Using GRIP to Create a Pipeline
A convenient way to create a frame processing pipeline is to use the FRC tool called 

1. On Mac start from Applications->GRIP
2. Turn on the Romi
3. Add Source -> IP Camera.  Put the URL of the camera stream.  wpilibpi.local:1181/stream.mjpg
4. Follow [FRC GRIP documentation](https://docs.wpilib.org/en/latest/docs/software/vision-processing/grip/index.html) to create the filter.
The last filter should be Find Contours.
5. Generate the code Tools->Generate Code.  
6. Select Python as the output language.
7. Use `GripPipeline` as the class name.
8. Put it into the main directory of you camera server project.
9. The module name can be `grip`.

If you're generating the java pipeline version make sure the the "Implement WPILIB VisionPipeline" box is checked.  This will place the following code into the generated GRIP file:

    import edu.wpi.first.vision.VisionPipeline;

The class definition will look like this:

    public class GripPipeline implements VisionPipeline {

## Update your Camera Server Program





### Display the Tracking View in Shuffleboard
Shuffleboard uses the Network Tables to display the camera data so your java program must be running in order to see the live camera stream.

## Upload Python Program
1. cd ~/Documents/romi-examples/python-multiCameraServer
2. The python program has multiple files so you need to upload them all.  This is done with a zip file.  Run `python3 build` to build the zip file.
3. On the Romi WPILibPi.local webpage. Go to **Application**.
4. Put Raspberry Pi file system into Writable mode.
5. In the **File Upload** select the file wpilib.tar.gz file for upload.  Make sure that file extract is selected. Click the **Upload** button.
6. Select "Uploaded Python file" in the dropdown.
7. Select multiCameraServer.py for the file.  You only need to upload this if you change it, which shouldn't be very often. 

Issues:

The runCamera file keeps getting overwritten when you upload a new multiCameraServer.py file.  So just upload the tar file and then `Terminate` the application on the **Vision Status** page, and then press the `Up` button.

![Upload Camera Program](../images/Romi/Romi.019.jpeg)

## Upload Java Program
1. cd ~/Documents/romi-examples/java-multiCameraServer
2. run `./gradlew build` to build the jar file.  Make sure that the build is successful.
3. On the Romi WPILibPi.local webpage, click on **Application** in the left panel.
4. Put into Writable mode
5. Select "Uploaded Java jar" in the dropdown.
6. Click on **Choose File** file and upload the file `build/libs/java-multiCameraServer-all.jar`.

## Test your Program
Run the your java program from VSCode. In the Simulator you will see the Network Tables showing the data coming in from the python camera server program.  You can use this data to control the robot.

## References
[OpenCV](https://opencv.org/)

[GRIP documentation](https://docs.wpilib.org/en/latest/docs/software/vision-processing/grip/index.html)

<h3><span style="float:left">
<a href="romiFirmware">Previous</a></span>