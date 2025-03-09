---
layout: page
title: Online Aero Parameter Identification
description: Real-time aerodynamic parameter estimation for UAV propellers for applications in adaptive control.
img: assets/img/projects/aerocoeff/crazyflie_frames.jpg
importance: 3
category: work
related_publications: false
---

**TL;DR:** We synthesized an Extended Kalman Filter for identifying aerodynamic parameters (thrust/torque coefficients) for a quadrotor UAV in real time. 

---

In the Spring of 2022, I took ESE 650: Learning in Robotics, an elective as part of my robotics masters degree at the University of Pennsylvania. The course was marketed as a survey of methods spanning perception, planning, and control, but we ended up spending a large chunk of the semester digging deep into the principles of state estimation. While it certainly wasn't my first exposure to Kalman filtering, it was the first time that the concept really clicked with me.

For the final project of the course, I teamed up with a former labmate, Alexander, and we implemented an Extended Kalman Filter for estimating the thrust and drag torque coefficients of a quadrotor's propellers using *only* measurements from the onboard gyroscope. The novelty with this work was that each propeller's aerodynamic coefficients were estimated independently, whereas the vast majority of other works at the time assumed each propeller was identical. Let's be real, in 99% of cases this is a *perfectly fine assumption*, but our approach would theoretically be useful in situations like where an individual propeller is damaged mid-flight.

A lot of time was spent tuning the Kalman filter to converge within a fraction of a second (around 20-30 measurement updates). Once we got the filter to converge so fast, we had the idea to incorporate the estimated aerodynamic coefficients into a classical quadrotor trajectory tracking controller. In doing so, we essentially had a model-based adaptive controller! In simulation, we were able to nearly recover the tracking performance of a baseline "oracle" controller that had privileged knowledge of the correct aerodynamic coefficients from the start. 

We also wrote an automated nonlinear observability analysis to determine the minimum sensor suite (accelerometer, gyroscope, cameras, GPS, etc.) necessary to observe distinct propeller coefficients. The analysis also informed a condition where observability broke down: hover! This is pretty consequential because quadrotors are kind of designed to hover in place most of the time! If you look closely at the UAV state estimation literature, you'll find the hover degeneracy for a lot of other filters too. In my humble opinion, only the good papers are going to acknowledge this up front...

Anyways, eventually this project was abandoned after we tried to transition from simulation to hardware primarily because of two reasons:
1. by construction, the filter required measurements of the propeller speeds and since our target platform was a [Crazyflie](https://www.bitcraze.io/products/old-products/crazyflie-2-1/) with brushed motors, these measurements simply were not available; and
2. we learned the reality that small changes in these aerodynamic coefficients don't really matter that much as far as tracking control is concerned, because the lower level control is PID all the way down. 

The second point is a little nuanced and perhaps controversial. If you look at any popular open source flight stacks out there like PX4 or ArduPilot, you won't see an explicit thrust or drag torque coefficient in the code. The closest thing you might find is a "control effectiveness value" for each axis or at best a dimensionless thrust coefficient. And yet, I can go and buy a new drone, upload the default parameters, and still get pretty good tracking control performance right off the bat. Why is this? Because the controllers for all of these open source autopilots rely on high frequency, high gain, closed-loop PID feedback control. When we transitioned to hardware, we quickly realized that propeller coefficients would only come into play *at the lowest level* of the control stack, the rate loop, which already benefits from high frequency feedback from the onboard gyroscope. A set of properly tuned PID gains coupled with high bandwidth control can effectively crush most model uncertainties, including in the aerodynamic coefficients. 

Now, that being said, there has been plenty of excellent research in recent years demonstrating improved tracking control with more-or-less explicit aerodynamic parameter identification, but these papers tend to be focused on specific cases like operating in ground effect or the aforementioned propeller damage scenario. Ultimately I think these sort of methods will enhance, but not replace, traditional PID feedback control for small rotary-wing UAVs. For larger UAVs (like autonomous helicopters) with less control bandwidths, this might be a *very* different story... 

All said and done, this project helped me build a strong foundation in state estimation which would be a strong influence on my later work on wind estimation. In fact, I spent upwards of two years after this class focusing my research on state estimation!

For all the details on the methodology and our simulation results, feel free to check out our [report](/assets/pdf/ese650_project_report.pdf). 