# Kalman Filters
Kalman Filters fuse measurements from one or more sensors with a State Space model of the system to optimally estimate a system’s state.  They have methods of extending them to accommodate non-linear systems, something that is not possible with classical control methods such as PID.

They are expressed in the form of differential equations.  

![Kalman Filter](../../images/FRCOptimalEstimation/FRCOptimalEstimation.001.jpeg)


![Project State Ahead](../../images/FRCOptimalEstimation/FRCOptimalEstimation.002.jpeg)

![Project Error Ahead](../../images/FRCOptimalEstimation/FRCOptimalEstimation.003.jpeg)

![Calculate Kalman Gain](../../images/FRCOptimalEstimation/FRCOptimalEstimation.004.jpeg)

![Update State with Measurement](../../images/FRCOptimalEstimation/FRCOptimalEstimation.005.jpeg)

![Update the Error](../../images/FRCOptimalEstimation/FRCOptimalEstimation.006.jpeg)

## References
- FRC Documentation [State Observers and Kalman Filters](https://docs.wpilib.org/en/stable/docs/software/advanced-controls/state-space/state-space-observers.html)

- Tyler Veness [Controls Engineering in the
FIRST Robotics Competition](https://file.tavsys.net/control/controls-engineering-in-frc.pdf) Chapter 10.

- Alonzo Kelly [Mobile Robotics](https://www.cambridge.org/core/books/mobile-robotics/5BF238489F9BC337C0736432C87B3091) Chapter 5.3

- Roger Labbe [Kalman and Bayesian Filters in Python](https://github.com/rlabbe/Kalman-and-Bayesian-Filters-in-Python)

<h3><span style="float:left">
<a href="stateEstimation">Previous</a></span>
<span style="float:right">
<a href="optimalEstimationIndex">Back</a></span></h3>