---
title: "Autonomous Boat - Power System & Mechanisims"
date: "2026-01-15"
category:
  - Electrical / Mechanical
description: "A fully autonomous low-profile vessel capable of navigating open water, evading detection, identifying and interacting with targets, launching a drone, and returning to its starting point without any human input"
image: "/assets/images/ndaimm/boat_field.png"
link: ""
---

 
NDAIMM (Notre Dame Artificial Intelligence Maritime Maneuver) is Notre Dame's entry in the AIMM Indiana Collegiate Challenge. The project is built around a fully autonomous low-profile vessel (LPV) that completes a series of maritime tasks including gate navigation, obstacle dodging, LIDAR evasion, buoy identification, payload deployment, drone launch, object recovery, and autonomous return, all without any human input after the mission starts.
 
I have been part of NDAIMM since the team was founded three years ago, working on the project from its first iteration through the current build. The 2025-2026 season was a major redesign. The previous boat had proven the concept worked, but it was heavy, hard to move, and difficult to update between test sessions. The team split into three tracks: mechanical, electrical, and software. Mechanical members led the new hull geometry and ballast system. The software team handled navigation and the AI inference pipeline. I led the electrical track, taking ownership of the power system design from component selection through integration and validation.
 
---
 
## Mechanical Design
 
The new hull is built on a modular box design, replacing a boat that was hard to transport, leaked frequently, and needed manual ballast weights to stay balanced. One of my early contributions was creating concept sketches to help the team visualize how everything would fit together before fabrication started. Working out where the electronics enclosures, thruster mounts, and attachment points would sit spatially on paper first made it much easier for mechanical and electrical work to happen in parallel without constantly waiting on each other.

![Modular Boat System](/assets/images/ndaimm/modular.jpg)

The front and back sections detach independently for easy component swaps and upgrades. An automatic ballast system pumps water in and out of a flooded compartment to manage trim, and also lowers the boat's profile for the Evade challenge.
 


---
 
## Propulsion
 
The boat runs on six ApisQueen U92 thrusters producing 64.2 kg of combined thrust in a skid-steer layout, with steering controlled by varying power between the left and right motor banks. The team selected this through a trade study, choosing it for maneuverability, redundancy, and resistance to debris fouling the propellers, which had caused problems the prior year.
 
---
 
## Electrical System
 
With the mechanical layout settled, the electrical work was mine to lead end to end. The core challenge was that six thrusters, a ballast system, sensors, heating elements, and communication hardware all running simultaneously have very different power requirements, and the system had to handle all of them without faults or thermal issues under real operating conditions.
 
I started by building out the component selection before any wiring began. That meant identifying the right ESCs to handle thruster load, choosing a power distribution module rated for the full system draw, and designing a charging setup that matched how the team needed to operate in the field. Each of those choices constrained the others, so I worked through them together rather than in isolation.
 
Leading the electrical track also meant managing how work got distributed across the team. In a competition club where there is always more to do than time allows, I delegated physical layout and construction to newer members so I could stay focused on design and system-level decisions. Several of those members were freshmen, and teaching them the reasoning behind the work, not just the task itself, was one of the more rewarding parts of the role. Getting someone to the point where they could work independently was genuinely fun and left the team in a better position for future builds.

![Internal control systems computer and wiring layout](/assets/images/ndaimm/electrical_internal.jpg)
 
### Power System
 
The main power module I selected is rated for 200A of continuous discharge, sized to cover the six thrusters plus all onboard systems under peak load. During load testing I found that the in-water stall current on the thrusters was significantly higher than bench measurements had suggested, enough to push the batteries into a thermal protection mode that throttled output. I traced the issue to the wire gauge feeding the power module not being sufficient for the actual load, and resolved it by upsizing those runs to hold a 1.5x safety margin on amperage. That kept the protection mode from ever triggering again under normal operation.
 
### Charging System
 
One of the specific things I changed from the prior design was the charging architecture. The old setup required physically disconnecting the batteries to charge them, which added handling time and risk between test sessions. I redesigned it so the system supports two explicit states: charging and connected. The batteries charge in parallel while staying series-connected, meaning no one has to touch the terminals between runs. I also added a redundant battery backup to keep the control computer powered if the main pack runs low, and kept a manual shutoff in place for emergency stops.
 
### Integration and Validation
 
After component selection, I worked through how each subsystem would be wired given its specific requirements and delegated the physical construction to team members once the layout was defined. The flooded ballast compartment needed power and data routed through sealed conduit to stay isolated. Electronics enclosures were sized and sealed around the components going into them. Control signals for the ballast valves, magnet relay, and recovery arm were routed to spare channels on the flight controller so they could all be triggered through the navigation system without adding extra hardware.
 
Before integrating, each component was tested individually against expected resistance and continuity values to confirm correct behavior. I used this process as a teaching moment with newer members, walking through what we were measuring and what a failure would look like, so they could run the checks themselves with confidence rather than just following steps.
 
![Power routing and wiring harness detail](/assets/images/ndaimm/wiring_detail.png)
 
---
 
## Control and Computing
 
The boat runs ArduPilot on a Pixhawk flight controller for navigation, with a high-performance companion computer handling the AI workload. The sensor suite includes stereo cameras for SLAM-based mapping, side cameras for buoy detection, a LIDAR module, and a thermal camera, giving the boat enough situational awareness to navigate the course and identify targets autonomously. Three radio systems handle communication: WiFi for live monitoring, an RC module for manual control and failsafe, and LoRa modules for long-range telemetry.
 
![GPS coordinate testing and path planning output on the companion computer GUI](/assets/images/ndaimm/computing.png)
 
---
 
## Challenge Solutions
 
The competition has nine sequential challenges and the team's strategy was to use GPS-based navigation as the reliable backbone, with sensor fusion layered on top where time allowed. Gate and Dodge both use the same waypoint navigation core to plot a square-wave path through buoy pairs. Evade drains the ballast compartment to drop the hull below the LIDAR beam. Identify fuses camera data with GPS to locate and drive toward the target buoy. Deploy releases a 1,200 lb-rated powered magnet payload on command via relay. Launch sends an autonomous drone to hold position at around 20 ft above the target before the operator triggers the drop. Recover extends a net arm to trawl the water surface for the object. Receive pulls data from the shore station over the LoRa radio link, and Return navigates the boat autonomously back to the launch point using GPS.
 
---
 
## Testing
 
Testing ran from February through April 2026. I validated each electrical component individually before system integration, then ran the full system through load testing at over 1,000 lbs. The stall current issue was caught during this phase and required rerouting wire runs to fix before the boat went on the water. System mode transitions and sensor performance were confirmed across two lake sessions.
 
![Boat operating in auto mode during lake testing](/assets/images/ndaimm/testing.png)
 
---
 
## Lessons Learned
 
The most important electrical lesson from this build was that bench motor current measurements do not predict in-water stall current. Running load tests under actual operating conditions earlier in the process would have caught the thermal protection issue before it became something that needed a last-minute fix.
 
The sketching process at the start also turned out to be worth more than I expected. It was a small investment upfront that removed a lot of coordination overhead later, and it is something I would do again on any project where multiple subsystems share physical space.
 