---
layout: post
title: "System Architecture of the LEGO Sorting Machine"
description: Inspired by a YouTube comment written by BrickImperial, let’s dive into the architecture of the sorting machine.
date: 2023-12-16 12:00:00 +0100
author: bsm
image: '/assets/images/system-arch/01_raspi.webp'
image_caption: 'Raspberry Pi controlling the machine mechanics'
tags: [build]
featured: false
---
## Physical Setup
The LEGO sorting machine is driven by two main compute units. A Raspberry Pi 3 as interface to the [L293D](https://www.ti.com/product/L293D) motor drivers and a [Intel® NUC Kit D34010WYK](https://ark.intel.com/content/www/us/en/ark/products/76978/intel-nuc-kit-d34010wyk.html) handling all image processing, classification and HMI. Images are acquired by a [ELP 5MP 120° Wide FOV USB camera module](https://www.amazon.de/-/en/Cameras-Operating-Definition-2592X1944-USB500W02M-L21/dp/B07GBNYX8H).

## Logical Architecture
All system units are implemented as independent services (python processes) communicating via TCP sockets using a very simple text based message passing protocol. The Raspberry Pi is acting as a relay server routing certain message types to the intended receivers.

![Drawing of the Logical Architecture]({{site.baseurl}}/assets/images/system-arch/02_logical_arch.webp){:loading="lazy"}
*Logical Architecture*

## Raspberry Pi / Machine Controller
The machine controller is driven by a state machine, which handles the operation of the two conveyor belts and the two v-channel vibration feeders. While the scanner belt is running continuously, both the storage belt and the vibration feeders switch activation states based on a fixed timing sequence. Whenever an object is detected on the scanner belt, the vibration feeders are stopped.

![Photo of Brick Scanner with Camera Module and Mirror]({{site.baseurl}}/assets/images/system-arch/03_scanner.webp){:loading="lazy"}
*Brick Scanner with Camera Module and Mirror*

## NUC / Vision Service
The vision service handles all image processing and part detection. Images are captured via USB and the [OpenCV background subtraction](https://docs.opencv.org/4.x/d1/dc5/tutorial_background_subtraction.html) is detecting bricks against the white background of the scanner belt. Whenever a part is detected on the scanner a belt busy message is sent to stop the vibration feeders. The moment the part reaches the trigger area, a image is stored and a request is sent to the classification service.

![Screenshot of Sorting Machine HMI with a car part detected and classified]({{site.baseurl}}/assets/images/system-arch/04_hmi.webp){:loading="lazy"}
*Sorting Machine HMI with a car part detected and classified*

## NUC / Classification Service
The classification service receives stored camera images and creates image cutouts for both direct perspective (side view) and mirror perspective (top view). Then CNN inference is triggered on both cutouts simultaneously for part class prediction. The prediction results are again distributed via a TCP message.

## NUC / Serial Service
The serial service is a gateway between the TCP socket connection and the USB/Serial interface for Arduinos. As of now, only a single Arduino is part of the machine. It is controlling the servos of the rotational slide. After a part class prediction message is received, the serial service forwards a slide positioning message to the Arduino. The Arduino then controls the servos to smoothly rotate the slide to the corresponding storage bin location.

## NUC / Notification Service
The notification service is handling non-visual human machine interaction. This includes both audio feedback on part class prediction results as well as notifications on soft e-stop states of the machine. Soft e-stops are currently only triggered if no part was detected within the last 60s. This can be caused by the storage conveyor running empty or a part blocking the stream. In future, optical encoders are planned to be added to monitor belt speeds / detect blocked conditions. Based on the suggestion of a dear friend, error conditions are now forwarded to smartphones via the Pushover service 😉.

This concludes today’s view into the sorter architecture. I am always interested to get in contact with other sorting machine builders. Feel free to contact me via DM on Instagram.
