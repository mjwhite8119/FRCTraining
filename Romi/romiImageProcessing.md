# <a name="code"></a>Image Processing
In the previous module we got the camera streaming images to Shuffleboard and put image related data into the Network Tables for further processing.  In this module you'll learn how to process camera images to extract certain features.  For this module we'll extract a line that's marked on the floor.  The line should be a distinctive color that doesn't blend in with the surrounding colors.  During this lesson we'll decide on a color and tune the camera in to lock onto that color.  Once we've "locked on" to the color we'll draw a center line on the camera image so as we can follow the line. The camera server will use the Robotpy [Network Tables](https://robotpy.readthedocs.io/en/stable/guide/nt.html#networktables-guide) to send data to the [Simulator](https://docs.wpilib.org/en/latest/docs/software/wpilib-tools/robot-simulation/index.html) and [Shuffleboard](https://docs.wpilib.org/en/latest/docs/software/dashboards/shuffleboard/index.html). We'll also send data to the Network Tables on where the center of the line is. 

## Create your Vision Program
For this lesson we'll use the [ImageProcessing](https://github.com/mjwhite8119/romi-examples/tree/main/ImageProcessing) project.  Clone this project to VSCode.  The **ImageProcessing** project uses the WPI example project **RomiReference** to run and view the camera data in the Simulator and Shuffleboard.  There are no changes made to the **RomiReference** code.

The python code for running the camera has been included in this project so as we have both of the software components in one place.  It makes use of the [Camera Server](https://docs.wpilib.org/en/stable/docs/software/vision-processing/introduction/cameraserver-class.html) class from the WPI Library. You'll upload the camera program to the Raspberry Pi on the Romi in a later step.  The following sections explain how to process images.

## Camera Program General Structure
Before we start programming lets look at the general structure that our camera program will take on.  The main idea is to get a frame from the camera, process the frame to extract objects from the scene that we're interested in, and put data regarding those objects into the Network Tables.  Our program running on the laptop will find useful things to do with that data.

The camera program can also send the data frames over to Shuffleboard in the form of a video stream. Before sending the frames the camera program can overlay them with useful visual information such as a center line of a target object.

![Camera Program Structure](../images/Romi/Romi.040.jpeg)

## Using GRIP to Process Images
In the above diagram you can see the camera sending frames to a piece of code called **GripPipeline**.  This code is generated from the FRC tool called [GRIP](https://docs.wpilib.org/en/latest/docs/software/vision-processing/grip/index.html).  A major part of this lesson will be to learn the GRIP tool and create a pipeline to process images coming from the camera.

1. On Mac start from Applications->GRIP
2. Turn on the Romi
3. Add Source -> IP Camera.  Put the URL of the camera stream.  wpilibpi.local:1181/stream.mjpg
4. Follow [FRC GRIP documentation](https://docs.wpilib.org/en/latest/docs/software/vision-processing/grip/index.html) to create the filter.
The last filter should be `Find Contours`.
5. Generate the code Tools->Generate Code.  
6. Select Python as the output language.
7. Use `GripPipeline` as the class name.
8. Put it into the `Vision` directory of your project.
9. Name the module `grip`.

<!-- If you're generating the java pipeline version make sure the the "Implement WPILIB VisionPipeline" box is checked.  This will place the following code into the generated GRIP file: -->

    import edu.wpi.first.vision.VisionPipeline;

The class definition will look like this:

    public class GripPipeline implements VisionPipeline {

## Upload Python Program
You won't be able to run the camera server code on your laptop since it's not currently supported.  You have to upload it to the Raspberry Pi to test it. In a terminal or Powershell:

1. `cd ~/Documents/romi-examples/ImageProcessing/Vision`
2. The python program has multiple files so you need to upload them all.  This is done with a zip file.  Run `python3 build.py` to build the zip file.
3. On the Romi WPILibPi.local webpage. Go to **Application**.
4. Put Raspberry Pi file system into Writable mode.
5. In the **Vision Application Configuration** section select "Uploaded Python File" from the dropdown menu.
6. In the **File Upload** section select the file `wpilib.tar.gz` file for upload.  Make sure that file **Extract** is selected. Click the **Upload** button.

![Upload Camera Program](../images/Romi/Romi.019.jpeg)

To confirm that the vision program is running you can view the output from the **Vision Status** tab.  Make sure that you enable console output.

![View Vision output](../images/Romi/Romi.021.jpeg)
<!-- ## Upload Java Program
1. cd ~/Documents/romi-examples/java-multiCameraServer
2. run `./gradlew build` to build the jar file.  Make sure that the build is successful.
3. On the Romi WPILibPi.local webpage, click on **Application** in the left panel.
4. Put into Writable mode
5. Select "Uploaded Java jar" in the dropdown.
6. Click on **Choose File** file and upload the file `build/libs/java-multiCameraServer-all.jar`. -->

## Test your Program
Run the your java program from VSCode by pressing the F5 key. In the **Simulator** you will see the Network Tables showing the `targetData` coming in from the python camera server program.  You can use this data to control the robot.
1. Connect the Joystick and drag it from **System Joysticks** window to the **Joysticks** window.
2. Put the robot in **Teleoperated** mode.
3. Press the joystick START button to run your custom PID line following routine.
3. Press the joystick SELECT button to run the WPI `PIDCommand` line following routine.

Shuffleboard uses the Network Tables to display the camera data so your java program must be running in order to see the live camera stream.

## References
- [OpenCV](https://opencv.org/)

- [Robotpy cscore](https://robotpy.readthedocs.io/projects/cscore/en/stable/api.html)

- Robotpy - [Network Tables](https://robotpy.readthedocs.io/en/stable/guide/nt.html#networktables-guide)

- FRC Documentation - [Network Tables](https://docs.wpilib.org/en/latest/docs/software/networktables/index.html)

- FRC Documentation - [Camera Server](https://docs.wpilib.org/en/stable/docs/software/vision-processing/introduction/cameraserver-class.html)

- FRC Documentation - [Vision with WPILibPi](https://docs.wpilib.org/en/stable/docs/software/vision-processing/wpilibpi/index.html#)

- FRC Documentation - [GRIP documentation](https://docs.wpilib.org/en/latest/docs/software/vision-processing/grip/index.html)

- Robotpy - [Camera & Vision](https://robotpy.readthedocs.io/en/stable/vision/index.html)

- [Robotpy examples - github](https://github.com/robotpy/robotpy-cscore/tree/main/examples)

- Code Example - [ImageProcessing](https://github.com/mjwhite8119/romi-examples/tree/main/ImageProcessing)

<h3><span style="float:left">
<a href="romiVision">Previous</a></span>
<span style="float:right">
<a href="romiLineFollow">Next</a></span></h3>