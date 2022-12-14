---
layout: post
title:  "LanceBot: a platform robot in infancy"
subtitle: "A two wheeled robot balancing by PID control."
author: Kojo
categories: [ Mechatronics, Dynamic Systems and Control ]
image: assets/images/posts/balancebot.jpg
show_image_in_body: false
featured: true

github_url: https://github.com/kjwelbeck3/lanceBot_v1
class_link: https://www.mccormick.northwestern.edu/robotics/curriculum/#independent-project
class_name: MSR Independent Winter Project
project_period: 01/04/21 - 03/18/21
---
<figure>
<iframe
    class = "youtube-insert"
    src="https://www.youtube.com/embed/1vmVGw6rdEQ"
    frameborder="0"
    allow="autoplay; encrypted-media"
    allowfullscreen
>
</iframe>
<figcaption>LanceBot balancing, with minor(tentative!) disturbances</figcaption>
</figure>

Like many dynamics and control theory enthusiasts before me, I sought out to design and build a two-wheeled balancing robot and to build intuition and experience about stabilizing unstable systems.

This robot, hereby dubbed Sir LanceBot, was conceived as a platform robot for developing and testing various control schemes for both balancing and navigation.

In this post and in the accompanying github repository, I chronicle the implementation of a Proportional-Integral-Derivative (PID) control scheme to keep LanceBot upright, as a first milestone toward building bots like Ascento.



### PID Control

The general control architecture features a constant tracking of the robot’s pitch angle by an inertial measurement unit (IMU) and a responsive control command sent by the on-board microcontroller to modulate the voltages supplied to the motors, all towards the goal of achieving a reference configuration/state.
There is considerable theoretical deliberation in characterizing the stability, controllability, observability of a non-linear dynamic system and towards developing an optimal controller - a scheme among many worth exploring and implementing in the near future.

The PID-based controller, however, lends itself to robust control based on the robot’s error from a reference state. In this case, my reference state is that the robot stays upright with zero pitch. The controller is captured by the following formulation:

`Control PWM Command = P * pitch error + I * total pitch error + D * rate of change of the pitch`


### Progress Snapshots

This milestone bookends a series of redesigns and rebuilds, a shift from a microprocessor implementation to a microcontroller build, where I have tighter control and more flexibility on control the control signal, timing and peripheral interfacing.

<figure>
<iframe class="youtube-insert"
    src="https://www.youtube.com/embed/tM6XfRu1-X0"
    frameborder="0"
    allow="autoplay; encrypted-media"
    allowfullscreen
>
</iframe>
<figcaption>Starts of balancing gingerly, then runs away.</figcaption>
</figure>

<figure>
<iframe class="youtube-insert"
    src="https://www.youtube.com/embed/UrxwE6Zeq8E"
    frameborder="0"
    allow="autoplay; encrypted-media"
    allowfullscreen
>
</iframe>
<figcaption>Calibrating and then loosely balancing.</figcaption>
</figure>


### Next Steps

My next steps: 
 - to switch from a bench power supply to battery power; 
 - to continue tuning gains; 
 - to incorporate the motor encoders into determining the robot’s wheel states, and 
 - to implement some driving control possibly based on the wheel states and with a user-interface.
