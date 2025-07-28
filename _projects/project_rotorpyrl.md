---
layout: page
title: Crossing the Sim2Real Gap with RotorPy
description: Teaching a quadrotor to fly in minutes on a laptop. 
img: assets/img/projects/rotorpyrl/brushless_crazyflie.jpg
importance: 2
category: work
related_publications: false
---

**TL;DR:** We successfully trained a quadrotor tracking control policy via reinforcement learning in just minutes using [RotorPy](https://github.com/spencerfolk/rotorpy), and deployed it on a real quadrotor.

---

Recently my colleague [Hersh Sanghvi](https://hersh500.github.io/) has been using RotorPy to generate training data for his [research on meta learning](https://openreview.net/forum?id=xeFKtSXPMd). In support of this we've been working on rewriting RotorPy's backend in PyTorch so that it can be parallelized on GPUs. The results have been impressive--depending on the system specs we're seeing upwards of 100x speedup over a CPU-bound RotorPy!

We thought a really cool demo to illustrate the speed up would be to train an RL policy in RotorPy and then transfer it to the real world. After quite a bit of experimentation we managed to get a solid policy. Below is a video demonstration of the policy in action!

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/1oEUddiqP6_Far7B9ccilX0qUq7pL39yh/preview" width="1920" height="1080" allow="autoplay"></iframe>
</div>
<div class="caption">
    Hovering demonstrated by an RL policy trained in RotorPy. The policy is robust to a variety of disturbances. 
</div>

The policy receives an observation containing the position error, velocity error, the orientation, and body rates. The observation also includes a horizon of future position commands from the trajectory. Odometry is conveniently provided by an external motion capture system!

The output of the policy is a collective thrust and attitude command (i.e. "angle" mode), which is then tracked by lower level controllers running onboard the quadrotor. The policy itself runs on the base station computer. 

The policy was trained using PPO and our [custom Gymnasium environment](https://github.com/Hersh500/rotorpy/blob/rotorpy_rl/rotorpy/learning/quadrotor_environments.py#L635). In simulation, the agent was exposed to sinusoidal trajectories of varying amplitudes and frequencies. On Hersh's M1 MacBook Pro, it took a little over 3 minutes to train a policy over a couple million simulation steps. 

Below is another example of the policy, but this time tracking a figure eight pattern on the XY axis. 

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/17M130lk5eDwshL-CdBR0QBp8QsVpaP_k/preview" width="1920" height="1080" allow="autoplay"></iframe>
</div>
<div class="caption">
    Our RL policy tracking a figure eight pattern. We found including a horizon improved tracking performance and reduced oscillations especially for aggressive maneuvers.  
</div>

If you're an RL expert, you're probably thinking we didn't really do anything novel here. I completely agree! Nevertheless, we're quite proud of how fast we were able to train a policy using RotorPy, and super excited we were able to cross the infamous *sim2real gap*. 

Possible follow-ups we're thinking about: 
1. We'd love to figure out how to compile the policy and run it using the onboard processor. [It's been done before](https://arxiv.org/abs/2311.13081), and our policy is probably small enough to fit on the flash memory. 
2. Towards running everything on board, we want to try to train a policy that uses IMU measurements (accelerometer and gyroscope), perhaps even replacing the motion capture observations. There are a lot of practical reasons that I suspect would prevent this from working, but it would get our policies closer to the edge! Fortunately RotorPy has an [IMU model](https://github.com/spencerfolk/rotorpy/blob/main/rotorpy/sensors/imu.py) already!
3. Try training policies on lower control abstractions, such as body rates or even single motor thrust commands. 
3. Replicating and testing similar works such as [DATT](https://arxiv.org/abs/2310.09053).