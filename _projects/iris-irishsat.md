---
title: "Atmospheric sensor - Heating and Power system"
date: "2025-05-10"
category:
  - Electrical/Mechanical
description: "A guided descent module developed through IrishSat that autonomously navigates HAB payloads to designated landing zones using a parachute-to-parafoil transition system."
image: "/assets/images/irishsat/launch.png"
link: ""
---

IRIS: Information Recovery Integrated System

IRIS is a guided descent module developed through IrishSat, Notre Dame's student satellite organization, designed to autonomously navigate HAB payloads to designated landing locations using a parachute-to-parafoil transition system. I served as project lead for the 2024-25 year, inheriting a system that had already demonstrated core functionality and focusing the team's efforts on reliability, refinement, and getting IRIS flight-ready.

Leading a Redesign Year

Inheriting a project that had already demonstrated core functionality meant the focus for the year was refinement rather than recovery. The primary mechanical direction was shrinking the overall system footprint, making IRIS easier to integrate with HAB payloads and improving flight characteristics without compromising what the previous iteration had proven out. Beyond that, I structured the year around letting team members propose improvements in their own areas, whether that was refining the heating system, rethinking power distribution, or improving internal organization, and my role was creating the space for those proposals to be evaluated seriously and integrated in a way that kept the system coherent. Much of my energy went into coordination across the electrical, mechanical, and software sides, making sure decisions were compatible with each other and that testing reflected real flight conditions rather than just bench conditions.

**2024**

![](/assets/images/irishsat/2024.png) 

**2025**

![](/assets/images/irishsat/2025.JPG) 

Power System & Budget

As components were swapped and updated across the electrical system throughout the redesign, I developed and maintained a formal power budget as a way to keep the integration process grounded. With changes happening across sensors, the heating grid, and communication hardware, the budget served as a living reference that was updated alongside the hardware rather than treated as a one-time document. It gave the team a shared way to track how each component decision affected the overall load, reason about the isolated heating, power, and control grids as a system, and catch potential conflicts early before they became integration problems. Having that accounting in place made it easier to evaluate proposed changes on their merits without losing sight of what the system could actually support.

![](/assets/images/irishsat/powerbudget.png)

Cold Testing

Before committing to a full HAB flight, I pushed to implement a formal cold test as a prerequisite for launch clearance within the team. IRIS operates at altitude where temperatures drop significantly, and validating that the system could maintain operation in those conditions on the ground was a step the previous iteration had not fully formalized. We ran IRIS through a -10°C cold test, confirming 2.5 hours of continuous operation, which gave the team a much clearer picture of thermal performance and helped validate the heating system design before the payload ever left the ground.

![](/assets/images/irishsat/cold1.png) 
![](/assets/images/irishsat/cold.png)

Satellite Communication Parsing

Another area I took direct ownership of was implementing the method to parse and receive data transmitted over the RockBLOCK 9603N Iridium satellite communication module. IRIS has the capability to uplink positional data over the Iridium network during flight, but getting that data into a usable format on the ground required building out the parsing pipeline on the receiving end. I worked through the message formatting and implemented the logic to correctly interpret incoming satellite transmissions, which gave the team real-time positional awareness during the full flight in May 2025.

Air Traffic Control Coordination

Coordinating with air traffic control was another responsibility I took on as project lead. HAB launches require communication with local ATC to ensure the balloon's flight path doesn't conflict with active airspace, and managing that process involved filing the appropriate notices, understanding the airspace constraints around our launch site, and making sure the team was ready to hold or adjust the launch window based on ATC guidance. It was a logistical piece that doesn't show up in the hardware but is essential for actually getting the system in the air legally and safely.
Flight Performance

IRIS completed its full flight in May 2025, landing approximately 2,700 feet off-target. For a first full flight of a guided descent system with a parachute-to-parafoil transition, it was a meaningful result and gave the team a clear set of data points to work from for future iterations. The system held together mechanically, the power system performed within budget, and the satellite communication link functioned during descent.

Ultimately, a system as technically broad as IRIS only comes together when people have the opportunity to go deep in their area rather than spreading thin across everything. The full flight in May 2025 was the product of that specialization, with each subsystem reflecting the focused work of the people who owned it. My role was to make sure those efforts stayed connected and that the system we were building was one that could actually fly, but the result was genuinely collaborative in a way that a more top-down approach would not have produced.

![](/assets/images/irishsat/launch.png)


https://ndirishsat.com/projects/iris/

https://ndirishsat.com/leads-2024-2025/allen-uy/