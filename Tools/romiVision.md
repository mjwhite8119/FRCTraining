# <a name="code"></a>Vision Programming
Explain camera server and filtering ...

![Development Environment](../images/Romi/Romi.019.jpeg)

![Development Environment](../images/Romi/Romi.020.jpeg)

![Development Environment](../images/Romi/Romi.018.jpeg)

![Development Environment](../images/Romi/Romi.021.jpeg)

## GRIP
On Mac start from Applications->GRIP
Turn on the Romi
Add Source -> IP Camera.  Put the URL of the camera stream.  wpilibpi.local:1181/stream.mjpg
Follow FRC documentation to create the filter.
The last filter must should be Filter Contours.
Generate the code Tools->Generate Code.  Put it in your java main directory of your project.
Change the class definition.  It must implement VisionPipeline.
cd ~/Documents/romi-examples/java-multiCameraServer
./gradlew build
On the Romi WPILibPi.local webpage go to Application.
Put into Writable mode
Select "Uploaded Java jar" in the dropdown
Upload the file build/libs/java-multiCameraServer-all.jar
Run the Simulator


<h3><span style="float:left">
<a href="romiFirmware">Previous</a></span>