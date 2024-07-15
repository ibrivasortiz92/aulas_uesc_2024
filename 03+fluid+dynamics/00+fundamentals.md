# Fluid Dynamics

## 1. Frame of Reference

The `Eulerian` frame is fixed in space, observing the flow properties at different points, while the `Lagrangian` frame moves with the object, tracking its individual motion.

### Eulerian Frame of Reference

* In the Eulerian frame, the observer remains stationary at a fixed point in space, while the fluid or object of interest flows or moves past that point.

* Instead of tracking the motion of individual particles, the Eulerian approach focuses on observing the flow properties at each point in space over time.


### Lagrangian Frame of Reference

* In the Lagrangian frame, the observer moves with the fluid or object of interest, following its motion through space.

* This approach tracks the motion of individual particles or objects as they move through space and time.
- It is useful for studying the trajectory and behavior of specific particles or objects, such as in particle physics or analyzing the motion of objects in a fluid.

<br>


## 2. Derivation of the Continuity Equation

The conservation of mass states that the fluid mass cannot change. So, the rate of change of mass within the control volume is equivalent to the mass flux across the surface $S$ of the control volume $V$.

$$\frac{d}{dt} \int_V{\rho dV} = - \int_S{(\rho \mathbf{v}) \cdot \mathbf{n} dS} \tag{2.1}$$

where $\mathbf{n}$ is the unit normal vector. We can apply Gauss's divergence theorem that equates the volume integral of a divergence of a vector into a area integral over the surface that defines the volume. This is stated as

$$\int_V \nabla \cdot (\rho \mathbf{v}) dV = \int_S (\rho \mathbf{v}) \cdot \mathbf{n} dS \tag{2.2}$$

Using the above theorem, the surface integral in Eq. (2.1) may be replaced by a volume integral, hence, the equation becomes

$$ \int_V \left[ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) \right] dV = 0 \tag{2.3}$$

Since Eq. (2.3) is valid for any arbitrary volume $V$, the implication is that

$$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0\tag{2.4} $$

Eq. (2.4) is known as the continuity equation because it requires no assumptions except that the density and velocity are continuum functions. That is, the flow may be either `steady` or `unsteady`, `viscous` or `frictionless`, `compressible` or `incompressible`.

### Steady Compressible Flow

If the flow is steady and all properties are functions of position only, Eq. (2.4) reduces to

$$ \nabla \cdot (\rho \mathbf{v}) = 0 \tag{2.5} $$

### Incompressible Flow

A special case that affords great simplification is `incompressible` flow, where the density changes are negligible. Then $\partial \rho / \partial t \approx 0$ regardless of whether the flow is steady or unsteady, and the density can be slipped out of the divergence in Eq. (2.5) and divided out. The result

$$ \nabla \cdot \mathbf{v} = 0 \tag{2.6} $$

is valid for steady or unsteady incompressible flow. Most practical engineering flows are approximately incompressible, the chief exception are high-speed gas flows.

An explicit criterion for incompressible flow is

$$Ma^2 = \frac{v^2}{a^2} \ll 1 \tag{2.7}$$

where $Ma = v / a$ is the dimensionless `Mach number` of the flow, and $a$ is the speed of sound of the fluid. The commonly accepted limit is $Ma \le 0.3$. For air at standard conditions, a flow can thus be considered incompressible if the velocity is less than about 100 $m/s$. Further, is is clear that almost all liquid flows are incompressible, since flow velocities are small and the speed of sound is very large.

<br>


## 3. Derivation of the Momentum Equation

Newton's second law of motion states that the sum of forces, which is acting on a fluid element, equals to the product between its mass and acceleration of the element.

$$m \mathbf{a} = \sum \mathbf{F}  \tag{3.1}$$

### 3.1 Acceleration Term

The acceleration vector $\mathbf{a}$ of the flow is computed through the total derivative of the velocity vector

$$\mathbf{a} = \frac{d \mathbf{v}}{dt} = \mathbf{i} \frac{du}{dt} + \mathbf{j} \frac{dv}{dt} + \mathbf{k} \frac{dw}{dt} \tag{3.2}$$

Since each scalar component is a function of the four variables ($x, y, z, t$), we use the chain rule to obtain each scalar time derivative.

$$\frac{du}{dt} = \frac{\partial u}{\partial t} + \frac{\partial u}{\partial x} \frac{dx}{dt} + \frac{\partial u}{\partial y} \frac{dy}{dt} + \frac{\partial u}{\partial z} \frac{dz}{dt} \tag{3.3}$$

where $\frac{dx}{dt} = u$, $\frac{dy}{dt} = v$, and $\frac{dz}{dt} = w$ are the local velocity components. Then, the acceleration components can be expressed as

$$a_x = \frac{du}{dt} = \frac{\partial u}{\partial t} + u \frac{\partial u}{\partial x} + v \frac{\partial u}{\partial y} + w \frac{\partial u}{\partial z} = \frac{\partial u}{\partial t} + \left( \mathbf{v} \cdot \nabla \right) u $$

$$a_y = \frac{dv}{dt} = \frac{\partial v}{\partial t} + u \frac{\partial v}{\partial x} + v \frac{\partial v}{\partial y} + w \frac{\partial v}{\partial z} = \frac{\partial v}{\partial t} + \left( \mathbf{v} \cdot \nabla \right) v $$

$$a_z = \frac{dw}{dt} = \frac{\partial w}{\partial t} + u \frac{\partial w}{\partial x} + v \frac{\partial w}{\partial y} + w \frac{\partial w}{\partial z} = \frac{\partial w}{\partial t} + \left( \mathbf{v} \cdot \nabla \right) w $$

$$\mathbf{a} = \frac{d \mathbf{v}}{dt} = \frac{\partial \mathbf{v}}{\partial t} + \left( u \frac{\partial \mathbf{v}}{\partial x} + v \frac{\partial \mathbf{v}}{\partial y} + w \frac{\partial \mathbf{v}}{\partial z} \right) = \frac{\partial \mathbf{v}}{\partial t} + \left( \mathbf{v} \cdot \nabla \right) \mathbf{v} \tag{3.4}$$

The term $\partial \mathbf{v} / \partial t$ is called the local acceleration, and the three terms in parentheses are called the `convective acceleration` which arises when particle moves through regions of spatially varying velocity.

### 3.2 Net Force

The forces acting on a fluid element are of two types: body forces (gravity, magnetism, electric potential) and surface forces due to stresses (hydrostatic pressure and viscous stresses).

$$\sum \mathbf{F} = \int_V{\mathbf{f} dV} + \int_S{\mathbf{\sigma} \cdot \mathbf{n} dS}  \tag{3.5}$$

where $\mathbf{f}$ are body forces, and $\mathbf{\sigma}$ represent surface stresses. Using Gauss's divergence theorem on Eq. (3.5) results in

$$\int_V{\rho \frac{d \mathbf{v}}{dt} dV} = \int_V{ \left( \nabla \cdot \mathbf{\sigma} + \mathbf{f} \right) dV} \tag{3.6}$$

so that

$$\rho \frac{d \mathbf{v}}{dt} = \nabla \cdot \mathbf{\sigma} + \mathbf{f} \tag{3.7}$$

### 3.3 Surface Forces

The surface forces are the sum of hydrostatic pressure plus viscous stresses that arise from motion with velocity gradients

$$\mathbf{\sigma} = - p + \mathbf{\tau} \tag{3.8}$$

where $\mathbf{\tau}$ is a tensor that represent the viscous stresses

$$ \mathbf{\tau} = 
\begin{bmatrix}
\tau_{xx} & \tau_{yx} & \tau_{zx} \\ 
\tau_{xy} & \tau_{yy} & \tau_{zy} \\ 
\tau_{xz} & \tau_{yz} & \tau_{zz} \\ 
\end{bmatrix} \tag{3.9}$$

Substituting Eq. (3.9) in (3.7), we obtain the general form of the momentum equation

$$\rho \frac{d \mathbf{v}}{dt} = -\nabla p + \nabla \cdot \mathbf{\tau} + \mathbf{f} \tag{3.10}$$

<br>


## 4. Navier - Stokes equations

For a `newtonian fluid`, the viscous stresses are proportional to the velocity rates. The Stokes formula is

$$\mathbf{\tau_{ij}} = \mathbf{\tau_{ji}} = \mu \left( \frac{\partial v_i}{\partial j} + \frac{\partial v_j}{\partial i}\right) - \left( \frac{2}{3} \mu - \kappa\right) \nabla \cdot \mathbf{v} \delta_{ij} \tag{4.1}$$

where $\mu$ is the dynamic viscosity and $\kappa$ is the volumetric viscosity, both are function of the pressure and temperature of the fluid. For `incompressible fluid`, $\nabla \cdot \mathbf{v} = 0$, the viscosity stresses can be reduced to 

$$\mathbf{\tau_{ij}} = \mu \left( \frac{\partial v_i}{\partial j} + \frac{\partial v_j}{\partial i}\right) \tag{4.2}$$

and, for `constant viscosity` coefficients, the divergence of the viscosity stresses can be written as

$$\nabla \cdot \mathbf{\tau} = \mu \nabla^2 \mathbf{v} \tag{4.3}$$

Substitution into Eq. (3.10) gives the differential momentum equation for a newtonian fluid with constant density and viscosity with is known as the Navier-Stokes equations

$$\rho \frac{d \mathbf{v}}{dt} = -\nabla p + \mu \nabla^2 \mathbf{v} + \mathbf{f} \tag{4.4}$$

<br>
