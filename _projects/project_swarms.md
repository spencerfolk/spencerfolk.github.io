---
layout: page
title: Formation Flying Robots
description: A swarm of small UAVs flying in formation using motion capture. 
img: assets/img/projects/swarms/swarms_preview.png
importance: 2
category: work
related_publications: false
---


**TL;DR:** We developed and ran a cool demo of swarming UAVs for the 2024 APS John Scott Award ceremony. It was kind of like a miniature drone show!

---

In late fall of 2024, myself and a few of my labmates were tasked with putting together a demo of a coordinated swarm of UAVs for the [John Scott Award](http://thejohnscottaward.org/) administered by the American Philosophical Society. 

The goal was to showcase multiple UAVs flying unique formations, somewhat mimicking the increasingly popular drone shows displayed at large events, but this demo had to happen indoors and of course had to be safe for viewers! To accomplish this we actually set up a small motion capture space. You can see below what the demo space looked like. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/swarms/mocap_setup.jpg" class="rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Our mobile motion capture space set up at the John Scott Award ceremony. November 14th, 2024. Philadelphia, PA. Big props go to Fernando Cladera for coordinating all the logistics for this setup. 
</div>

The exciting part of this demo was using our creativity to come up with sequences of dynamic trajectories that were entertaining to watch. We played around with circles, lissajous paths, and more to create complex patterns moving in space. Moreover, we designed transition trajectories using minimum snap trajectory generation that would seamlessly reposition the UAVs from the end of one formation to the beginning of the next. 

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/1NBDKm7-J_7QgY_mRDESS0Uw8P_Cyh8BT/preview" width="960" height="540" allow="autoplay"></iframe>
</div>
<div class="caption">
    A train of quadrotor UAVs performing a figure eight formation. 
</div>

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/1o2m4WTqH2aynb6mLst_150lwLS-1-tNX/preview" width="960" height="540" allow="autoplay"></iframe>
</div>
<div class="caption">
    Four quadrotor UAVs forming a twisting circle that traces out a toroid in space. Yes, there was a crash at the end of this video!
</div>

The hard part of this demo was figuring out the coordination of these UAVs to ensure that they did not collide on takeoff or when transitioning between formations. We didn't have time to come up with or implement a sophisticated solution involving some multi-agent routing algorithm... instead we had to rely on a little bit of trial and error. 

To aid with that trial and error, the night before the event I wrote a script using [RotorPy](https://github.com/spencerfolk/rotorpy/tree/main) to check our trajectories offline rather than waste precious time and batteries. RotorPy simulated the closed loop tracking of all the agents' trajectories simultaneously and checked for any collisions. It would report where collisions happened in space and which two agents collided, so that it was clear which trajectories needed to be adjusted. 

I wrote an interface that would interpret our ROS launchfiles and set up RotorPy appropriately such that we could craft the trajectories in ROS and test them in simulation before running them on the robots. Since RotorPy was using the same tracking controller as our real UAVs, we could test for collisions even if the UAVs started far away from their initial waypoint (e.g. takeoff). 

You can see one of the set of formations that we flew running in RotorPy below: 

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/15vo491mqBGwe-H6PhMqTgvKC3KScnrLV/preview" width="960" height="540" allow="autoplay"></iframe>
</div>
<div class="caption">
    One of the formation sequences we came up with and tested in simulation for collisions before deploying. 
</div>

This was a very rewarding experience--mostly teaching me how to work under some serious time pressure, but also demonstrating to me the real logistical challenges drone shows face that you don't really understand until you have to implement it yourself. 