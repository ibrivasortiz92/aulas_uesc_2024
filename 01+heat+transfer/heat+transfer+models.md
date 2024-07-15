# Mathematical Model for Heat Transfer

## 1. Heat Conduction Governing Equation

Consider a small volume element in Cartesian coordinate having sides $dx$, $dy$, and &dz&. The energy balance for this little element is obtained from the first law of thermodynamics as

$$\begin{bmatrix} \text{Net Heat per} \\ \text{unit time (I)} \end{bmatrix} + \begin{bmatrix} \text{Internal Heat per} \\ \text{unit element (II)} \end{bmatrix} \\ = \begin{bmatrix} \text{Increase in internal} \\ \text{energy per unit time (III)} \end{bmatrix} + \begin{bmatrix} \text{Work done} \\ \text{ per unit time (IV)}  \end{bmatrix} \tag{1.1} $$

The last term of Eq. (1.1) is very small because the flow work done by solids due to temperature changes is negligible.

The rate of heat flowing into the element in x-direction is

$$Q_x = q_x \cdot dydz = -k_x \frac{\partial T}{\partial x} dy dz \tag{1.2}$$

and the rate of heat flowing out of the element in x-direction is

$$Q_{x+dx} = Q_x + \frac{\partial Q_x}{\partial x} dx = -k_x \frac{\partial T}{\partial x} dy dz - \frac{\partial}{\partial x} \left( k_x \frac{\partial T}{\partial x} dydz \right) dx \tag{1.3}$$

where $k_x$ is the `thermal conductivity` of the material in x-direction, and $\partial T / \partial x$ is the `temperature gradient` in x-direction. Then, the net rate of heat entering the element in x-direction is the difference between the entering and leaving heat flow rates

$$ Q_x - Q_{x+dx}  = \frac{\partial}{\partial x} \left( k_x \frac{\partial T}{\partial x} \right) dxdydz \tag{1.4}$$

So, the net heat conducted into the element $dxdydz$ per unit time, term `I` is

$$I = \left[ \frac{\partial}{\partial x} \left( k_x \frac{\partial T}{\partial x} \right) + \frac{\partial}{\partial y} \left( k_y \frac{\partial T}{\partial y} \right) + \frac{\partial}{\partial z} \left( k_z \frac{\partial T}{\partial z} \right) \right] dxdydz \tag{1.5}$$

The rate of energy generation in the element, term `II`, is

$$II = \dot{q} dxdydz \tag{1.6}$$

where $\dot{q}$ is the internal heat generation per unit time and per unit volume ($W/m^3$).

The heat energy is defined as

$$\text{heat energy} = c_p \rho T \tag{1.7}$$

where $c_p$ is the `specific heat` of the material, and $\rho$ is their `density`. So, the change in internal energy per unit time, term `III`, is

$$ III = \rho c_p \frac{\partial T}{\partial t} dxdydz \tag{1.8}$$

Substitution of Eqs. (1.5), (1.6), and (1.8) into (1.1) leads to the `general three-dimensional equation for heat conduction`

$$ \frac{\partial}{\partial x} \left( k_x \frac{\partial T}{\partial x} \right) + \frac{\partial}{\partial y} \left( k_y \frac{\partial T}{\partial y} \right) + \frac{\partial}{\partial z} \left( k_z \frac{\partial T}{\partial z} \right) + \dot{q} = \rho c_p \frac{\partial T}{\partial t} \tag{1.9} $$

Since for most engineering problems the materials can be considered isotropic for which $ k_x = k_y = k_z = k = \text{const} $, the general three-dimensional heat conduction equation becomes

$$\nabla^2T + \frac{\dot{q}}{k}  = \frac{1}{\alpha} \frac{\partial T}{\partial t} \tag{1.10} $$


where

$$ \nabla^2T= \frac{\partial^2 T}{\partial x^2} + \frac{\partial^2 T}{\partial y^2} + \frac{\partial^2 T}{\partial z^2} \tag{1.11} $$

is called the `Laplacian` of $T$. $\alpha = k / \rho c_p$ is known as the `thermal diffusivity` of the material ($m^2/s [L^2 / t]$). The physical significance of thermal diffusivity is that it tells us how fast heat is propagated or it diffuses through a material during changes of temperatures with time. The larger the thermal diffusivity, the faster the heat conduction.

<br>

## 2. Special Forms of the Heat Conduction Equation

### Steady state conditions

The temperature at any point in the material does not change with time. The heat conduction equation for this case becomes the `Poisson equation`

$$\nabla^2T + \frac{\dot{q}}{k}  = 0 \tag{2.1} $$

### No heat source

In the absence of any heat generation or release of energy within the body, the heat conduction equation becomes the `Diffusion equation`


$$\nabla^2T = \frac{1}{\alpha} \frac{\partial T}{\partial t} \tag{2.2}$$

if in addition, the process is in steady state, then the heat conduction equation becomes the `Laplace equation`

$$\nabla^2T = 0 \tag{2.3}$$

<br>

## 3. Initial and Boundary Conditions

The temperature distribution in a medium of given form and size can be determined by solving the heat conduction equation subject to given constraints, called the `initial` and `boundary` conditions of the problem.

### Initial Condition

The initial conditions describe the temperature distribution in a medium at the initial moment of time, and these are needed only for the time dependent (transient) problems. In general, these can be expressed as

$$t = 0 \quad T = T(x,y,z) \tag{3.1}$$

A simple but typical form of Eq. (3.1) ofr a uniform initial temperature distribution is

$$t = 0 \quad T = T_0 = const \tag{3.2}$$

### Boundary Condition

The boundary conditions specify the temperature or the heat flow at the surface of the body. Boundary conditions may be prescribed in a number of ways

**Prescribed surface temperature**: The temperature distribution `T_s` is given at a boundary surface for each moment of time

$$T_s = T(x,y,z,t) \tag{3.3}$$

**Prescribed heat flux**: The heat flux at a boundary is prescribed

$$-k \frac{\partial T}{\partial n} = q_s \tag{3.4}$$

`Isolated` or `adiabatic` boundary is set when $q_s = 0$.

**Convective condition**: The boundary surface is subjected to a convective heat transfer into a medium at the ambient temperature

<br>


