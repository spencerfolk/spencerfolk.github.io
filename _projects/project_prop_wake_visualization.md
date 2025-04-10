---
layout: page
title: Propeller Wake Visualization
description: Experimental attempts at visualizing the wakes of small UAV propellers.  
img: assets/img/projects/prop_wake_visualization/5inprop_diff.png
importance: 3
category: work
related_publications: false
---

**TL;DR:** I spent a long time trying to visualize the wake of a very small propeller. It was mildly successful! 

---

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/1uK6M31inFo143eEuVVUpDHUJt1OimMk3/preview" width="600" height="338" allow="autoplay"></iframe>
</div>
<div class="caption">
    Water vapor is sucked into a very small UAV propeller in an attempt to visualize the flow field. 
</div>

Very early on in my Ph.D., I worked on a project involving *extremely* small UAVs. The end goal was to build a swarm of tiny UAVs that could construct complex 3D formations in compact spaces--think [drone shows](https://www.youtube.com/watch?v=hNcMDoBmhGA) but scaled down to fit in your room. 

Unfortunately all (rotary-wing) UAVs emit a wake of relatively high speed and turbulent air as a byproduct of generating thrust. This wake can extend many propeller diameters below the UAV. This becomes a big problem when we start thinking about miniaturizing drone shows because
1. the UAVs have to operate much closer to each other relative to the size of each wake; and 
2. smaller UAVs are not particularly robust to any appreciable wind gusts.
In contrast, full size outdoor drone shows leverage the fact that the drones can be spaced *much* further apart and still make a coherent formation from the appropriate distance. Not to mention these larger drones can actually handle moderate wind disturbances without much of an issue. 

So, I decided to try and measure the wakes from our tiny propellers to see if we could fit an adequate model of the downwash for downstream planning tasks. This proved to be a much bigger challenge than I had initially thought. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/prop_wake_visualization/experimental_setup.jpg" class="rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/prop_wake_visualization/laser_setup.jpg" class="rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Our initial experimental setup for visualizing tiny propeller wakes. A high speed camera is focused on a propeller mounted on a thrust stand, and a laser with a diffractor shines a sheet of light centered on the propeller. 
</div>

I teamed up with two former Ph.D. students from [Paulo Arratia's fluid dynamics group](https://arratia.seas.upenn.edu/), Ran and Bryan, to hack together a basic particle image velocimetry (PIV) setup that included a laser, high speed camera, and an off-the-shelf humidifier for flow seeding. 

<div class="row justify-content-sm-center">
  <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/prop_wake_visualization/laser_setup_closeup.jpg" class="rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    A closeup of the (~50mm diameter) propeller glowing from the green light of the laser. Eventually we spray painted the propeller matte black to avoid laser reflections interfering with the high speed camera. 
</div>

From this setup we were able to obtain this slow motion video of water vapor particles in the wake of the propeller.  

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/1RiHctGggiD_5oWgiyQ_S_KS7jQT-UfrN/preview" width="512" height="992" allow="autoplay"></iframe>
</div>
<div class="caption">
    Wake visualization for a 50mm diameter propeller operating at 3,000 rpm. 
</div>

It was pretty cool to see this visualization for the first time! Most of the vapor collects near the hub where low speed vortices shed off at the root connection. It also gives a good impression of how turbulent the wake from these small propellers are. You'll also notice a flashing that occurs on the left side of the screen. This is caused by the oncoming propeller blade crossing the laser plane and reflecting light back towards the camera. We later tried to fix this by spray painting the propeller matte black, and it sort of helped!

Here is a wake visualization for the same propeller operating at 15,000 rpm. 

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/1t2DeSabOmM5LhxocSsrUNCT70j7LuzOQ/preview" width="512" height="992" allow="autoplay"></iframe>
</div>
<div class="caption">
    Wake visualization for a 50mm diameter propeller operating at 15,000 rpm. 
</div>

While the visualization certainly looks cool, we weren't really able to capture much velocimetry data from this. At higher speeds, the water vapor was too diffuse and our laser was too weak to capture the individual vapor particles necessary for PIV. Nevetheless, we *did* manage to get velocimetry data at 5,000 rpm and 7,500 rpm. 

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/175QT1pFfNhsqK0TjGFW995RQXltxVyqC/preview" width="480" height="864" frameborder="1" allow="autoplay"></iframe>
</div>
<div class="caption">
    Particle image velocimetry data extracted from a 50mm diameter propeller operating at 7,500 rpm. 
</div>

The animated velocimetry data further demonstrates how turbulent the wake flow field is. It seems that on average the wakes were between 1 and 2 m/s on average. Keep in mind though that typically these propellers operate between 15-20,000 rpm. 

<div class="row justify-content-sm-center">
  <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/prop_wake_visualization/5000rpm_contour.png" class="rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Time-averaged velocity contours extracted from particle image velocimetry at 5,000 rpm.
</div>
<div class="row justify-content-sm-center">
  <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/prop_wake_visualization/7500rpm_contour.png" class="rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Time-averaged velocity contours extracted from particle image velocimetry at 7,500 rpm.
</div>


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/prop_wake_visualization/Axial_velocity.png" class="rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/prop_wake_visualization/Axial_velocity_Radial.png" class="rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Time-averaged velocity data along the axial and radial axes of a 50mm propeller at different operating speeds. 
</div>

We knew from flight testing that the propellers were spinning at upwards of 20,000 rpm in hover, but due to hardware limitations we couldn't visualize the wakes at that speed, much less extract any useful velocimetry data. So ultimately, we decided to pivot. Nevertheless, I am extremely satisfied with the visualizations we were able to come up with, especially given the budget and resources available to us at the time!

Of course, huge credit goes to Ran and Bryan for helping design the experimental setup and run the velocimetry calculations on the footage we captured. 