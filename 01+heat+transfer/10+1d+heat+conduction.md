# Steady One Dimensional Heat Conduction in a Bar

Find the temperature distribution along a bar.

|Specifications||
|--------------|---------------------------|
|One dimensional Cartesian geometry.||
|Steady state problem.||
|Length:|$3.0 m$|
|Left boundary condition:|$0.0 \degree C$|
|Right boundary condition:|$0.5 W/m^2$|
|Thermal conductivity:|$1.0 W / m \degree C$|
|Internal source:|$2.0 W / m^3$|

<br>


## Pre - Analysis

### Governing Equations

$$k \frac{d^2 T}{d x^2} + \dot{q} = 0$$

$$T(0) = T_0, \quad -k \frac{dT(x)}{dx} \Big|_L = q_L$$

where $k = 1.0 W / m \degree C$ $L = 3 m$, $\dot{q} = 2.0 W / m^3$, $T_0 = 0.0 \degree C$, and $q_L = 0.5 W/m^2$.

### Hand Calculations

The analytical solution has the form

$$T(x) = T_0 + \frac{1}{k} \left[ -\dot{q} \frac{x^2}{2} + \left(\dot{q}L - q_L \right) x \right]$$

* Temperature at $x = L$: $7.5 \degree C$

* Heat flux at $x = 0$: $5.5 W/m^2$

<br>


## Numerical Solution

Analysis System: Steady-State Thermal

### TODO: Create Geometry

* Geometry -> Properties -> Analysis Type: 2D 

* Geometry -> SpaceClaim:

  * File -> SpaceClaim Options -> Units -> Length: Meters

  * Select sketch plane: XY

  * Set plane view

  * Rectangle -> Draw Rectangle (1m height, 3m length)

### TODO: Create Mesh

* Model:

  * Mesh -> Mesh Control:

    * Face Meshing.

    * Sizing -> Element Size: 1 m

  * Mesh -> Sizing -> Using Adaptive Sizing: Yes.

### TODO: Set Linear Element Approximation

* Model -> Mesh -> Defaults -> Element Order: Linear

### TODO: Set Boundary Conditions

* Setup -> Steady State Thermal:

  * Temperature:

    * Geometry: Left edge

    * Temperature: 0

  * Heat Flux:

    * Geometry: Right edge

    * Heat: -0.5

### TODO: Set Material

* Engineering Data -> New Material: material0

  * Isotropic Thermal Conductivity: 1

* Setup -> Geometry -> Material -> material0

### TODO: Set Internal Source

* Setup -> Steady State Thermal -> Internal Heat Generation: 2

### TODO: Run Calculations

* Solution: Solve

### TODO: Temperature Distribution

* Solution -> Thermal -> Temperature

* Probe: 

  * Temperature at X = 0

  * Temperature at X = 3

### TODO: Heat Flux

* Solution -> Thermal -> Total Heat Flux

* Probe:

  * Total Heat Flux at X = 0

  * Total Heat Flux at X = 3

  * Result Selection: X axis

### TODO: Temperature and Heat Flux Plots Along Line

* Model -> Construction Geometry -> Path: line:

  * Number of Sampling Points: 49

  * Start: 0

  * End: 3

* Solution -> Thermal -> Temperature:

  * Scoping Method: Path

* Solution -> Thermal -> Total Heat Flux:

  *Scoping Method: Path

  * Display Option: Unaveraged

### TODO: Calculate Reaction

* Result: Solution -> Probe -> Reaction -> Temperature

  * Boundary Condition: Left Edge

<br>


## Verification & Validation

### Linear Approximation

|                    |Numerical Solution| Expected Solution |
|--------------------|:----------------:|:-----------------:|
|Temperature at X = 0|             $0.0$|              $0.0$|
|Temperature at X = 3|             $7.5$|              $7.5$|
|Heat Flux at X = 0  |            $-5.5$|             $-4.5$|
|Heat Flux at X = 3  |            $-0.5$|             $-0.5$|


### Quadratic Approximation

* Model -> Mesh -> Defaults -> Element Order: Quadratic

|                    |Numerical Solution| Expected Solution |
|--------------------|:----------------:|:-----------------:|
|Temperature at X = 0|             $0.0$|              $0.0$|
|Temperature at X = 3|             $7.5$|              $7.5$|
|Heat Flux at X = 0  |            $-5.5$|             $-5.5$|
|Heat Flux at X = 3  |            $-0.5$|             $-0.5$|

<br>
