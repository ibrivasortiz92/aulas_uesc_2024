# ANSYS (Computational Modeling)

## Workbench

### Workbench Options

* File:

  * Archive: `.wbpz`. Save project in a compact file.

  * Restore Archive: `.wbpz`. Load project.

### Analysis Systems

* Steady - State Thermal: 

  * Engineering Data: `Engineering Data` Editor.

  * Geometry:

    * New Geometry: `DesignModeler` | `SpaceClaim` Geometry Engines

    * Analysis Type: `2D` | `3D`. Domain and mathematical model.

  * Model: `ANSYS Mechanical` Engine

<br>


## SpaceClaim

* SpaceClaim Options (File + SpaceClaim Options)

  * Units:

    * Length: `Meters`

### Create Geometry

* Set Grid Plane (`Select New Sketch Plane`)

* Create Sketch

  * `Space Bar`: Freeze sketch to set dimensions.

  * `Tab`: Switch between dimensions.

* Geometry to 3D (`3D Mode` Tool).

<br>


## ANSYS Mechanical

### Geometry (Domain)

* Material:

  * Assignment: Material (Engineering Data)

### Mesh

* Statistics: Nodes | Elements count.

* Order of Approximation: Mesh -> Defaults -> Element Order

### Create Mesh

* `Mesh` + `Update`: Generate default mesh.

* Mesh Control:

  * Method:

    * `MultiZone` (Fill with hexahedrons)

  * Face Meshing:

    * Geometry: Face | Volume Selector

    * `Update` Mesh.

  * Sizing:

    * Geometry: Line | Face | Volume Selector.

    * Element Size: `0.25`

    * Behavior: `Soft` | `Hard`. Soft / Hard Constraints.

#### Mesh Properties:

* Advanced Size Function: `Adaptive`

* Mesh Metric: 

  * Skewness: `0:1`. Less values best. Good element: < 0.5

### Mesh Tools

* Section Plane: Check interior mesh.

  * Edit: Move section plane.

  * Hole element: Show entire elements.

* `Update` Mesh.

### Define Boundary Conditions

* `Steady - State Thermal`: 

  * Temperature:

    * Magnitude: Temperature value

  * Convection:

    * Film Coefficient: $h$

    * Ambient Temperature: $T_\infty$
  
  * Radiation 

  * Heat (default: 0)

* `Static Structural`:

  * Supports:

    * Fixed Support: Set to 0 the displacements.

  * Loads:

    * Force: 

### Define Internal Source

* `Steady - State Thermal`:

  * Internal Heat Generation

### Define Material

* Geometry (Geometry Object)

  * Material: Select the material

### Run Simulation

* `Solve`

### Post - Processing

* `Steady - State Thermal`: 

  * Thermal:

    * Temperature: 

    * Total Heat Flux

  * Reaction: (For energy conservation)

* `Static Structural (A5)`:

  * Deformation:

    * Total Deformation

  * Stress:

    * Normal Stress:

  * Probe:

    * Force Reaction: Fixed Support

#### Prove Specific Point Solution

* Create a coordinate system `Custom Coordinate`

* Solution + Probe:

  * Location Method: Coordinate System

  * Location: `Custom Coordinate`

* Right Click + `Evaluate All Results`

#### Solution Along Line

* Model + Construction Geometry + Path

* Set Start and End coordinates

* Set Number of Sampling Points

* Display Option: 

  * Unaveraged: Display the heat flux for each element

* Create Solution object on line

#### Create Image File

* Image to File

* View Settings to modifier image rulers.

<br>


## Engineering Data Editor

### Create new material

* Add new row in material table.

### Thermal Analysis

* Thermal: 

  * `Isotropic Thermal Conductivity`: $k$

### Structural Analysis

* Linear Elasticity:

  * Isotropic Elasticity:

    * Young Modulus: [Psi, Pa]

    * Poisson's Ratio

<br>
