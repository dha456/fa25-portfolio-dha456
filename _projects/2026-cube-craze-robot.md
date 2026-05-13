---
layout: project
title: MAE 3780 Cube Craze Robot Competition
description: Robot design and competition report for the Cube Craze autonomous robot game in MAE 3780/3783.
technologies: [Arduino C, L9110H, QTI sensors, autonomous navigation, mechanical design]
image: /assets/images/mae3780-cube-craze-cover.svg
imagealt: Cube Craze robot cover image
author: Davis Adams
published: true
---

## Project Overview
This MAE 3780/3783 robot competition project documents the design, testing, and competition performance for our Cube Craze robot. The robot was built to collect as many cubes as possible inside its legal perimeter while remaining mechanically robust and reliable under contact-heavy competition conditions.

## Robot Design & Strategy
The design prioritized passive cube collection rather than a complex intake system. A wide front opening allowed cubes to move underneath the robot as it drove forward. A heavier chassis and 3.5-inch lab wheels improved traction and stability so the robot could push through cube piles and collisions.

Key features:
- Wide front mouth for passive cube collection
- Rigid perimeter walls that define the scoring area and protect electronics
- 3.5-inch lab wheels selected for the best balance of clearance, stability, and mount reliability
- Arduino UNO and two L9110H H-bridges for motor control
- Two QTI sensors for border detection
- Repurposed color sensor LEDs to stabilize QTI lighting

## Design Process Reflection
Early iterations included servo-actuated front flaps that could expand to funnel cubes inward. Those moving parts were removed because they added complexity and risk without improving reliability.

During testing, we discovered the color sensor readings were inconsistent due to lighting, reflections, field glossiness, and sensor height. We simplified the navigation strategy to rely mainly on QTI border detection while using the color sensor LEDs only as a stable light source.

The final design favored durability and consistency. That meant fewer fragile mechanisms and more focus on staying operational through collisions and field congestion.

## Competition Analysis
Strengths:
- Durable layout that survived collisions and heavy contact
- Consistent cube collection from a simple opening-based strategy
- Strong border containment using QTI sensors and sweep navigation

Weaknesses:
- Cube retention was limited because the robot did not actively hold cubes once collected
- Sharp turns and contact with other robots sometimes caused cubes to fall out
- The robot occasionally spent too much time pushing opponents instead of continuing to collect cubes

## Conclusions
For a future iteration, the best improvements would be:
- Adding passive cube retention elements such as angled rails or internal walls
- Refining turning behavior to better exit obstructed situations
- Exploring a gear ratio tradeoff for higher torque and traction

The main takeaway: simplicity improved reliability, but the robot still needed carefully chosen complexity where it truly added performance.

## Bill of Materials (BOM)
Only purchased or sourced parts beyond the lab kit are included below.

| Item | Description | Qty | Unit Cost ($) | Total Cost ($) | Source | Used in Final Design |
|------|-------------|-----|---------------|----------------|--------|----------------------|
| Rubber Wheels | 5" diameter soft rubber | 2 | 9.30 | 18.60 | McMaster | N |
| Wheels | Larger lab-supply wheels | 2 | 2.00 | 4.00 | MAE Lab | Y |
| Weight | 2.5 kg scale calibration weight | 1 | 10.00 | 10.00 | Home estimate | Y |
| Scrap Wood Plank | 5x5x1/4 scrap wood for laser cutting | 1 | 1.00 | 1.00 | RPL scrap estimate | Y |

**Total Cost:** $33.60 / $40

## Circuit Diagram
![Circuit Diagram]({{ "/assets/images/circuit-diagram.png" | relative_url }})

## CAD, Drawings, and Flowchart
The design included:
- A laser-cut wooden mounting plate for servos, breadboard, and sensors
- Outer perimeter walls that extend down to the ground for legal scoring shape
- Angled inner deflectors near the front opening to guide cubes into the collection zone
- A wide-open front mouth with no active intake mechanism

### CAD Angle 1
![CAD Angle 1]({{ "/assets/images/cad-angle1.png" | relative_url }})

### CAD Angle 2
![CAD Angle 2]({{ "/assets/images/cad-angle2.png" | relative_url }})

### Control Flow
1. Initialize serial, motors, and QTI inputs
2. Run opening sequence to push toward the center
3. Enter sweep mode using QTI border detection
4. When a border is detected, reverse and turn to the next lane
5. Continue sweeping until the match ends

## Photos and Supporting Media
<div class="project-gallery">
  <div class="gallery-item">
    <img src="/assets/images/robot-side-view.jpg" alt="Side view of assembled robot">
    <p>Side view of the assembled robot on workbench</p>
  </div>
  <div class="gallery-item">
    <img src="/assets/images/robot-wheels-closeup.jpg" alt="Close-up of 3.5-inch lab wheels">
    <p>Close-up of the 3.5-inch lab wheels on modified servos</p>
  </div>
  <div class="gallery-item">
    <img src="/assets/images/wheel-comparison.jpg" alt="Wheel comparison">
    <p>Comparison of 5-inch McMaster wheels (unused) vs. 3.5-inch lab wheels</p>
  </div>
  <div class="gallery-item">
    <img src="/assets/images/robot-underside.jpg" alt="Underside view">
    <p>Underside showing angled deflectors and open chassis</p>
  </div>
  <div class="gallery-item">
    <img src="/assets/images/laser-cutter.jpg" alt="Laser cutter in action">
    <p>Laser cutter cutting the wooden chassis pieces</p>
  </div>
  <div class="gallery-item">
    <img src="/assets/images/electronics-top.jpg" alt="Electronics top view">
    <p>Top view of Arduino, H-bridges, and QTI sensors</p>
  </div>
  <div class="gallery-item">
    <img src="/assets/images/robot-front-view.jpg" alt="Front view of robot">
    <p>Front view showing wide mouth, sensors, and protective shell</p>
  </div>
  <div class="gallery-item">
    <img src="/assets/images/robot-on-field.jpg" alt="Robot on competition field">
    <p>Robot positioned on the Cube Craze competition field</p>
  </div>
</div>
