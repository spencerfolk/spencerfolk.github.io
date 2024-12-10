---
layout: page
title: Aero Parameter Identification
description: Real-time aerodynamic parameter estimation for UAV propellers for applications in adaptive control.
img: assets/img/projects/aerocoeff/crazyflie_frames.jpg
importance: 3
category: work
related_publications: false
---

In the Spring of 2022, I took ESE 650: Learning in Robotics, an elective as part of my robotics masters at the University of Pennsylvania. While the course is marketed as a survey of methods spanning perception, planning, and learning, we spent a lot of time delving into the underlying principles of state estimation and it was the first time the concept of a Kalman filter (and really state estimation as a whole) really clicked for me. It's also when I realized how important and powerful Bayesian filtering can be. 

The final group project for the course was open-ended. I teamed up with a (former) labmate Alexander and we developed an Extended Kalman Filter that could estimate the thrust and drag torque coefficients of the propellers a quadrotor UAV using *only* measurements from an onboard gyroscope. The novelty with this work was that we estimated each propeller's thrust and torque coefficient uniquely whereas the vast majority of other works at the time assumed each propeller was identical. In 99% of cases this is a perfectly fine assumption, but we were interested in scenarios where the aerodynamic coefficients would be different, like where a propeller is damaged mid-flight.

We used a nonlinear observability analysis to determine the minimum sensor suite necessary to observe these aerodynamic coefficients and we were able to verify this analysis through simulation studies. As a consequence of the nonlinear observability analysis, we also identified a condition where the observability of the system was broken: hover. This is quite unfortunate, because hovering is something that quadrotors do quite well! With this in mind, we also constructed a "calibration trajectory" that consisted of minor oscillations on the roll, pitch, and yaw axes, to ensure the system remained observable. 

We were able to tune the Kalman filter to converge within a fraction of a second, so as an added bonus we incorporated the estimated aerodynamic coefficients into a classical trajectory tracking controller for a quadrotor. With this construction, we essentially had an adaptive controller! In simulation, we were able to nearly recover the tracking performance of the baseline controller that had the correct aerodynamic coefficients to begin with. 

This work was never published because
1. it required measurements of the propeller speeds and since our target platform was a [Crazyflie](https://www.bitcraze.io/products/old-products/crazyflie-2-1/) with brushed motors these measurements were not available;
2. there is a harsh reality that small changes in these aerodynamic coefficients don't matter that much as far as tracking control is concerned because the lower level control is PID all the way down. 

The second point is a little nuanced and perhaps controversial. If you look at any popular open source flight stacks out there like PX4 or Betaflight, you won't see an explicit thrust or drag torque coefficient in the code (although to be clear you'll probably see a dimensionless thrust coefficient like in PX4). And yet, I can buy a new drone and get pretty good performance with the default parameters and gains because a properly-tuned PID controller will be able to handle the model discrepancies at the low level. 

Now, that being said, I still think for instances like propeller damage detection this could still be a valid approach and might be of interest to some PX4 developer one day. All said and done, this was an extremely valuable experience for me and helped me build a strong foundation in state estimation that would influence my later work on wind estimation. 

For all the details on the methodology and the results, feel free to check out our [report](/assets/pdf/ese650_project_report.pdf). 