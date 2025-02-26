---
layout: post
title: "Scaling Up LEGO Brick Storage for Large-Scale Sorting"
description: Let's explore the idea of significantly expanding the amount of sorted storage bins - to 100, 200, or potentially thousands of bins.
date: 2025-01-18 12:00:00 +0100
author: bsm
image: '/assets/images/asrs/complete.gif'
image_caption: 'CAD drawing of the automated storage and retrival system'
tags: [build, update, asrs]
featured: false
---
The motivation is straightforward: LEGO so far has produced approximately 20,000 different parts (including variations such as color). To advance sorting machines beyond handling part classes and enable sorting by individual part IDs, the number of discrete storage locations must strongly increase.

Storage approaches typically scale hardware needs linearly in the number of bins. For example, a <a href="/survey/Exploring-LEGO-Sorting-Machines-A-Survey-of-Designs/#stage-4--sorted-storage">belt-and-gate system</a> requires one dedicated gate and servo for each storage location. This quickly becomes infeasible as the number of bins increases, leading to complex and expensive machines.

**A Scalable Approach: Automated Storage and Retrieval Systems (AS/RS)**

To overcome this limitation, I'm exploring an approach with more favorable scaling properties. It draws inspiration from large-scale warehouse storage, specifically Automated Storage and Retrieval Systems (AS/RS). These systems efficiently manage vast quantities of goods using automated cranes or shuttles to retrieve items from dense storage racks.

![Photo of an automated highbay warehouse]({{site.baseurl}}/assets/images/asrs/arno-senoner-warehouse-wide.jpg){:loading="lazy"}
*An automated highbay warehouse (photo by [Arno Senoner](https://unsplash.com/@arnosenoner?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash) on [Unsplash](https://unsplash.com/photos/blue-and-brown-metal-bridge-yqu6tJkSQ_k?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash))*

Many DIY AS/RS projects have emerged within the maker community, demonstrating the feasibility of adapting this technology for smaller-scale applications. These projects often utilize readily available components like stepper motors, linear rails, and microcontrollers.

[Insert Image: A conceptual image showing a LEGO sorting machine in the foreground with a simplified AS/RS system behind it. The sorting machine's output feeds into the AS/RS system. This could be a simple 2D drawing or a more elaborate 3D render.]

**Retrieval Times and Buffer Considerations**

A key consideration with AS/RS is retrieval time. We need to analyze the trade-off between latency (the time it takes to retrieve a single part) and overall system speed. While a single retrieval might take slightly longer than a direct drop into a bin, the ability to access thousands of parts from a compact storage unit offers significant advantages.

To further optimize performance, a buffer section can be implemented between the sorting mechanism and the AS/RS. This buffer would temporarily hold sorted parts, allowing the AS/RS to operate more efficiently by batching retrievals.

**CAD Model**

[Insert Image: A CAD model of the proposed AS/RS system designed for LEGO storage. This should showcase the storage racks, the retrieval mechanism (e.g., a robotic arm or shuttle), and how it interfaces with the output of the LEGO sorting machine. It's important to showcase the density of the storage and the mechanism for accessing individual locations. No physical prototype photos are available yet.]

This CAD model illustrates the proposed design for a LEGO-specific AS/RS. It emphasizes compact storage and efficient retrieval, enabling the storage of a significantly larger number of LEGO parts compared to traditional methods. While a physical prototype is still under development, the CAD model provides a concrete visualization of the concept and its potential. This approach promises a significant leap in the scalability of LEGO sorting machines, paving the way for truly comprehensive part sorting.
