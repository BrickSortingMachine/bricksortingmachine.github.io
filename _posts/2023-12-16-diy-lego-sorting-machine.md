---
layout: post
title: "DIY LEGO Sorting Machine"
description: The first video of the machine is released - let me give some background on the design choices of my build.
date: 2023-12-16 12:00:00 +0100
author: bsm
image: '/assets/images/intro-own/Scanner2.png'
image_caption: 'View into the LEGO brick scanner'
tags: [build]
featured: false
---
The [preceding article]({{site.baseurl}}/exploring-lego-sorting-machines-a-survey-of-designs) provided a comprehensive overview of the wide range of existing LEGO sorting machines. Joining the release video below, this article will look into the details and individual components of our specific sorting machine, explaining the rationale behind various design decisions.

<p><iframe src="https://www.youtube.com/embed/FRHMMGDMjuQ?si=CGcTTlynZEoe7O72" loading="lazy" frameborder="0" allowfullscreen></iframe></p>

Constructing a complete sorting machine requires developing a long list of components and addressing various design challenges. Given that this is a hobby project, there was a strong need to minimize development time and effort to achieve a functional system within a reasonable timeframe. The foundational decision thus was to construct the machine out of LEGO components itself. This safes on part manufacturing and enables rapid cycles of design and testing. Achieving long-term durability and high operational uptime presents a challenge when using standard LEGO parts. For this reason, the design incorporates non-LEGO components, such as [metal gear motors](https://www.reichelt.de/getriebemotor-27-mm-90-1-12-v-dc-gm27-90-12v-p159631.html?nbc=1), [LEGO compatible metal gears or axles](https://metal-technic-parts.com) and [rubber conveyor bands](https://www.ebay.de/itm/334604695326), where necessary.

Next, this article will examine the 4 principal stages common to most sorting machines:

**Bulk Storage → Part Separation → Classification → Sorted Storage**

## Bulk Part Storage
The bulk storage system follows the “belt-beneath-a-pile-of-bricks” design of [Daniel West](https://www.youtube.com/watch?v=04JkdHEX3Yk), [Jacques Mattheij](https://jacquesmattheij.com/sorting-two-metric-tons-of-lego/), [Gijs van Haeff](https://www.youtube.com/watch?v=9OO0SsRy6FE) and many others. However, the design diverges in one aspect. Instead of continuously moving the belt through a large accumulation of parts, the parts are piled directly atop the conveyor belt. This modification means that the belt must move at a considerably slower pace, as a single half-cycle effectively empties the storage area. The advantage of this approach is that it eliminates the risk of voids or cavities forming within the pile of stored components above the belt.

![Bulk storage conveyor belt]({{site.baseurl}}/assets/images/intro-own/01_bulk.webp){:loading="lazy"}
*Bulk storage conveyor belt*

## Part Separation
The next crucial step of the sorting machine’s workflow is to separate and disentangle the LEGO parts, preparing them for the scanning stage. To accomplish this, the design employs a dual set of V-channel vibration feeders, offering several advantages:

1. Lateral Alignment: Parts are automatically aligned into a single line
2. Stacking Prevention: The vibrational mechanism ensures that stacked parts slide down, while the amplitude of vibrations is small enough to prevent adjacent parts from stacking atop one another.
3. Retention of Round Elements: The V-channel’s inherent friction prevents round parts, such as pins, from rolling away when the feeder comes to an abrupt halt — unlike what occurs with a conventional conveyor.

![V-channel vibration feeder]({{site.baseurl}}/assets/images/intro-own/02_vibration-feeder.webp){:loading="lazy"}
*One of two v-channel vibration feeders*

The V-channel is constructed from two 8-stud wide plates set at a 90-degree angle, with paper tape adhered to their surfaces to reduce some friction (will be replaced by large LEGO tiles in future). Even with the large variance in frictional properties between LEGO components — such as plastic parts vs. rubber tires — this approach has proven effective. The plates are structurally supported by a frame made of technic bricks, optimized for minimal weight. This frame is suspended on rubber o-rings, allowing slight longitudinal and vertical movements but restricting lateral shifts.

At the center of the frame, an axle holds an offset weight, composed of gray pins on lift arms. A [LEGO 9V 74569](https://www.philohome.com/motors/motorcomp.htm) motor, connected to this axle via two universal joints, powers the rotation of the offset weight without itself being subject to vibration. This design not only saves weight but also extends the motor’s lifespan. After mechanically integrating the feeder, it’s crucial to fine-tune both frequency (via motor rotation speed) and amplitude (via the mass of the offset weight) for efficient part transportation.

![Storage conveyor with v-channel vibration feeders]({{site.baseurl}}/assets/images/intro-own/02_bulk-and-feeder.webp){:loading="lazy"}
*Storage conveyor with v-channel vibration feeders*

The bulk storage conveyor releases parts into the first v-channel based on a timer mechanism. Specifically, the conveyor advances approximately 5mm every time the feeder’s vibrations accumulate to a 12-second duration. This timing configuration has proven effective across a wide range of LEGO part sizes.

![Parts longitudinally close in the v-channel]({{site.baseurl}}/assets/images/intro-own/03_top-view-feeder.webp){:loading="lazy"}
*Parts longitudinally close in the v-channel*

The v-channel is designed to align parts in a linear sequence, although the parts remain closely spaced. Consequently, there’s a risk that multiple parts may be ejected from the V-channel in quick succession. To ensure that the scanner processes only one part at a time, the machine deactivates the v-channel as soon as its camera detects a part on the conveyor belt.

Latency is a crucial factor in this system. If the parts are too closely spaced, the v-channel’s deactivation may be delayed, resulting in multiple parts being mistakenly sent towards the scanner. To mitigate this issue, the vibration feeder of the V-channel operates in a pulsed manner. Each pulse is typically short enough to eject only a single part, while the pause between pulses provides the scanner with some extra time to detect any part being dispensed.

## Scanner
Following the part separation stage, individual LEGO bricks are conveyed to the scanner for recognition and classification. The scanning system is solely camera-based, featuring a conveyor belt that transports the LEGO bricks past the camera.

![View through the scanner towards the v-channel with mirror and camera]({{site.baseurl}}/assets/images/intro-own/04_scanner.webp){:loading="lazy"}
*View through the scanner towards the v-channel with mirror and camera*

The design of the scanner adopts a key idea from Johann Rocholl’s [Conveyor belt for LEGO sorting](https://www.youtube.com/watch?v=o-FL02ePFEU). The solution consists of a single camera paired with a mirror, allowing the machine to capture two different perspectives simultaneously. The core motivation behind this is to capture the LEGO parts from multiple perspectives, as some parts are difficult to identify when viewed from certain angles. Choosing a mirror over multiple cameras not only simplifies the overall design but also ensures synchronization between the captured images. Additionally, it significantly reduces the computational and bus load.

Lighting is another crucial element in each scanning system. The machine utilizes strong, non-flickering illumination that is isolated from external environmental factors. This approach allows the camera to operate with very short exposure times, effectively minimizing motion blur and thereby enhancing the accuracy of the part identification process.

Object detection is realized via [OpenCV’s MOG background subtraction](https://docs.opencv.org/3.4/d8/d38/tutorial_bgsegm_bg_subtraction.html). The moment the detected part reaches a pre-defined position in the image, two cut-outs are taken. One of the direct view and one via the indirect mirror view. Both cutouts are presented simultaneously to a multi input CNN, which consists of two weight sharing instances of the same pre-trained MobileNetV2 encoder plus a dense classification head. The network thus always works on image pairs. Both during training and inference.

## Sorter
After the scanner successfully identifies the part type, the next step is to guide these parts into the corresponding storage compartment. The [preceding article]({{site.baseurl}}/exploring-lego-sorting-machines-a-survey-of-designs) gave an overview of existing solutions. Again the design was primarily driven by minimizing complexity, both in terms of the number of moving parts and required motion control accuracy.

![Rotary slide consisting of the base with servo and cardboard slide on top]({{site.baseurl}}/assets/images/intro-own/05_slide.webp){:loading="lazy"}
*Rotary slide consisting of the base with servo and cardboard slide on top*

The rotary slide design requires only a single LEGO compatible 360° servo. In the current configuration, it serves up to 12 storage compartments. This limitation originates in the size of storage bins and the repetition accuracy of the slide. The servo is controlled by an Arduino Nano to minimize servo jitter and enable smoothly accelerated motion (ServoEasing library). The Arduino receives control messages via USB from the control PC. While the usage of sorting bins has proven effective for today, it will need an upgrade in bin size to accommodate larger-scale operations in the near future.

## Summary
This concludes the overview of the current design. Future posts will give updates on the currently ongoing machine updates. Feel free to comment in case you are interested in further specific details. To close this article let me try to transport the surprising feeling when you have a running sorter, sorted a large box of parts and suddenly you need to find an efficient way how mix them up again 😉