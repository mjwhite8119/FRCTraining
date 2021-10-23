# State Space Control
**State Space** control is an alternative to PID control.  State Space control is based on the idea that if you know the physics of your system and can predict how it’ll react to a given input then you can tune the system in a way that’s similar to tuning PID controllers.  State Space control is more flexible than PID control.  Chapter 6 of the book [Controls Engineering in the FIRST Robotics Competition](https://file.tavsys.net/control/controls-engineering-in-frc.pdf) gives a detailed explaination of the topic. Once you understand the basics of State Space  control the you can refer to the FRC documentation [State Space Controllers](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/state-space/state-space-intro.html) that shows you how to set these up using the WPI class libraries.  The following sections will step you through each of these classes.



State Space Control tries to control the system by developing an accurate model of the system that we are trying to control. 
<!-- 
Alonzo Kelly [Mobile Robotics](https://www.cambridge.org/core/books/mobile-robotics/5BF238489F9BC337C0736432C87B3091) Chapter 7.2 -->

## Observabilty and Controlabilty

### Linear Systems
In [Controls Engineering](https://file.tavsys.net/control/controls-engineering-in-frc.pdf) the system that you're modelling is called a *Plant*.  




## References
- FRC Documentation [State Space Controllers](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/state-space/state-space-intro.html)

- Tyler Veness [Controls Engineering in the
FIRST Robotics Competition](https://file.tavsys.net/control/controls-engineering-in-frc.pdf)

- Christopher Lum [Introduction to Linear Quadratic Regulator (LQR) Control](https://www.youtube.com/watch?v=wEevt2a4SKI&t=7s)

- MATLAB [State Space Control](https://www.youtube.com/playlist?list=PLn8PRpmsu08podBgFw66-IavqU2SqPg_w)

- MATLAB [Robust Control](https://www.youtube.com/playlist?list=PLn8PRpmsu08qFLMfgTEzR8DxOPE7fBiin)

- FRC Documentation - [State-Space and Model Based Control with WPILib](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/state-space/index.html)

- Tyler Veness [Controls Engineering in the
FIRST Robotics Competition](https://file.tavsys.net/control/controls-engineering-in-frc.pdf) Chapter 6

- Alonzo Kelly [Mobile Robotics](https://www.cambridge.org/core/books/mobile-robotics/5BF238489F9BC337C0736432C87B3091) Chapter 7.1


<h3><span style="float:left">
<a href="classicalControl">Previous</a></span>
<span style="float:right">
<a href="LQR">Next</a></span></h3>