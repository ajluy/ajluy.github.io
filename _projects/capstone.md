---
title: "Glove Controller for Guitar Hero"
date: "2025-05-10"
category:
  - Electrical/Mechanical
description: "A wearable, two-glove Guitar Hero controller built on ESP32s, using flex sensors, IMUs, and wireless communication to replace the traditional plastic guitar with a lightweight, affordable alternative."
image: "/assets/images/glove_controller/glove_final.png"
link: ""
---

As part of a capstone project me along with 2 other computer engineers decided to design a glove controller for guitar hero, where I spesifically centered on the physical hardware design, power system, illustration, and final assembly, working closely with teammates who handled firmware and PCB layout to bring the full system together.

Illustration & Early Ideation

Before any components were ordered or code was written, I took on the role of illustrating the initial concept diagrams and physical layout sketches for the team. Getting a shared visual reference early on so teammates could see where each component would sit, how the wiring would route, and how the two gloves related to each other as a system, it became easier to have concrete conversations about firmware decisions, PCB design, and control mechanics. The whiteboard sketches and layout diagrams gave the team something tangible to react to and refine collaboratively.


|![](/assets/images/glove_controller/glove_sketch.png) | ![](/assets/images/glove_controller/glove_sketch1.png)|

Power System & Hardware Layout

One of my primary responsibilities was selecting a power supply that met the ESP32's requirements while remaining small enough to embed in a wearable. I landed on 3.7V 800mAh lithium-ion cells for each glove, regulated down to 3.3V to power the ESP32, IMU, and voltage divider circuits. When our custom PCB ran into issues with its charging circuit and voltage regulator, I adapted by soldering the regulator directly to the 3.3V rail pins and wiring the battery JST receptor accordingly, keeping the system functional despite the board issues.

This power architecture informed several downstream design decisions. With a self-contained source on each glove, we had wireless freedom, but it also meant keeping component count low and current draw manageable to hit our 2+ hour battery life target, constraints I worked through in close coordination with the teammates designing the PCBs.

Physical Design & Controls

The early layout helped the team think through how the controller should actually behave. Mapping the flex resistors to individual fingers in the diagrams made it immediately clear that fretting should mirror the natural curl of pressing down, which aligned with how Guitar Hero players already think about finger placement. Positioning the IMU on the back of the left hand in the layout pointed toward using a strong upward lift for star power, a gesture that emerged partly from where the sensor sat rather than being designed top-down. On the right glove, illustrating the IMU as the primary strum sensor reinforced that the strum motion should feel like an actual strum rather than a button press. The physical layout, in that way, helped the team settle on control mechanics that felt intuitive, and gave my teammates a concrete reference when building out the gesture detection logic.

|![](/assets/images/glove_controller/glove_layout.png) | ![](/assets/images/glove_controller/glove_layout1.png)|

For both gloves, I sewed the electronics into an inner glove and placed an outer glove over the top to conceal wiring and hold components in place. This two-layer approach kept the build clean and protected connections during play, while keeping the overall form factor light enough to wear comfortably through a full session.

![](/assets/images/glove_controller/glove_final.png)

Component Sourcing & Budget

A core motivation for the project was building something cheaper than what is currently available. Replacement Guitar Hero controllers are scarce and expensive, and the closest alternative on the market, the AIRAIX haptic glove, runs significantly higher than what most players would spend. We wanted to undercut that while still delivering a functional, responsive controller.

That goal made the $407.61 total budget feel tight in practice. Roughly half went toward the custom PCBs, which meant every other purchasing decision required some prioritization. We had to be deliberate about what was worth ordering and what could be tested with what we already had. Common materials like solder, tape, and thread were sourced from the engineering building to preserve budget for components that actually required ordering.

The initial prototype came in around $130 using pre-built ESP32 dev boards, which gave the team a low-cost way to validate the design before committing to PCB fabrication. That framing, test cheaply first, spend on refinement second, shaped how we approached the whole build. When the right glove PCB never arrived, the dev board assembly we had used for early testing became the final right glove, and it held up well enough that the tradeoff was worth it. I handled the sewing and final assembly for both gloves ahead of the demo, pulling the hardware side together while my teammates finalized BLE and firmware integration.
