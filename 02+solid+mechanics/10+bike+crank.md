# Bike Crank

3D structural mechanics problem

Consider a crank mounted on a bicycle. When a rider is pedaling the bicycle, he is applying a variable force to this bike crank. To simplify the analysis, we'll neglect the variation of the force with time and focus on the response of the crank to a static force.

**Specifications**

* Left three hole surfaces are fixed and a load of $100$ lbf is applied on the right hole surface in the upward direction.

**Calculate**:

* Deformed shape and displacement field

* Stress distribution in the crank.

<br>

## Pre - Analysis

### Governing Equations

* **3**: 3D Equilibrium Equations

* **6**: 3D Hooke's law.

* **6**: Strain-Displacement Relations.

### Boundary Conditions

* Traction: Natural Boundary Condition

* Displacements: Essential Boundary Condition.

### Hand Calculations

Euler-Bernoulli Beam Theory

E-B beam theory: For constant cross-section:

$$-\sigma_x = \frac{M y}{I}$$

* $M$: Moment.

* $y$: Distant from the neutral axis.

* $I$: Moment of Inertia.

E-B beam theory can extended to varyng cross-section if rate of variation is "small"

$$-\sigma_x = \frac{M y(x)}{I(x)}$$

**Result**: 

* At mid-bottom: $\sigma_x = 14.300 \quad psi$

* At mid-top: $\sigma_x = -14.300 \quad psi$

<br>


## ANSYS Analysis

Static Structural

<br>


## Geometry

Geometry File: `crankGeometry.x_t`

Project (including geometry): `crankInitial.wbpz`

<br>


## Mesh

* Sizing method with 0.2 inch size on average (Soft).

* Multizone mesh method.

### Refine Mesh Locally

* Sizing method with 0.1 (Soft) inch size on hole surfaces.

* Check interior mesh using section plane.

### Review Mesh Quality

* Check skewness mesh metric.

<br>


## Model Setup

* Assign material: aluminum 6061-T6 alloy

  * Young's modulus: $1 \times 10^7 \quad psi$. 
  
  * Poisson's Ratio: $0.33$

* Set boundary conditions:

  * Fixed support in holes

  * Set force load to $100 \quad lbf$ along $y$.

<br>


## Numerical Results

* Calculate total deformation and compare with the Undeformed WireFrame (auto scale and true scale).

* Calculate normal stress along x axis (Undeformed Model). Make an image file

* Create a line at the middle of the domain along y axis and plot normal stress along the line.

<br>


## Verification and Validation

* Check boundary condition and traction are satisfied:

  * Zero displacement at the holes.

  * Zero traction at the free surfaces.

  * External force divided by the area equals the traction.

* Check equilibrium satisfied (Reaction Balance)

  * Force reaction at the fixed holes to be -100 lbf

### Mesh Independence

* Refine the mesh and verify the results.

<br>

