---
layout: page
title: Real-Time LiDAR Simulation
description: Enabling mixed reality sensing on small UAVs by simulating LiDAR sensors in ROS.
img: assets/img/projects/lidarsim/lidar_snapshot.png
importance: 2
category: work
related_publications: false
---

**TL;DR:** We developed a ROS package to simulate navigational LiDAR sensors in real time using motion capture. 

---

As part of my Ph.D. thesis, I've been running experiments on a *very* small quadrotor UAV. It's so small that it can easily fit in the palm of your hand. The payload capacity is 20g or so and that's on a good day. 

The algorithms I've developed thus far rely on data from navigational LiDARs in order to work. These expensive sensors use laser scans to detect surrounding geometry and typically weigh about 500g, which is over 10x the weight of my UAV... 

This problem motivated me to figure out a way to simulate LiDAR sensors in real time on any arbitrary robot no matter the size. The idea was pretty simple: if I could track the poses of the robot and any objects of interest in real time, then I should have all the information necessary to produce fake point cloud data, right? 

This turned into an incredible collaboration with a fellow researcher at the lab, Kashish Garg, where we rapidly developed a ROS package for LiDAR simulation. The idea is simple: our ROS node listens to data from external motion capture (such as Optitrack) to determine where objects are relative to the robot. Objects are then decomposed into a triangle mesh, and the simulator performs an optimized Moller-Trumbore raycasting algorithm to find intersections between the fake laser rays and triangles in the scene. 

The main advantages of our LiDAR simulator over other similar tools are: 
1. Our simulator runs in the loop using real time data collected from motion capture which means you can easily track dynamic obstacles. 
2. We use the full 6 DoF information about the robot and objects to produce a 3D point cloud. 
3. The sensor intrinsics (sensor noise, field of view, resolution, min/max range, etc.) are all easily configurable and can even be reconfigured in real time. 
4. It is basically plug-and-play with existing ROS codebases as our method runs in the background and provides data in the [`sensor_msgs/PointCloud2`](http://docs.ros.org/en/noetic/api/sensor_msgs/html/msg/PointCloud2.html) format. 

Check out the video below to see our LiDAR simulator in action!

<div class="row justify-content-sm-center">
    <iframe src="https://drive.google.com/file/d/1jp71Sjoh8empzK6erD_5WNbeADNfdYKk/preview" width="960" height="540" allow="autoplay"></iframe>
</div>
<div class="caption">
    Our LiDAR simulator visualized in RViz with a real world perspective in the bottom right. The resolution, field of view, and refresh rates are based on an Ouster OS1. The simulator is running on a Beelink SER5 Pro Mini PC. 
</div>

We have plenty of planned improvements. Here's a small teaser: 
1. **Further performance gains**: Our simulator is already quite fast, but there are some ways we're thinking about making it even faster with some clever low-level optimizations. We're also looking into GPU acceleration. 
2. **Augmented reality worlds**: Perhaps the feature I'm most excited about, we're looking at ways to easily import virtual worlds through engines like Unreal or Unity to transform your motion capture space into whatever you can imagine it to be. 

I'm quite confident that the LiDAR simulator would be an incredibly helpful tool in classrooms teaching graduate level topics in perception, simultaneous localization and mapping (SLAM), and more. I'm looking forward to seeing ways people can use this tool for instruction. 

**Our plan is to release this package publicly very soon, so stay tuned for updates on this page!**