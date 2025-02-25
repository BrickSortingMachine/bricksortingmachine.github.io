---
layout: post
title: "Exploring LEGO Sorting Machines: A Survey of Designs"
description: There are countless ingenious LEGO sorting machines online, so I set out to create a systematic overview of the designs.
date: 2023-12-13 12:00:00 +0100
author: bsm
image: '/assets/images/survey/01_collage.png'
image_caption: 'Collage of sorting machines'
tags: [community]
featured: true
---
Probably the best-known LEGO sorter is Daniel West's <a href="https://www.youtube.com/watch?v=04JkdHEX3Yk" target="_blank">Universal LEGO Sorting Machine</a>. His work was inspired by Akiyuki's <a href="https://www.youtube.com/watch?v=6lZ9rSZwDzE" target="_blank">NXT Vision Guided Brick Sorter</a> and Jacques Mattheij's <a href="https://jacquesmattheij.com/sorting-two-metric-tons-of-lego/" target="_blank">Sorting two metric tons of lego</a>. Focusing on hardware, all three machines show a similar four stage design:

**Bulk Storage → Part Separation → Classification → Sorted Storage**

The following overview will look at a larger field of machines and show the creative variety in designing each stage.

## Stage 1 — Bulk Storage
In bulk storage you have a large amount of unsorted, entangled bricks and the goal is to feed it to the machine progressively. There are two typical designs used for bulk brick storage. Nr. 1 is what I call the "belt slowly moving under pile of bricks" type. Two nice examples can be seen with Daniel's and Jacques Mattheij's machines.

![The WORLD'S FIRST Universal LEGO Sorting Machine]({{site.baseurl}}/assets/images/survey/02_daniel_west_bulk.png){:loading="lazy"}
*From Daniel West's [The WORLD'S FIRST Universal LEGO Sorting Machine](https://www.youtube.com/watch?v=04JkdHEX3Yk)*

![Sorting two metric tons of lego.]({{site.baseurl}}/assets/images/survey/03_jaques_mattheij_bulk.png){:loading="lazy"}
*From Jacques Mattheij's Sorting two metric tons of lego*

While in Daniel's Design, we have a narrow bulk storage where the full width of the ground is transporting bricks, Jacques's machine features small 1x4 tiles being glued to the belt. As a result only the small middle part is feeding a small amount of bricks to the machine. If you want to learn more about these two machines, both Daniel (<a href="https://towardsdatascience.com/a-high-speed-computer-vision-pipeline-for-the-universal-lego-sorting-machine-253f5a690ef4" target="_blank">here</a> and <a href="https://towardsdatascience.com/how-i-created-over-100-000-labeled-lego-training-images-ec74191bb4ef" target="_blank">here</a>) and Jacques published additional background information (<a href="https://jacquesmattheij.com/sorting-two-metric-tons-of-lego/" target="_blank">Part 1</a>, <a href="https://jacquesmattheij.com/sorting-lego-the-software-side/" target="_blank">Part 2</a> and <a href="https://jacquesmattheij.com/sorting-lego-many-questions-and-this-is-what-the-result-looks-like/" target="_blank">Part 3</a>).

The bulk storage design Nr. 2 is based on a "step feeder", where a step is moving vertically through the storage pile and feeds a small portion of bricks into the machine. Akiyuki's, Francisco Garcia's and Johann Rocholl's machines employ this design idea.

![LEGO Mindstorms NXT Vision Guided Brick Sorter ver1]({{site.baseurl}}/assets/images/survey/04_akiyuki_bulk.png){:loading="lazy"}
*From Akiyuki's [LEGO Mindstorms NXT Vision Guided Brick Sorter ver1](https://www.youtube.com/watch?v=6lZ9rSZwDzE)*

![Lego Sorter with TensorFlow on Raspberry Pi]({{site.baseurl}}/assets/images/survey/05_franzisco_garcia_bulk.png){:loading="lazy"}
*From Francisco Garcia's [Lego Sorter with TensorFlow on Raspberry Pi](https://www.youtube.com/watch?v=uCuQsNwX1QY)*

![Brick feeder prototype]({{site.baseurl}}/assets/images/survey/06_johann_rocholl_bulk.png){:loading="lazy"}
*From Johann Rocholl's [Brick feeder prototype](https://www.youtube.com/watch?v=TYAh1lxqg8o)*

## Stage 2 — Part separation
The task of part separation is to take the entangled stream of bricks and separate it into individual parts which can be passed on to the scanner strictly one by one at a time. Separation is especially challenging with LEGOs, since the parts have a huge variety in size (e.g. 1x1 plates stuck inside a window) and also friction (e.g. bricks vs. rubber wheels). On the machines I saw so far, part separation is built up from one of the following tools.

**Chicaning Conveyors** are belts with diagonal barriers which force the parts on the conveyor to align sequentially. The delicious video below shows the chicanes being used in the food industry.

<p><iframe src="https://www.youtube.com/embed/CrGrcaJoyws" loading="lazy" frameborder="0" allowfullscreen></iframe></p>

Here are nice examples of chicaning conveyors in Lego sorting machines.

![Lego Sorter with TensorFlow on Raspberry Pi]({{site.baseurl}}/assets/images/survey/07_francisco_garcia_cc.png){:loading="lazy"}
*From Francisco Garcia's [Lego Sorter with TensorFlow on Raspberry Pi](https://www.youtube.com/watch?v=uCuQsNwX1QY)*

![Deep Learning Lego Sorter]({{site.baseurl}}/assets/images/survey/08_peter_back_cc.png){:loading="lazy"}
*From Peter Backx's [Deep Learning Lego Sorter](https://www.streamhead.com/3d%20printing/ai/2021/11/01/deep-learning-lego-sorting.html)*

**Two-speed belt steps** are another possible component to achieve part separation. They consist of a slow moving conveyor belt, which drops parts onto a second, much faster moving belt. This feature takes parts which are already sequentially aligned and spreads them out longitudinally.

![LEGO Mindstorms NXT Vision Guided Brick Sorter]({{site.baseurl}}/assets/images/survey/08_akiyuk_step.png){:loading="lazy"}
*From Akiyuki's [LEGO Mindstorms NXT Vision Guided Brick Sorter](https://www.youtube.com/watch?v=6lZ9rSZwDzE)*

![Lego Sorter with TensorFlow on Raspberry Pi]({{site.baseurl}}/assets/images/survey/09_francisco_garcia_step.png){:loading="lazy"}
*From Francisco Garcia's [Lego Sorter with TensorFlow on Raspberry Pi](https://www.youtube.com/watch?v=uCuQsNwX1QY)*

The **vibration feeder** is the most frequently used part separator. It strongly shakes parts inside a v-shaped channel. As a result it forces the parts to align sequentially. Vibration feeders have the advantage of being able to separate even entangled parts. The amplitude and frequency of the vibrations as well as the slope of the feeder needs to be tuned well to achieve good separation performance.

![Universal LEGO Sorting Machine]({{site.baseurl}}/assets/images/survey/10_daniel_west_vchannel.png){:loading="lazy"}
*From Daniel West's [Universal LEGO Sorting Machine](https://www.youtube.com/watch?v=04JkdHEX3Yk)*

![Sorting two metric tons of lego]({{site.baseurl}}/assets/images/survey/11_jacques_matteij_vchannel.png){:loading="lazy"}
*From Jacques Mattheij's [Sorting two metric tons of lego](https://jacquesmattheij.com/sorting-two-metric-tons-of-lego/)*

![Big Robot LEGO Sorting Machine]({{site.baseurl}}/assets/images/survey/12_chris_james_vchannel.png){:loading="lazy"}
*From Chris James's [Big Robot LEGO Sorting Machine](https://www.youtube.com/shorts/7FFnoSeIwnU)*

![Brick feeder prototype]({{site.baseurl}}/assets/images/survey/13_johann_rocholl_vchannel.png){:loading="lazy"}
*From Johann Rocholl's [Brick feeder prototype](https://www.youtube.com/watch?v=TYAh1lxqg8o)*

![Lego Sorting machine close-up]({{site.baseurl}}/assets/images/survey/14_peter_v_vchannel.png){:loading="lazy"}
*From Peter V's [Lego Sorting machine close-up](https://www.youtube.com/watch?v=ZOox_HX_6eo)*

Also combinations of these designs are possible. The LegoLAS system by Jörn Schlingensiepen runs two vibration feeders at different slopes and thus effectively different transport speeds. This combines the sequential alignment of the vibration feeder with the longitudinal spreading of the belt step.

![Lego Automatic Sorting LegoLAS2.0]({{site.baseurl}}/assets/images/survey/15_joern_schlingensiepen_vchannel.png){:loading="lazy"}
*From Jörn Schlingensiepen's [Lego Automatic Sorting LegoLAS2.0](https://www.youtube.com/watch?v=sCfN5LrUlKc)*

## Stage 3 — Classification
After part separation, the bricks are transported one by one into the classification stage. Its task is to recognize/classify parts or part categories. Most classification stages rely on visual recognition via camera images. There are different approaches in how camera based scanners are designed. Driving motivation is to capture parts from multiple perspectives because sometimes parts are hard to distinguish from certain angles. Also strong, non-flickering lighting, which is decoupled from the environment is important. It allows cameras to operate on very short exposure times to minimize motion blur.

**Multiple Poses** — Daniel's machine achieves capturing of multiple perspectives by letting the parts run towards the camera. The angle of observation and the scale of the part thus changes slightly while the parts are approaching. A specialty of this setup is that the classifier needs to become scale invariant. It thus can't use absolute image dimensions as a classification cue.

![Universal LEGO Sorting Machine]({{site.baseurl}}/assets/images/survey/16_daniel_west_visualization.png){:loading="lazy"}
*From Daniel West's [Universal LEGO Sorting Machine](https://www.youtube.com/watch?v=04JkdHEX3Yk)*

**Multiple Cameras** — Gijs van Haeff's sorting machine instead uses multiple cameras to capture multiple perspectives simultaneously.

![Universal LEGO Sorting Machine]({{site.baseurl}}/assets/images/survey/17_gijs_van_haeff_vision.png){:loading="lazy"}
*From Gijs van Haeff's [Universal LEGO Sorting Machine](https://www.youtube.com/watch?v=9OO0SsRy6FE)*

**Mirror** — Johann Rocholl's sorter features a single camera and a mirror to capture two perspectives at once. This design reduces complexity, ensures synchronization between the captured images and greatly reduces bus/CPU load compared to grabbing multiple cameras.

![Conveyor belt for LEGO sorting]({{site.baseurl}}/assets/images/survey/18_johann_rocholl_mirror.png){:loading="lazy"}
*From Johann Rocholl's [Conveyor belt for LEGO sorting](https://www.youtube.com/watch?v=o-FL02ePFEU)*

**Smartphone** — Spencer Hunber's Nexus sorting machine is using a smartphone for high quality camera and potential CNN accelerator hardware.

![Nexus]({{site.baseurl}}/assets/images/survey/19_spencer_huber_mobile.png){:loading="lazy"}
*From Spencer Hubert's [Nexus](https://github.com/spencerhhubert/nexus)*

**Scale** — Part weights are a great complementary feature to standard visual input for classification. Akiyuki fitted a digital scale to his Lego sorting machine. This can be achieved using either a USB scale or via a camera looking at the display of the scale and doing basic character recognition. However, the classifier needs to be adapted to accept multimodal input. A mechanism is also needed for pushing parts onto and off the scale. The weight feature could also be useful for detecting multiple parts erroneously presented to the camera at the same time. By combining visual input with part weights, sorting machines potentially can achieve higher classification accuracy.

![LEGO Mindstorms NXT Vision Guided Brick Sorter]({{site.baseurl}}/assets/images/survey/20_akiyuki_scale.png){:loading="lazy"}
*From Akiyuki's [LEGO Mindstorms NXT Vision Guided Brick Sorter](https://www.youtube.com/watch?v=6lZ9rSZwDzE)*

## Stage 4 — Sorted Storage
After the correct part type has been identified inside the classification stage. The part can be directed to its correct storage location. This can be achieved using one of the following approaches.

**Horizontal Gates** — Usually a conveyor belt with mechanical arms which direct the part into the intended bucket. The two examples below don't just guide the part but even actively push the parts into the bucket while closing. This allows parts to follow each other more closely on the belt.

![Lego Sorting Machine]({{site.baseurl}}/assets/images/survey/21_neal_anthoons_gates.png){:loading="lazy"}
*From NealAnthoons's [Lego Sorting Machine](https://www.youtube.com/watch?v=6IAMW4N4ohY)*

![Universal LEGO Sorting Machine]({{site.baseurl}}/assets/images/survey/22_gijs_van_haeff_gates.png){:loading="lazy"}
*From Gijs van Haeff's [Universal LEGO Sorting Machine](https://www.youtube.com/watch?v=9OO0SsRy6FE)*

**Vertical Gates** turn the principle around and replace the conveyor with a vertical channel through which the parts are falling. A gate directly above the target bin then directs them to the right place. The speed of the falling part is high thus allowing parts to be sorted quickly.

![Sorting Machine Flap Design]({{site.baseurl}}/assets/images/survey/23_johann_rocholl_vertical_gates.png){:loading="lazy"}
*From Johann Rocholl's [Sorting Machine Flap Design](https://www.youtube.com/watch?v=ZGXZsMSBHzg)*

![Nexus]({{site.baseurl}}/assets/images/survey/24_spencer_huber_vertical_gates.png){:loading="lazy"}
*From Spencer Hubert's [Nexus](https://github.com/spencerhhubert/nexus)*

**Pneumatic Sorters** use a short, directed blast of air to push the parts off the belt and into the storage bin. They feature very little moving parts and typically use a solenoid valve which can be triggered from GPIO ports. Timing is crucial in order for the parts not to fly sideways into the wrong bin. A belt position encoder (e.g. optically via the wiggly line in Jacques's design) helps measuring the exact belt and thus part position. A belt with lateral cleats (see Eppos Vision System below) helps to keep the parts on course when they fly with the air stream. Jacques Mattheij's machine apparently even adjusts the dose of air based on the respective part size. Finally it is very helpful to use a silent air compressor, since normal ones are quite loud for long term usage. Apart from the compressor noise, personally I think pneumatic sorters at work are super relaxing to watch 😉

![Sorting two metric tons of lego]({{site.baseurl}}/assets/images/survey/25_jacques_matteij_air.png){:loading="lazy"}
*From Jacques Mattheij's [Sorting two metric tons of lego](https://jacquesmattheij.com/sorting-two-metric-tons-of-lego/)*

![The Shape Sifter — First working demonstration]({{site.baseurl}}/assets/images/survey/26_peter_v_air.png){:loading="lazy"}
*From Peter V's [The Shape Sifter — First working demonstration](https://www.youtube.com/watch?v=0VHN3AZKY0E)*

![Automatic LEGO sorting machine]({{site.baseurl}}/assets/images/survey/27_eppos_vision_air.png){:loading="lazy"}
*From Eppos Vision System's [Automatic LEGO sorting machine](https://www.youtube.com/watch?v=FCiqmOP6NQc)*

**Rotary Slides** again use mechanical servos but instead of just binarily opening or closing a gate they choose one out of many storage locations by pointing a slide towards the target. This design is very efficient in the number of servos required. In theory multiple such slides could even be cascaded.

![Lego Sorter with TensorFlow on Raspberry Pi]({{site.baseurl}}/assets/images/survey/28_francisco_garcia_slide.png){:loading="lazy"}
*From Francisco Garcia's [Lego Sorter with TensorFlow on Raspberry Pi](https://www.youtube.com/watch?v=uCuQsNwX1QY)*

![Automated AI LEGO Sorting machine]({{site.baseurl}}/assets/images/survey/29_claus_christiansen_slide.png){:loading="lazy"}
*From Claus Christiansen's [Automated AI LEGO Sorting machine](https://www.youtube.com/watch?v=vwPZwttLG2A)*

![Lego Automatic Sorting LegoLAS2.0]({{site.baseurl}}/assets/images/survey/30_joerg_schlingensiepen_slide.png){:loading="lazy"}
*From Jörn Schlingensiepen's [Lego Automatic Sorting LegoLAS2.0](https://www.youtube.com/watch?v=sCfN5LrUlKc)*

![LEGO Sortierer (Color Sorter) mit raspberry pi]({{site.baseurl}}/assets/images/survey/31_michael_talarczyk_slide.png){:loading="lazy"}
*From Michael Talarczyk's [LEGO Sortierer (Color Sorter) mit raspberry pi](https://www.youtube.com/watch?v=jego7nntfAM)*

**Picking Robots** are the final variant of sorting systems. A robotic arm is grabbing the parts, moving over a 2D set of storage locations and dropping it into the respective bin. While such part handling takes more time, the two-dimensional storage matrix allows for an extremely large amount of bins.

![Robotic LEGO sorting robotwith machine learning]({{site.baseurl}}/assets/images/survey/32_tampere_univeristy_robot.png){:loading="lazy"}
*From Tampere University's [Robotic LEGO sorting robotwith machine learning](https://www.youtube.com/watch?v=qUhMBUhAEMc)*

![First automatic Lego™ bricks sorting system]({{site.baseurl}}/assets/images/survey/33_rbtx_arm.png){:loading="lazy"}
*From RBTX's [First automatic Lego™ bricks sorting system](https://www.youtube.com/watch?v=Gwx8xHtitGA)*


## Recent Updates

In the time since I wrote this article new machines continue to be in the making. In this section I am trying to keep up with recently published machines.

### 2023–12–27
360er0/awesome-lego-machine-learning gives a great overview on LEGO machine learning projects including many sorting machines.

### 2024–03–13
Freakstuff published a video on his automatic sorting machine. What's special about this project is, that it is purely mechanical. It sorts LEGO parts by size. This is both very useful for subsequent manual sorting and as a preceding step for automated shape sorting. In shape sorting, part separation is a very hard task which gets much easier if parts are pre-sorted to be similar in size.

![Freakstuff's automatic sorting machine (German)]({{site.baseurl}}/assets/images/survey/36_freakstuff.webp){:loading="lazy"}
*From Freakstuff's [automatic sorting machine (German)](https://www.youtube.com/watch?v=AhR8x4PuMIM)*

Looking at the design in detail, the 4 typical stages are still apparent even though being grouped in an interesting way.

Bulk storage is organized as a wooden crate with a step feeder which ensures a constant in-flow of parts. The step is oriented parallel to a conveyor belt. With each stroke the step releases a well defined portion of bricks in longitudinal sequence onto the conveyor. This realizes the required part separation.

![Freakstuff's step feeder]({{site.baseurl}}/assets/images/survey/37_freakstuff.webp){:loading="lazy"}
*Freakstuff's step feeder*

Part classification (in terms of part size) is implemented using a sequence of sieve tubes featuring progressively larger openings. Small parts fall through the openings in the early stages, larger parts get transported further on to fall into a later bin.

The sieve openings are designed in a spiral shape. This is a very interesting choice which according to freakstuff is key for the parts to progress through the tubes in a continuous motion.

![Freakstuff's spiral shaped sieve tubes]({{site.baseurl}}/assets/images/survey/38_freakstuff.webp){:loading="lazy"}
*Freakstuff's spiral shaped sieve tubes*

According to Freakstuff, his machine is already used in production in his BrickLink store, followed by manual sorting for individual parts. He is planning to extend the setup by a visual classification based auto sorting stage. Classification shall be realized via the the brickognize web service. In general it will remain interesting to follow the project on his channel.

### 2024–05–21
In a parallel development, Smyrnoff Specialist Lego Parts has also been working on a fully mechanical sorter since January of this year. The design is similar to Freakstuff's approach, utilizing tube modules with progressively larger dimensions for part sorting. Each module incorporates a spiral shape for efficient part transport. This machine is constructed from a combination of LEGO elements as well as 3D printed components.

![Sorter for LEGO® bricks by Smyrnoff Specialist Lego Parts]({{site.baseurl}}/assets/images/survey/39_smyrnoff.webp){:loading="lazy"}
*[Sorter for LEGO® bricks](https://www.instagram.com/p/C6RwE0trDwt) by Smyrnoff Specialist Lego Parts*

## Feedback and Contact
If you are also currently in the process of building a sorting machine I would love to hear from you. Also if you would like to add a missing machine/design to this list please contact me. In all cases I am easiest to reach via DM as [BrickSortingMachine](https://www.instagram.com/bricksortingmachine) on Instagram.
