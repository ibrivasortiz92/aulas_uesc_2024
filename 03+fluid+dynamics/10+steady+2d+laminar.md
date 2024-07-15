# Steady Two Dimensional Laminar Flow

Consider fluid flowing through a circular pipe of constant radius. The pipe diameter $D = 0.2$ $m$ and length $L = 3$ $m$. Consider the inlet velocity to be constant over the cross-section and equal to $1$ $m/s$. The pressure at the pipe outlet is $1$ $atm$. Take density $\rho = 1$ $kg/m^3$ and coefficient of viscosity $\mu = 2 \times 10^{-3}$ $kg/(m*s)$.

The fluid flow is laminar for pipe flow

$$Re_D = \frac{\rho \bar{v} D}{\mu} = 100 < 2300$$

Assumption: Incompressible Steady - State Axisymmetric Two Dimensional problem.

<br>


## Pre - Analysis

### Hand Calculations

Length at fully developed flow:

$$\frac{L_e}{D} \approx 0.06 Re_D$$

Parabolic velocity profile in the fully developed region:

$$\frac{v_z}{\bar{v}} = 2\left[ 1 - \left( \frac{r}{R} \right)^2 \right]$$

<br>


## Numerical Solution

Analysis System: Fluid Flow (Fluent)

### TODO: Create Geometry

* Geometry -> Properties -> Analysis Type: 2D 

* Geometry -> SpaceClaim:

  * File -> SpaceClaim Options -> Units -> Length: Meters

  * Select sketch plane: XY

  * Set plane view

  * Rectangle -> Draw Rectangle (0.1 m height, 3 m length)

  * Zoom -> Extends

  * 3D Mode (To create the surface)

### TODO: Create Mesh

* Model:

  * Mesh -> Mesh Control:

    * Sizing:

      * Geometry: Edge Selection (Begin and End Edges)
    
      * Type: Number of Divisions (10)

      * Behavior: Hard

    * Sizing:

      * Geometry: Edge Selection (Top and Bottom Edges)
    
      * Type: Number of Divisions (100)

      * Behavior: Hard

    * Face Meshing:

      * Geometry: Face Selection (Rectangle Domain)

    * Property (Use Adaptive Sizing): Yes

    * Update Mesh

  * Geometry: Surface

    * Property (Details -> Material -> Fluid/Solid -> Defined by Geometry): Fluid.

### TODO: Label Boundary Conditions

* Mesh

  * Edge Selection (Left Click + Create Named Selection)

    * inlet

    * outlet

    * pipe_wall

    * center_line

  * Face Selection (Left Click + Create Named Selection)

    * flow_domain

### Fluent Solver

* Setup: Enable Double Precision

  * General: Check Mesh

### TODO: Set Governing Equations

* Setup:

  * General:

    * 2D Space: Axisymmetric

  * Models:

    * Viscous: Laminar

  * Materials:

    * Fluid: (Right Click + New):

      * Name: mat1

      * Density: 1

      * Viscosity: 2e-3
  
  * Cell Zone Conditions:

    * fluid_domain (fluid):

      * Material Name: mat1

### TODO: Set Boundary Conditions

Absolute Pressure = Gauge Pressure + Reference Pressure

* Boundary Conditions:

  * fluid_domain (Operating Conditions):

    * Operating Pressure (Reference Pressure): 101325 pascal

  * inlet:

    * Type: velocity-inlet

    * Edit: 

      * Velocity Specification Method: Components

      * Axial Velocity: 1

      * Radial Velocity: 0

  * outlet:

    * Type: pressure-outlet

    * Edit: 

      * Gauge Pressure: 0

  * pipe_wall:

    * Type: wall

    * Edit: 

      * Shear Condition: No Slip

  * center_line:

    * Type: axis

### TODO: Run Calculations

* Solution: 

  * Monitors:

    * Residuals -> Edit:

      * Tolerance: 1e-6

  * Solution Initialization:

    * Check Standard Initialization

    * Gauge Pressure: 0

    * Axial Velocity: 1

    * Radial Velocity: 0

    * Initialize

* Results:

  * Graphics -> Contours:

    * Contours of: Velocity | Axial Velocity

    * Options: Disable Node Values

    * Display

### TODO: One Iteration

* Run Calculation:

  * Number of Iterations: 1

  * Calculate

* Graphics -> Contours:

    * Contours of: Velocity | Axial Velocity

    * Options: Disable Node Values

    * Display

* Graphics -> Contours:

    * Contours of: Residuals | Mass Imbalance

    * Options: Disable Node Values

    * Display

### TODO: Run Calculations

* Run Calculation:

  * Number of Iterations: 1000

  * Calculate

<br>


## Results

* Graphics -> Contours:

  * Contours of: Residuals | Mass Imbalance

  * Options: Disable Node Values

  * Display

* Graphics -> Contours:

  * Contours of: Velocity | Axial Velocity

  * Options: Disable Node Values

  * Display

<br>


## Post Processing

* Contours (Name velocity magnitude)

  * Locations: Periodic 1

  * Variable: Velocity

* Contours (Name pressure contours)

  * Locations: Periodic 1

  * Variable Pressure

* Vector (Name: Velocity Vectors)

  * Locations: axial location 1 | axial location 2

  * Variable: Velocity

  * Symbol: Arrow 3D

    * Symbol Size: 0.5

* Create Location: Line (axial location 1)

  * Point 1: 0.2 0 0

  * Point 2: 0.2 0 0

* Create Location: Line (axial location 2)

  * Point 1: 0.4 0 0

  * Point 2: 0.4 0 0

<br>