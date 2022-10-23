---
layout: post
title:  "pick, place, sort, press, repeat."
subtitle: "A robotic cell prototype to assemble arrays of dry-erase markers and caps."
author: Kojo
categories: [ ROS, Robotic Manipulation, Computer Vision, Manufacturing ]
image: assets/images/posts/pickNplace.jpg
show_image_in_body: false
featured: true

github_url: https://github.com/kjwelbeck3/final-project-group-4-inc-1
class_link: https://www.mccormick.northwestern.edu/mechanical/academics/courses/descriptions/495-embedded-systems-in-robotics.html
class_name: Embedded Systems in Robotics
project_period: 11/10/21 - 12/6/21
---
<figure>
<iframe class="youtube-insert"
    src="https://www.youtube.com/embed/m37ZtrH2SsE"
    frameborder="0"
    allow="autoplay; encrypted-media"
    allowfullscreen
>
</iframe>
<figcaption>Full run of the 7-DOF Franka Panda robot arm, assembling markers and caps and sorting into gradients of hues.</figcaption>
</figure>

The inspiration was the wide application of robots in the manufacturing space.

The goal was to prototype an assembly cell that would 
1. take singly-arrayed dry-erase markers and singly-arrayed marker caps, 
2. match colors between the caps and markers, 
3. sort them into a color gradient, and 
4. snap-fit the caps onto respective markers.

The result was a ROS package built on top of MoveIt!, the SMACH state machine library, OpenCV and some Franka-provided ROS packages. The project comes complete with some custom Python packages to facilitate manipulation, perception and state-transition tasks respectively, and culminated in a demonstration showcasing the reliable assembly of caps and markers.


### The Setup

We built up an arrangement of 3 trays, one for each of (1) uncapped markers, (2) caps and (3) assembled caps and markers; and mounted an Intel Realsense camera to the robot wrist just above the end effector.


### My Responsibilities

My primary role was building out the sequence of robot manipulations. This was a layering process of wrapping MoveIt! functions and franka actions into atomic services; composing atomic service calls into higher level functions for constrained movements and for gripping and releasing caps and markers; and then, finally, exposing a couple pick-and-place services for use in the overarching state machine. At each level of abstraction, each service would return expressive messages for debugging purposes and for error-checking along the pick-and-place sequence.

The iterative process, to ensure reliability across the full scope of the prototype, included continually fine-tuning the pick-up and place-down orientation of the end-effector for better alignment with the parts on the trays. Similarly, I repeatedly re-measured to correctly encode tray locations in the robot’s reference frame, and reworked some constraints and speeds of the various motion profiles. Misalignment issues were relayed back into the tray re-design. And the robot’s allowable force thresholds were dialed in to accommodate the snap-fitting press.

I implemented a series of unit tests on the custom python packages: on the vision package, to verify the part and color detection algorithm on sample images; on the manipulation package, to check calculated absolute positions for tray locations; and on the state machine package to ensure correct matching between caps and markers and correct sorting on the assembled parts tray. The plan was to sort in ascending order of hues.


### Opportunities for Further Development

Beyond a prototype, there are a few obvious areas for further development.

Particularly, I would expand the vision system to autonomously characterize the trays’ configurations in the robot’s frame of reference. This would likely involve placing AprilTags on the trays for calculating the necessary transformations. The added flexibility, instead of hard-coding each tray’s location, would accommodate different infeed and outfeed systems – crates on conveyors, perhaps.

Another area to develop on would be using the franka_control ROS package to implement force control on the snap-fit press. As it stands, we only monitor the maximum forces experienced during the press, and report it as a validation/verification metric.
