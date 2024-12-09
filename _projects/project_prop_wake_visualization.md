---
layout: page
title: Propeller Wake Visualization
description: Experimental attempts at visualizing the wakes of small UAV propellers.  
img: assets/img/projects/prop_wake_visualization/5inprop_diff.png
importance: 3
category: work
related_publications: true
---

<iframe style="display: block; margin: auto;" src="https://drive.google.com/file/d/1bVmLU7y2LIrQjiZZ-Qtv6k995YNnwOHZ/preview?autoplay=1&mute=1" width="640" height="360" frameborder="0" allow="autoplay"></iframe>

Very early on in my Ph.D., I worked on a project involving *extremely* small UAVs. The concept was to build a swarm of tiny UAVs that could construct complex 3D formations in compact spaces--think [drone shows](https://www.youtube.com/watch?v=hNcMDoBmhGA) but scaled down to fit in your room. 

Unfortunately all (rotary-wing) UAVs emit a wake of relatively high speed and turbulent air as a byproduct of generating thrust. This wake can extend many propeller diameters below the UAV. This becomes a big problem when we start thinking about miniaturizing drone shows because

1. the UAVs have to operate much closer to each other relative to the size of each wake; and 
2. smaller UAVs are not particularly robust to any appreciable wind gusts.

In contrast, full size outdoor drone shows enjoy the fact that the drones can be spaced *much* further apart and they can handle moderate wind disturbances. 

So, I decided to try and measure the wakes from our tiny propellers so we could fit an adequate model for downstream planning tasks. This proved to be a much bigger challenge than I had initially thought. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/prop_wake_visualization/experimental_setup.jpg" title="" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/prop_wake_visualization/laser_setup.jpg" title="" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Our initial experimental setup for visualizing tiny propeller wakes. A high speed camera is focused on a propeller mounted on a thrust stand, and a laser with a diffractor shines a sheet of light centered on the propeller. 
</div>

