---
layout: page
title: Tailsitter Transition Maneuvers
description: Designing constant altitude longitudinal transition maneuvers using equilibrium analyses. 
img: assets/img/projects/tailsitter/ref_frame_fbd.png
importance: 3
category: work
related_publications: false
---

**TL;DR:** For my Ph.D. Qualifying Exam, I developed a novel method for generating constant-altitude transition maneuvers for tailsitter VTOLs.

---

In my second semester of my Ph.D., I had to go through my Qualifying Exams. In [my department](https://www.me.upenn.edu/), the Qualifying Exam was quite unique in that it was a semester-long independent study that culminated in a written report and an hour long oral presentation plus questions. A few weeks before the semester began, we had to propose an appropriately-scoped research topic that we would explore throughout the semester, and we were mostly evaluated on how well we could come up with a research topic, conduct the research, and present the results in what turned out to be a "mini-defense" of sorts. 

For my Qualifying Exam, I proposed a research project investigating transition maneuvers for tailsitter UAVs, which are a specific type of hybrid UAV that can both hover in place like a helicopter and cruise efficiently like a conventional airplane with the use of lifting surfaces. Unlike other hybrid UAVs (like a tilt-rotor or tilt-wing), the actuators and primary lifting surfaces on tailsitter UAVs are fixed in place, and switching between hovering and forward flight requires the entire aircraft to pitch forward almost 90 degrees. This makes the tailsitter UAV much less *mechanically* complex, but it makes the transition between hover and forward flight much more complicated primarily because lifting surfaces are at high risk of stalling. 

There are a handbag of excellent solutions for generating dynamically feasible transition maneuvers for tailsitters ranging from heuristics to principled trajectory optimizations, but the unique perspective I took with my project was to constrain my transition maneuvers to a *constant altitude* which was motivated by the concern for constrained airspaces over suburban and urban regions. 

My approach was to analyze the passive stability of the aircraft as a function of angle of attack and airspeed. The stability analysis provided a mapping from a desired angle of attack to a (unique) airspeed for stability, so I could prescribe a sequence of desired angles of attack transitioning from hover (90 deg) to forward flight (somewhere near 5 deg) and my algorithm would output a trajectory in position, velocity, and acceleration which could then be tracked with a trajectory tracking controller adapted from quadrotor literature. Going from the desired angle of attack to a trajectory required solving a 2nd order nonlinear ODE which we can solve numerically in very little time. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/tailsitter/qbit_animated_prescribed_aoa_1x.gif" class="rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    A crude animation of a tailsitter UAV transitioning from hover to forward flight at constant altitude. 
</div>

This work remains unpublished because while it (sort of) works in simulation, it relies on too many assumptions to be practically implemented on a real platform. The trajectory is planned and executed open loop and while I suppose the trajectory tracking controller might be able to compensate for small perturbations I can't imagine it would actually work well in practice. Also, the method does not account for input constraints like thrust limits and the controller fails horrendously if these constraints are violated. If I (or you) were to revisit this topic today, I think a very different approach would be taken. 

Despite the shortcomings, it was an incredibly valuable experience for me and I learned a lot of useful knowledge and skills that I still use today. The simulation environment I developed for this project eventually helped me in the creation of [RotorPy](https://github.com/spencerfolk/rotorpy). And while I don't support the methodology, I think it is certainly a unique solution to the transition maneuver problem that I have yet to see published anywhere else. 

For a thorough treatment of this work, feel free to take a look at my [Qualifying Exam Report](/assets/pdf/meam_qualifying_report.pdf). 