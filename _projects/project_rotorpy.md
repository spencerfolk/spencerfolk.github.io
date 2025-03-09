---
layout: page
title: Python UAV Simulator
description: A fast and accessible multirotor UAV simulator with lumped parameter aerodynamics developed for education and research. 
img: assets/img/projects/rotorpy/quadrotor_model.jpg
importance: 1
category: work
related_publications: false
---

**TL;DR:** I developed and now maintain a UAV simulator that can be used for research or as a good entry point into learning about estimation, planning, and control for UAVs. Check it out [here](https://github.com/spencerfolk/rotorpy)!

---

<p align="center">
  <img src="https://raw.githubusercontent.com/spencerfolk/rotorpy/main/media/ppo_hover_1000k.gif" width="32%"/>
  <img src="https://raw.githubusercontent.com/spencerfolk/rotorpy/main/media/gusty.gif" width="32%"/>
  <img src="https://raw.githubusercontent.com/spencerfolk/rotorpy/main/media/minsnap.gif" width="32%"/>
</p>

During my Ph.D. I developed RotorPy, a UAV simulator written in Python and born out of a desire for a fast, modular, easy-to-use simulation framework that I could use for my research. When I surveyed existing UAV simulators for this purpose, I found that their aerodynamic models were either lacking or nonexistent. I also struggled with developing with them--simple modifications like implementing a new sensor or modifying the dynamics models seemed overly complicated either because of poor architecture design or (in the majority of cases) lacking documentation. 

In retrospect I think a lot of my confusion came from the limited background in `C++` I had at the time--a consequence I attribute to my upbringing in mechanical engineering. Nevertheless, I thought it would be a worthwhile exercise to develop my own UAV simulator in Python, a language I and most other engineers have a strong background in. I felt this decision would make my simulator more interpetable and accessible to more inexperienced engineers, especially those coming from a non-CS background. 

It helped that I already had a really good example of a Python-based UAV simulator via an advanced robotics course I took at Penn. The simulator (simply named `flightsim`) was written by Jimmy Paulos for the sole purpose of course instruction. RotorPy uses the same integration scheme and underlying architecture for simulation, but the dynamics model was improved, a few features were added, and everything was restructured and modularized. 

Because my main goal was to use this simulator for research, I was seeking the following properties: 
1. **Speed**: The simulator needed to be fast enough to generate a reasonably large dataset for deep/reinforcement learning applications, with a Real-Time-Factor of no less than 1. 
2. **Easy to Install/Interpret/Use/Modify**: I did not want complex dependencies (outside of Python's `pip`) and I wanted to have control over every aspect of the simulator with ease. The concept of "rapid prototyping" comes to mind here. 
3. **Modular**: I wanted to make sure I could easily expand the simulator with new sensors, dynamics models, controllers, etc. as my research topics evolved over time. 
4. **Inertial Sensing**: For model-based wind estimation, proper accelerometer and gyroscope models were necessary. 
5. **Basic Visualizations**: It was important to me that I could make basic yet clean plots and animations of my simulations not only for presentations but also for rapid "sanity checking" when developing, say, control algorithms. 
6. **Wind Models**: Because my research revolves around wind and its effects on UAVs, it was really important that wind was treated as a fundamental module that was tightly integrated into RotorPy. The wind module needed to model winds in both space and time.
7. **Lumped Parameter Aerodynamics Models**: The UAV dynamics needed to incorporate aerodynamic models, and I favored explicit lumped parameter models of thrust, drag, etc. over implicit schemes (e.g. panel methods) because they are faster, easier to modify, and more interpretable. 

The first requirement arguably should have disqualified Python, but it was a price I was willing to pay for code that was easier to read and develop. Because of some code optimization and integration choices, RotorPy actually runs quite fast on laptops and desktop computers. 

RotorPy became public on [Github](https://github.com/spencerfolk/rotorpy) on March 15th, 2023. Soon after I presented the simulator to the workshop ["The Role of Robotics Simulators for Unmanned Aerial Vehicles"](https://imrclab.github.io/workshop-uav-sims-icra2023/) at ICRA 2023. 

Since then RotorPy has been improved and expanded in many ways. I added a first order lag to the motor speeds to simulate motor dynamics. I also added new sensors including a 2D range sensor to simulate LiDAR. Most recently, I incorporated the multirotor dynamics model into a custom [Gymnasium](https://github.com/Farama-Foundation/Gymnasium) environment for reinforcement learning, which uniquely supports different control abstractions from high level velocity commands all the way down to direct motor control. 

RotorPy continues to be a fantastic resource for learning about sensing, planning, and control for flying robots. It includes implementations of classical algorithms like A*, a nonlinear geometric tracking controller, and minimum snap trajectory generation for quadrotors. 

You can install RotorPy in Python using `pip install rotorpy`, or you can clone it [here](https://github.com/spencerfolk/rotorpy) and read the documentation for more information. 