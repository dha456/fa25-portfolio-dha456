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

## MAE 3780 Robot Competition Final Report

**Group 50:** Davis Adams (dha45), Reggie Harris (rdh252), Ryan Xie (rsx3)

### Robot Design & Strategy Overview
Our robot was designed around a clear objective: to maximize reliable cube collection while remaining mechanically robust under competition conditions. Since cubes only needed to finish within the robot's perimeter to score, we prioritized passive collection area over active intake mechanisms. This led to a wide-open front chassis that allowed cubes to pass underneath the robot as it drove forward. The final design emphasized durability and reliability rather than mechanical complexity. The robot used 3.5-inch lab wheels to provide enough ground clearance for cubes to pass underneath the chassis while still fitting securely on the provided motor shafts. A wide front opening and added chassis weight improved cube collection, traction, and stability during contact-heavy gameplay. The outer shell served as both the legal scoring perimeter and a protective structure for the electronics and sensors.

> Electrically, the robot used the Arduino UNO, two L9110H H-bridges, the provided servos, and two QTI sensors for border detection. The color sensor was repurposed for consistent lighting rather than navigation. The autonomous strategy: rush the center cube line on match start, then sweep the field using QTI border detection to remain within the arena.

### Design Process Reflection
The robot went through several major design iterations before reaching its final form. Early designs included servo-actuated front flaps to funnel cubes inward. Those moving parts increased software complexity and introduced failure modes, so we replaced them with fixed, rigid flaps. On competition day the rigid flaps exceeded the legal perimeter and were removed; testing showed the wide opening and wheel clearance still provided effective passive collection.

Wheel selection and traction were major tradeoffs. We briefly evaluated 5-inch McMaster wheels for extra clearance but found them difficult to mount and unnecessary; the 3.5-inch lab wheels provided the best balance of clearance, stability, and mounting reliability. We experimented with adding chassis weight to improve contact performance and considered series-batteries to increase motor power, but ultimately avoided electrical configurations that risked damaging servos or H-bridges.

Milestone testing drove important pivots in sensing. During Milestone 3 color sensing proved unreliable due to lighting, reflections, and sensor height sensitivity. We simplified the control strategy to rely primarily on QTI border detection and used the color sensor LEDs as a controlled light source to stabilize QTI readings.

### Competition Analysis
On competition day the robot's strengths were durability, consistency, and its ability to handle contact without losing control. The opening autonomous routine collected many cubes quickly and the sweeping pattern with QTI border detection generally kept the robot inside the field and collecting. The principal weakness was cube retention: the open chassis allowed cubes to slide out during sharp turns or collisions, and the robot sometimes spent time pushing opponents instead of returning to collection.

### Conclusions and Future Work
Primary improvements for a next iteration:
- Add passive retention (angled rails, internal walls) to reduce cube loss during turns and impacts
- Refine turning behavior and state machine to disengage from pushing scenarios faster
- Consider gear ratio changes for more torque and traction while balancing wheel speed

Testing under realistic conditions was crucial—many promising ideas were abandoned after field testing, especially those relying on color sensing. The overall lesson: favor simplicity that improves reliability, but be willing to add well-justified complexity where it measurably improves performance.

---

### Appendix A: Bill of Materials (BOM)
Only purchased or sourced parts beyond the lab kit are included.

| Item | Description | Qty | Unit Cost ($) | Total Cost ($) | Vendor/Source | Used in Final Design |
|------|-------------:|:---:|--------------:|---------------:|:-------------|:--------------------:|
| Rubber Wheels | 5" diameter soft rubber (2243T23) | 2 | 9.30 | 18.60 | McMaster | N |
| Wheels | Larger lab-supply wheels | 2 | 2.00 | 4.00 | MAE Lab | Y |
| Weight | 2.5 kg calibration weight | 1 | 10.00 | 10.00 | Home estimate | Y |
| Scrap Wood Plank | 5x5x1/4 for laser cutting | 1 | 1.00 | 1.00 | RPL scrap | Y |

**Total Cost:** $33.60 / $40

---

### Appendix B: Circuit Diagram
![Circuit Diagram]({{ "/assets/images/circuit-diagram.png" | relative_url }})

### Appendix C: CAD Files & Drawings
- Laser-cut mounting plate for servos, breadboard, and sensors
- Outer side panels forming the scoring perimeter
- Angled inner deflectors near the front opening
- Wide-open front mouth with no active intake

![CAD Angle 1]({{ "/assets/images/cad-angle1.png" | relative_url }})
![CAD Angle 2]({{ "/assets/images/cad-angle2.png" | relative_url }})

### Appendix D: Flowchart
Start → Initialize serial, motors, QTI inputs → If gameOpening: run opening sequence (drive forward 3s, turn) → Else: read QTI sensors → If border detected: run corner escape or sweep turn → Else: drive forward → repeat

### Appendix E: Code (excerpt)
```c
// key control functions (excerpt)
void drive_forward();
void drive_backward();
void turn_left();
void turn_right();
void stop();
int checkBlack();
void escapeCorner();
void doSweepTurn();
```

### Photos and Supporting Media
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

---

#### Notes
- I preserved your original images and added the full final report text you provided. If you want me to rename the file, change the `title`, or adjust which images appear first, tell me which edits to make next.

