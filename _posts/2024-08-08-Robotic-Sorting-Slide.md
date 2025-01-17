---
layout: single
title:  "Robotic Sorting Slide"
date:   2024-08-08 12:00:00 +0000
categories: own-build
---

Thee final stage of every LEGO® Sorting Machine is storing the classified bricks in the corresponding bins. This article summarizes the current work-in-progress to completely rebuild the storage stage of my sorting machine. The goal of this rebuild is to maximize the machine’s operation time by allowing it to run unattended for longer periods without human support. This includes simplifying and accelerating human maintenance, such as refilling unsorted parts and emptying storage containers for sorted LEGO® bricks.

[attachment_0](attachment)

*Robotic slide guiding the classified bricks — sped-up video of the final result.*


There are many possible options for designing the sorted storage: Conveyor belts, horizontal/vertical gates, pneumatic/mechanical approaches, etc. To reduce complexity, space and hardware requirements, I decided to follow the simple rotational slide design principle.

Bricks are falling on a slide which sits on top of a rotating platform. Based on the brick classification results, the platform rotates in order to direct each brick into its target bin. This design is very hardware efficient since it merely uses two servos to serve a large number of densely packed storage bins. As a bonus, timing is not particularly critical with this system.

## First Designs

My very first design iteration of the slide was built mostly from Lego (unfortunately no pictures were taken at that time yet). The construction was quite large, thus resulting in a pretty high slide mass. The high mass far off the slide’s center of rotation created a large moment of inertia. The servo was under high load and during acceleration and deceleration there were oscillations.

Thus I learned to keep the mass low which led to the second design iteration built from a mixture of LEGO bricks and cardboard. It immediately performed much better. The oscillations were greatly reduced. The servo was able to position the slide quickly and accurately above the bins. During this time I was using hardware storage containers as storage bins (after all this whole machine is being built in a woodshop).

[attachment_1](attachment)
[attachment_1](attachment)

*First variants of the cardboard slide*

On the electronics side, the slide is actuated by 360° Geekservos. Out of the box they are LEGO compatible so no adapters had to be made. The servos are controlled by an Arduino Nano. The code of the slide controller (and the full machine) is available on github. It uses the excellent ServoEasing library which enables smooth acceleration curves. The Arduino receives its motion commands via USB/serial by the serial service of the sorting machine stack (sorting machine architecture).

## Going 2D

Right from the beginning I wanted the slide to operate in 2 dimensions. Thus not just rotate but also pitch. This would at least double the amount of reachable storage bins. To realize this, both the slide and the storage containers had to be modified.

On the slide, the change was simple. I mounted a second servo onboard the rotating platform. Via a gear reduction the servo drives two arms which pitch the slide up and down. The motion is quick and precise and the mechanics integrate nicely into the existing design.

[attachment_3](attachment)

*Slide pitch mechanics*

The work on the storage bins was more extensive. The primary goal was to pack as many bins as possible around the slide in an almost full circle. To achieve this, the bins needed to be as narrow as possible while still allowing parts to fall in reliably. The initial prototypes of these 2-level chutes were designed in FreeCAD and built from cardboard. This approach enabled rapid iterations on the dimensions, yielding first promising results.

[attachment_4](attachment)

*Cardboard prototype of the 2-level chutes (see video)*

After the design was validated in cardboard, the work took a little bit of a detour since I started getting into 3D printing. This allowed the design of the chutes to be much more refined. It still features two channels which now separate at the bottom and change shape into round tubes. They are round because it is intended to hang round cloth tubes (they look almost like socks) beneath them in order to store sorted parts. The chute design also features mounting holders to mount them inside a cutout of the tabletop board. The CAD design files are available here.

[attachment_5](attachment)
[attachment_5](attachment)
[attachment_5](attachment)
[attachment_5](attachment)

*Onshape drawing, printing and arrangement of the redesigned chutes*

For the mounting of the chutes the tabletop board had to be modified heavily. The board is made from OSB wood. It features a C-shape cutout into which the chutes get mounted from below. The center wood circle is supported from one side only, thus utilizing approximately 300° of the full circle.

[attachment_9](attachment)
[attachment_9](attachment)
[attachment_9](attachment)
[attachment_9](attachment)

*Mounting of the 2-level chutes inside the tabletop board — cloth storage “socks” added on the bottom right.*

After the chutes were mounted, the cloth “socks” could be added as well. They just fit over the round end of the chutes. A rubber band holds them in place while locking on to the rim.

[attachment_13](attachment)

*View of the complete machine as of today.*

This is the final view of the completed new design. I am super happy with it because it reduces manual handling efforts significantly and thus causes the machine to be running more often. The 22 bins fit our 20 bin sorting concept perfectly (+1 bin for parts with low confidence classification). I'll make sure to create a video soon, until then you can reach me via DM as BrickSortingMachine on Instagram. If you are interested in LEGO® sorting machines in general you might also want to join the fabulous Discord server of the Great Brick Lab where frequent exchange is happening.
