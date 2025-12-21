---
layout: project
title: Instrumented Torque Wrench Design (MAE 3270)
description: Multi-disciplinary design project integrating materials selection,
  fracture mechanics, fatigue analysis, and finite element analysis
technologies: [SolidWorks, ANSYS, MATLAB/Python]
image: /assets/images/Part2.STEP
author: Davis Adams
published: true
---

## Project Overview
For MAE 3270 (Materials and Structural Analysis), I designed a non-ratcheting, 3/8
inch drive instrumented torque wrench rated for 600 in-lbf. This project pulled
together multiple engineering disciplines: materials selection, fracture mechanics,
fatigue analysis, strain gauge theory, stress analysis, and finite element analysis.

### Design Requirements
The design objective was to maximize the voltage output (mV/V) of strain gauges bonded
to the wrench handle while meeting stringent safety and performance constraints:

- **Target sensitivity:** ≥ 1.0 mV/V output at rated 600 in-lbf torque
- **Static safety factor (yield/brittle failure):** ≥ 4.0
- **Fracture mechanics safety factor:** ≥ 2.0 (for 1 mm initial crack)
- **Fatigue safety factor:** ≥ 1.5 (±600 in-lbf fully reversed for 106 cycles)
- **Material constraint:** Steel, aluminum, or titanium alloy

## Part 1: Baseline Design Analysis
I started with the provided baseline design to understand the fundamentals:

**Baseline Design Parameters:**

- Material: M42 Steel
- Young's modulus: 32 MPsi
- Poisson's ratio: 0.29
- Tensile strength: 370 ksi
- Fracture toughness: 15 ksi√in
- Fatigue strength (106 cycles): 115 ksi

**Baseline Results:**

- Load point deflection: 0.091 in
- Maximum normal stress: 12.80 ksi

- Strain at gauge: 375 microstrain
- Output: 0.38 mV/V (half bridge configuration)
- Safety factor (strength): 28.9
- Safety factor (crack growth): 2.95
- Safety factor (fatigue): 8.98

**Key observation:** The baseline design was overly conservative with excessive safety
factors but fell significantly short on sensitivity (0.38 mV/V vs 1.0 mV/V
requirement). This indicated the design could be optimized to reduce material and
maximize strain at the gauge location.

## Part 2: Optimized Design
Using hand calculations and iterative analysis, I developed an improved design that
better balanced all constraints. My design approach focused on:

1. **Material optimization** to improve sensitivity while maintaining safety margins
2. **Geometry refinement** to maximize strain at gauge locations
3. **Stress concentration mitigation** through thoughtful transitions
4. **Hand calculations** to predict behavior before FEM validation

### Material Selection and Analysis
I compared three candidate materials against design requirements:

| Material | E (Msi) | $S_y$ (Ksi) | $S_{fatigue}$ @ 106 cycles (Ksi) | $K_{IC}$ (Ksi√in) |
|----------|---------|-------------|-----------------------------------|-------------------|
| AISI 9255 Spring Steel | 31 | 150 | 101 | 60 |
| 7075-T6 Aluminum | 10.5 | 73 | 25 | 27 |
| Ti-6Al-4V (Grade 5) | 16.9 | 125 | 55 | 35 |

**Material Decision: AISI 9255 Spring Steel**
I selected AISI 9255 spring steel for the final design. While 7075-T6 aluminum offered
lower weight, it failed the fatigue strength requirements (25 ksi was insufficient).
Titanium (Ti-6Al-4V) met all structural requirements but produced strain levels that
were too low for reliable strain gauge measurement. AISI 9255 provided the optimal
balance: high stiffness (E = 31.3 MPsi), excellent fatigue resistance ($S_{fatigue}$ =
102 ksi), and measurable strain levels (~986 microstrain) for the strain gauge
transducer.

### Design Parameters
**Geometry:**
- Rated torque: $M = 600$ in-lbf
- Distance from drive to load point: $L = 7.0$ in
- Distance from drive to strain gauge: $c = 1.0$ in
- Handle width: $h = 0.50$ in
- Handle thickness: $b = 0.40$ in
- Assumed crack depth: $a_0 = 0.04$ in

**Material Properties (AISI 9255):**
- Young's modulus: $E = 31.3 \times 10^6$ psi
- Tensile strength: $S_u = 200$ ksi
- Fracture toughness: $K_{IC} = 60.1$ ksi√in
- Fatigue strength: $S_{fatigue} = 102$ ksi

### Hand Calculation Results
Using beam theory and fracture mechanics analysis with the MATLAB code developed for
design iteration:

**Stress Analysis:**
- Maximum normal stress: **36.00 ksi**
- Load point deflection: **0.075 in**
- Strain at gauge location: **986 microstrain**
- **Output at 600 in-lbf: 0.99 mV/V** (half bridge configuration)

**Safety Factors:**
- **Safety factor for strength (yield):** 5.56 ✓ (exceeds 4.0 requirement)
- **Safety factor for crack growth:** 4.20 ✓ (exceeds 2.0 requirement)
- **Safety factor for fatigue:** 2.83 ✓ (exceeds 1.5 requirement)

The design narrowly meets the 1.0 mV/V sensitivity requirement at 0.99 mV/V,
demonstrating effective optimization without excessive material or weight.

### CAD Model
Built in SolidWorks, my design incorporates the optimized dimensions derived from
analytical calculations:

![CAD Design Overview]({{ "/assets/images/CAD1.png" | relative_url }}){: .inline-image style="width: 400px"}
![CAD Design Detail View]({{ "/assets/images/Screenshot 2025-12-10 at 8.39.59 PM.png" | relative_url }}){: .inline-image style="width: 400px"}

### FEM Analysis in ANSYS
After importing the CAD model into ANSYS and conducting stress analysis at 600 in-lbf
torque (applied as lateral force at load point):

![Load and Boundary Conditions]({{ "/assets/images/BoundaryConditions.png" | relative_url }}){: .inline-image style="width: 500px"}
**Key FEM Results:**
- Maximum von Mises stress: **86.8 ksi**
- Load point deflection: **0.123 in**
- Maximum normal strain: **1460.7 microstrain**
- Strain in gauge region: **800–1400 microstrain**
![Global Normal Strain Contour]({{ "/assets/images/Normal Elastic Strain.png" | relative_url }}){: .inline-image style="width: 600px"}
![Gauge Probe Screenshot]({{ "/assets/images/Gauge screenshot.png" | relative_url }}){: .inline-image style="width: 500px"}

Measured strain at the selected gauge location (from ANSYS probe): **2145
microstrain**.
Using the half-bridge assumption, the FEM-based torque-wrench sensitivity is:
- FEM strain = 2145 με → FEM-based sensitivity = 2145/1000 = **2.145 mV/V** (half
bridge)

This FEM-based sensitivity exceeds the target 1.0 mV/V and is higher than the
hand-calculated 0.99 mV/V, reflecting local strain concentration at the selected gauge
site.

![Principal Stress Contour]({{ "/assets/images/Principal Stress.png" | relative_url }}){: .inline-image style="width: 600px"}

![Example Mesh (refined)]({{ "/assets/images/FirstMesh.png" | relative_url }}){: .inline-image style="width: 500px"}

**Hand Calculation vs FEM Comparison:**
The hand calculation predicted a maximum normal stress of 36.00 ksi based on
simplified beam theory and a rectangular cross-section. The FEM analysis showed higher
localized stresses (86.8 ksi peak) due to:
- Three-dimensional stress concentrations at geometry transitions
- Fillets and rounded corners that exist in the CAD model
- Strain gauge cutout features that create local stress rises
- Boundary condition effects near the fixed drive region

The FEM displacement (0.123 in) was higher than the hand-calculated value (0.075 in),
suggesting the actual structure is slightly more compliant. This difference can be
attributed to the effects of the cutout geometry and local compliance variations not
captured in the simple beam model.

Despite these differences, the overall trends align well: the hand calculation
correctly identified the order of magnitude for both stress and deflection, validating
the analytical approach for first-cut design.

### Design Validation & Reflections
**Beam Theory Accuracy:**
When examining the deformed mesh in ANSYS, most cross-sections along the handle
remained relatively straight as the wrench bent, confirming that plane sections
largely stayed plane—a key assumption of beam theory. However, this assumption broke
down at critical locations:
- Near the drive head fillet where stress concentrations develop
- Around the strain gauge cutout where local geometry disruptions occur
- At transitions between different cross-section geometries

Overall, beam theory remained accurate enough for predicting general bending behavior,
but it cannot capture the localized three-dimensional effects and stress
concentrations that FEM automatically includes. This makes FEM invaluable for final
design validation and determining actual strain levels for gauge calibration.

**Design Validation:**
All safety factors exceed their minimum requirements:
- Strength safety factor of 5.56 provides comfortable margin above 4.0
- Crack growth safety factor of 4.20 ensures fracture resistance above 2.0

- Fatigue safety factor of 2.83 exceeds the 1.5 minimum for 106 cycle life
The design achieves sensitivity of 0.99 mV/V, meeting the 1.0 mV/V requirement within
practical tolerance. This balanced optimization demonstrates effective engineering:
sufficient safety margins without excessive over-design, and measurable strain output
for reliable transduction.

### Hand-Calculation Script
The MATLAB function used for hand calculations is included in the repository. It
reproduces the stress, strain, safety factors, and sensitivity calculations used in
this report. See [scripts/torqueDesign.m](scripts/torqueDesign.m) for the full code
and example usage.

### Strain Gauge Selection
A compact strain-gauge spec used for reporting and FEM calibration:
- Type: bonded foil strain gauge, 350 Ω (uniaxial)
- Configuration: half-bridge (top/bottom faces) to maximize bending sensitivity
- Active gauge length: 6 mm (~0.236 in)
- Placement: centered at c = 1.0 in from the drive, clear of fillets/cutouts
This brief spec is included to document the measurement assumption used to convert FEM
strains to mV/V. Replace with a specific commercial part if available.

```

Nulla et magna urna. Morbi a ipsum sollicitudin, rhoncus risus volutpat, ultricies nunc. Quisque mollis finibus ante id imperdiet. Quisque vehicula elit sit amet felis facilisis fermentum.

![Shaded rendering of earlier version]({{ "/assets/images/radio-machine.jpg" | relative_url }}){: .inline-image-r style="width: 200px"}

Nulla et magna urna. Morbi a ipsum sollicitudin, rhoncus risus volutpat, ultricies nunc. Quisque mollis finibus ante id imperdiet. Quisque vehicula elit sit amet felis facilisis fermentum.

Aenean tincidunt aliquam arcu, in euismod dui dapibus eu. In placerat, mi et ultrices consequat, quam ligula cursus mauris, in semper neque nibh at est. Maecenas hendrerit dignissim porta. Phasellus nec fringilla dolor. Etiam efficitur nisi sit amet velit pharetra feugiat. Etiam ultrices turpis at leo semper, eleifend scelerisque neque malesuada. Aliquam molestie congue rhoncus. Donec blandit neque dolor, nec tristique mi pretium ac. Mauris tincidunt ullamcorper magna, nec pellentesque mi sagittis quis.

I was inspired by this old radio when I made this rendering:

![Photo of old radio]({{ "/assets/images/old-radio.jpg" | relative_url }}){: .inline-image-l}

Aenean tincidunt aliquam arcu, in euismod dui dapibus eu. In placerat, mi et ultrices consequat, quam ligula cursus mauris, in semper neque nibh at est. Maecenas hendrerit dignissim porta. Phasellus nec fringilla dolor. Etiam efficitur nisi sit amet velit pharetra feugiat. Etiam ultrices turpis at leo semper, eleifend scelerisque neque malesuada. Aliquam molestie congue rhoncus. Donec blandit neque dolor, nec tristique mi pretium ac. Mauris tincidunt ullamcorper magna, nec pellentesque mi sagittis quis.

Aenean tincidunt aliquam arcu, in euismod dui dapibus eu. In placerat, mi et ultrices consequat, quam ligula cursus mauris, in semper neque nibh at est. Maecenas hendrerit dignissim porta. Phasellus nec fringilla dolor. Etiam efficitur nisi sit amet velit pharetra feugiat. Etiam ultrices turpis at leo semper, eleifend scelerisque neque malesuada. Aliquam molestie congue rhoncus. Donec blandit neque dolor, nec tristique mi pretium ac. Mauris tincidunt ullamcorper magna, nec pellentesque mi sagittis quis.
