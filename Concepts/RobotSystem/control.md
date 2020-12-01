# Control Algorithms
Members of the programming team are primarily tasked with writing algorithms that control the robot.  This is the most heavily researched areas of robotics with a high demand of skilled programmers, especially those who understand robotic systems. To get an understanding of robot programming it's helpfull to try and categorize the algorithms into their functional areas.

A robot receives input from two sources; a user interface that sends it commands, and the sensors that perceive the environment around it.  Once the input is received the robot has to plan an action to perform and send control signals to it's actuators to carry out that action.  Input coming in from sensors must first be passed through the perception stack before it goes onto the planning algorithms. This is because sensor data is very large and coming in at a fast rate.  The robot has to make sense of that data before it can make use of it.

A critical piece of information that a robot would get from its sensors is <i>"Where am I?"</i> and <i>"What is my orientation?"</i>.  This process is call <i>**Localization**</i>. As the robot moves is needs to ensure that is remains on its intended path.  This process is called <i>**Tracking**</i>.  The perception algorithms need to filter the vast amounts of data coming in from the sensors in order to extract pertinent information.  

![Control Categories](../../images/FRCConcepts/FRCConcepts.012.jpeg)

<h3><span style="float:left">
<a href="intro">Previous</a></span>
