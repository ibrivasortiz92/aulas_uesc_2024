# Finite Volume Method

* The computational domain is subdivided into a finite number of contiguous control volumes. 

* At the centroid of each of the control volumes, the variable values are calculated. 

* Interpolation is used to express variable values at the control volume face in terms of the centre values.

* Suitable quadrature formulae are applied to approximate the surface and volume integrals.

The cornerstone of the finite-volume method is the control volume integration. In a control volume, the bounding surface areas of the element are directly linked to the discretization of the first- and second-order derivatives for $\phi$ (the generic variable) through the Gauss's divergence theorem

$$\frac{1}{\Delta V} \int_V{\frac{\partial \phi}{\partial x} dV} = \frac{1}{\Delta V} \int_A{\phi dA^x} \approx \frac{1}{\Delta V} \sum_{i=1}^N \phi_i A_i^x$$

<br>


## 1. Diffusion Problems

Consider the steady state diffusion of a property $\phi$ in a one - dimensional domain. The process is governed by

$$\frac{d}{dx} D(x) \frac{d \phi(x)}{dx} + S(x) = 0 \tag{1.1}$$

where $D(x)$ is the diffusion coefficient and $S(x)$ is the interior source. The key step of the finite volume method is the integration of the governing equation over a control volume to yield a discretized equation at its nodal point

$$\int_{x_{i-1/2}}^{x_{i+1/2}} \frac{d}{dx} D(x) \frac{d \phi(x)}{dx} dx + \int_{x_{i-1/2}}^{x_{i+1/2}} S(x) dx = D(x) \frac{d \phi(x)}{dx} \Big|_{x_{i+1/2}} - D(x) \frac{d \phi(x)}{dx} \Big|_{x_{i-1/2}} + \bar{S} h = 0 \tag{1.2}$$

where we have defined the average interior source $\bar{S}$ as

$$\bar{S} = \frac{1}{h} \int_{x_{1-1/2}}^{x_i+1/2} S(x) dx \tag{1.3}$$

### Central Differencing Scheme

The values of the property $\phi$ and the diffusion coefficient are defined and evaluated at nodal points. To calculate gradients at the control volume faces an approximate distribution is used. In a uniform grid linearly interpolated values for the diffusion coefficients are given by

$$D(x_{i+1/2}) = D_{i + 1/2} = \frac{D_i + D_{i + 1}}{2} \tag{1.4a}$$

$$D(x_{i-1/2}) = D_{i - 1/2} = \frac{D_{i - 1} + D_i}{2} \tag{1.4b}$$

and the diffusive quantities are evaluated as

$$D(x)\frac{d \phi(x)}{dx} \Big|_{i+1/2} = D_{i+1/2} \left( \frac{\phi_{i+1} - \phi_i}{h} \right) \tag{1.5a}$$

$$D(x)\frac{d \phi(x)}{dx} \Big|_{i-1/2} = D_{i-1/2} \left( \frac{\phi_i - \phi_{i-1}}{h} \right) \tag{1.5b}$$

where $\phi_i = \phi(x_i)$. Substitution of Eq. (1.5), into Eq. (1.2) gives

$$- D_{i-1/2} \phi_{i-1} + \left( D_{i-1/2}+D_{i+1/2} \right) \phi_i - D_{i+1/2} \phi_{i+1} = \bar{S} h^2 \tag{1.6}$$

and, substituting Eq. (1.4) into (1.6) gives

$$- \left( D_{i - 1} + D_i \right) \phi_{i-1} + \left( D_{i - 1} + 2D_i + D_{i + 1} \right) \phi_i - \left( D_i + D_{i + 1} \right) \phi_{i+1} = 2 h^2 \bar{S} \tag{1.7}$$

### Boundary Conditions

The diffusion coefficient evaluated at the left and right boundary conditions are given by

$$D_{1/2} = D_1 \quad D_{I+1/2} = D_I \tag{1.8}$$


and the diffusive quantities are evaluated as

$$D(x)\frac{d \phi(x)}{dx} \Big|_{1/2} = D_1 \left( \frac{\phi_1 - \phi_{1/2}}{h/2} \right) \tag{1.9}$$

$$D(x)\frac{d \phi(x)}{dx} \Big|_{I+1/2} = D_{I} \left( \frac{\phi_{I+1/2} - \phi_I}{h/2} \right) \tag{1.10}$$

Substituting Eqs. (1.9) into Eq. (1.2) for the left boundary condition gives

$$ \left( 5D_1 + D_2 \right) \phi_1 - \left( D_1 + D_2 \right) \phi_2 = 2 \bar{S} h^2 + 4 D_1 \phi_{1/2} \tag{1.11}$$

and, substituting Eq. (1.10) into Eq. (1.2) for the right boundary condition gives

$$- \left( D_{I - 1} + D_I \right) \phi_{I-1} + \left( D_{I - 1} + 5 D_I \right) \phi_I  = 2 \bar{S} h^2 + 4 D_{I} \phi_{I+1/2} \tag{1.12}$$

### Summary

The discretized equations can be formulated as

$$a \phi_{i-1} + b \phi_i +c\phi_{i+1} = d \tag{1.13}$$


| |a|b|c|d|
|--|--|--|--|--|
|Interior node |$- \left( D_{i - 1} + D_i \right)$|$\left( D_{i - 1} + 2D_i + D_{i + 1} \right)$|$- \left( D_i + D_{i + 1} \right)$|$2 h^2 \bar{S}$|
|Left Boundary |$0$|$\left( 5D_1 + D_2 \right)$|$- \left( D_1 + D_2 \right)$|$2 \bar{S} h^2 + 4 D_1 \phi_{1/2}$|
|Right Boundary|$- \left( D_{I - 1} + D_I \right)$|$\left( D_{I - 1} + 5 D_I \right)$|$0$|$2 \bar{S} h^2 + 4 D_{I} \phi_{I+1/2}$|

<br>


## 2. Convection - Diffusion Problems

The steady convection and diffusion of a property $\phi$ in a given one - dimensional flow field $u$ and in the absence of interior sources is governed by

$$\frac{d}{dx} \rho(x) u(x) \phi(x) = \frac{d}{dx} D(x) \frac{d}{dx} \phi(x) \tag{2.1}$$

where the flow must satisfy the continuity equation

$$\frac{d}{dx} \rho(x) u(x) = 0 \tag{2.2}$$

Integration of transport equation, Eq. (2.1), over the control volume gives

$$\int_{x_{i-1/2}}^{x_i+1/2} \frac{d}{dx} \rho(x) u(x) \phi(x) dx = \int_{x_{i-1/2}}^{x_i+1/2} \frac{d}{dx} D(x) \frac{d}{dx} \phi(x) dx \tag{2.3a}$$

$$\rho(x) u(x) \phi(x) \Big|_{x_{i+1/2}} - \rho(x) u(x) \phi(x) \Big|_{x_{i-1/2}} = D(x) \frac{d}{dx} \phi(x) \Big|_{x_{i+1/2}} - D(x) \frac{d}{dx} \phi(x) \Big|_{x_{i-1/2}} \tag{2.3b}$$

and integration of continuity equation yields

$$\int_{x_{i-1/2}}^{x_i+1/2} \frac{d}{dx} \rho(x) u(x) dx = 0 \tag{2.4a}$$

$$\rho(x) u(x) \Big|_{x_{i+1/2}} - \rho(x) u(x) \Big|_{x_{i-1/2}} = 0 \tag{2.4b}$$

### Central Differencing Scheme

For a uniform grid we can write the cell face values of property $\phi$ as

$$\phi(x_{i+1/2}) = \phi_{i+1/2} = \frac{\phi_i + \phi_{i+1}}{2} \tag{2.5a}$$

$$\phi(x_{i-1/2}) = \phi_{i-1/2} = \frac{\phi_{i-1} + \phi_i}{2} \tag{2.5b}$$

Substitution of the above expressions into the convection terms of Eq. (2.3) yields

$$\rho_{i+1/2} u_{i+1/2} \frac{\phi_i + \phi_{i+1}}{2} - \rho_{i-1/2} u_{i-1/2} \frac{\phi_{i-1} + \phi_i}{2} = \frac{D_i + D_{i + 1}}{2} \left( \frac{\phi_{i+1} - \phi_i}{h} \right) - \frac{D_{i - 1} + D_i}{2} \left( \frac{\phi_i - \phi_{i-1}}{h} \right) \tag{2.6}$$

This can be arranged to gives

$$- \left( \frac{\rho_{i-1/2} u_{i-1/2}}{2} - \frac{D_{i - 1} + D_i}{2h} \right)  \phi_{i-1} + \left( \frac{\rho_{i+1/2} u_{i+1/2} - \rho_{i-1/2} u_{i-1/2}}{2} + \frac{D_{i-1} + 2D_i + D_{i + 1}}{2h} \right)  \phi_i  $$

$$ + \left(\frac{\rho_{i+1/2} u_{i+1/2}}{2} - \frac{D_i + D_{i + 1}}{2h} \right) \phi_{i+1} = 0 \tag{2.7}$$

I can be easily recognized that Eq. (2.7) for steady convection - diffusion problems takes the same general form of Eq. (1.13) for pure diffusion problems. The difference is that the coefficients of the former contain additional terms to account for convection.

### Peclet Number

We define the non - dimensional cell Peclet number as a measure of the relative strengths of convection and diffusion

$$Pl = \frac{h \rho u}{D} \tag{2.8}$$

For high Peclet Number convection is dominant over diffusion and the transport of the property $\phi$ will be mainly influenced by the upstream source node along the flow direction.

For the numerical solution to be stable and accurate using the Central Differencing Scheme, the following condition must be satisfy:

$$Pl < 2 \tag{2.9}$$

It is important to note that the cell Peclet number is a combination of fluid properties ($\rho$ and $D$), a flow property ($u$), and the computational grid ($h$). For given values of $\rho$ and $D$, it is only possible to satisfy the stability condition if the velocity is small, hence in diffusion - dominated low Reynolds number flows ($Re = \rho u L / \mu$, ratio of inertial forces over viscous forces), or if the grid spacing is small.

Other discretization schemes which posses more favorable properties are: 

- Upwind Differencing scheme

- Quadratic Upwind Differencing scheme

- Total Variation Diminishing scheme

<br>


## 3. Pressure - Velocity Coupling in Steady Flows

Problems:

- The convective terms of the momentum equations contain non-linear quantities.

- All equations are intricately coupled. Every velocity component appears in each momentum equation and in the continuity equation.

For compressible flow, the continuity equation may be used as the transport equation for density. In addition, the energy equation is the transport equation for temperature. The pressure may then be obtained from density and temperature by using the equation of state $p = p(\rho, T)$.

For incompressible flow, the density is constant and not linked to the pressure. In this case, coupling between pressure and velocity introduces a constraint in the solution: If the correct pressure field is applied in the momentum equations, the resulting velocity field should satisfy the continuity equation.

Both the problems associated with the non - linearity and pressure - velocity coupling can be resolved by adopting an iterative solution strategy such as the SIMPLE (Semi - Implicit Method for Pressure Linked Equations) algorithm (Patankar & Spalding, 1972).

The governing equations for steady - state laminar flow in one - dimensional domain are

$$\frac{d}{dx} \rho(x) u^2(x) = \frac{d}{dx} \mu(x) \frac{d}{dx} u(x) - \frac{d}{dx}p(x) + S(x) \tag{3.1}$$

$$\frac{d}{dx} \rho(x) u(x) = 0 \tag{3.2}$$

The scalar variables, including pressure, are stored at the grid interfaces. The velocities are calculated on grids centers around the cell faces. So, the pressure nodes coincide with the cell faces. The pressure gradient is given by

### Discretized Momentum Equations

The discretized momentum equations are given by

$$\int_{x_{i-1/2}}^{x_{i+1/2}} \frac{d}{dx} \rho(x) u(x) u(x) dx = \int_{x_{i-1/2}}^{x_{i+1/2}} \frac{d}{dx} \mu(x) \frac{d}{dx} u(x) dx - \int_{x_{i-1/2}}^{x_{i+1/2}}  \frac{d}{dx}p(x) dx + \int_{x_{i-1/2}}^{x_{i+1/2}} S(x) dx \tag{3.3a}$$

$$\rho(x) u(x) u(x) \Big|_{x_{i+1/2}} - \rho(x) u(x) u(x) \Big|_{x_{i-1/2}} $$
$$= \mu(x) \frac{d}{dx} u(x) \Big|_{x_{i+1/2}} - \mu(x) \frac{d}{dx} u(x) \Big|_{x_{i-1/2}} - p(x) \Big|_{x_{i+1/2}} + p(x) \Big|_{x_{i-1/2}} + h \bar{S} \tag{3.3b}$$

$$\rho_{i+1/2} u_{i+1/2} \left( \frac{u_i + u_{i+1}}{2}\right) - \rho_{i-1/2} u_{i-1/2} \left( \frac{u_{i-1} + u_i}{2}\right)$$
$$ = \mu_{i+1/2} \left( \frac{u_{i+1} - u_i}{h} \right) - \mu_{i-1/2} \left( \frac{u_i - u_{i-1}}{h} \right) - p_{i+1/2} + p_{i-1/2} + h \bar{S} \tag{3.3c}$$

$$\left(\frac{\rho_{i-1/2} u_{i-1/2}}{2} - \frac{\mu_{i-1/2}}{h} \right) u_{i-1} + \left( \frac{\rho_{i+1/2} u_{i+1/2} - \rho_{i-1/2} u_{i-1/2}}{2} + \frac{\mu_{i+1/2} + \mu_{i-1/2}}{h} \right) u_i + \left( \frac{\rho_{i+1/2} u_{i+1/2}}{2} - \frac{\mu_{i+1/2}}{h} \right) u_{i+1}$$
$$ = - p_{i+1/2} + p_{i-1/2} + h \bar{S} \tag{3.3}$$

Given a pressure field $p$, discretized momentum equations can be solved to obtain the velocity fields. If the pressure field is correct, the resulting velocity field will satisfy continuity equation. As the pressure field is unknown, we need a method for calculating pressure.

### The SIMPLE Algorithm

To initiate the SIMPLE calculation process, a pressure field $p^*$ is guessed. Discretized Momentum Equations are solved using the guessed pressure field to yield the velocity estimates.

$$\left(\frac{\rho_{i-1/2} u_{i-1/2}}{2} - \frac{\mu_{i-1/2}}{h} \right) u^*_{i-1} + \left( \frac{\rho_{i+1/2} u_{i+1/2} - \rho_{i-1/2} u_{i-1/2}}{2} + \frac{\mu_{i+1/2} + \mu_{i-1/2}}{h} \right) u^*_i + \left( \frac{\rho_{i+1/2} u_{i+1/2}}{2} - \frac{\mu_{i+1/2}}{h} \right) u^*_{i+1}$$
$$ = - p^*_{i+1/2} + p^*_{i-1/2} + h \bar{S} \tag{3.4}$$

We define the correction $p'$ as the difference between correct pressure field $p$, and the guessed pressure field $p^*$

$$p_{i \pm 1/2} = p^*_{i \pm 1/2} + p'_{i \pm 1/2} \tag{3.5}$$

Similarly we define velocity correction $u'$ to relate the correct velocity $u$ to the guessed velocity $u*$

$$u_i = u^*_i + u'_i \tag{3.6}$$

Substitution of the correct pressure field $p$ into the momentum equations and subtract Eq. (3.4) yields

$$\left(\frac{\rho_{i-1/2} u_{i-1/2}}{2} - \frac{\mu_{i-1/2}}{h} \right) \left( u_{i-1} - u^*_{i-1} \right)  + \left( \frac{\rho_{i+1/2} u_{i+1/2} - \rho_{i-1/2} u_{i-1/2}}{2} + \frac{\mu_{i+1/2} + \mu_{i-1/2}}{h} \right) \left( u_{i} - u^*_{i} \right) $$
$$ + \left( \frac{\rho_{i+1/2} u_{i+1/2}}{2} - \frac{\mu_{i+1/2}}{h} \right) \left( u_{i+1} - u^*_{i+1} \right) = - \left( p_{i+1/2} - p^*_{i+1/2} \right) + \left( p_{i-1/2} - p^*_{i-1/2} \right)  \tag{3.7}$$

Using the correction formulas, Eqs. (3.5) and (3.6)

$$\left(\frac{\rho_{i-1/2} u_{i-1/2}}{2} - \frac{\mu_{i-1/2}}{h} \right) u'_{i-1} + \left( \frac{\rho_{i+1/2} u_{i+1/2} - \rho_{i-1/2} u_{i-1/2}}{2} + \frac{\mu_{i+1/2} + \mu_{i-1/2}}{h} \right) u'_{i} $$
$$ + \left( \frac{\rho_{i+1/2} u_{i+1/2}}{2} - \frac{\mu_{i+1/2}}{h} \right) u'_{i+1}= - p'_{i+1/2} + p'_{i-1/2} \tag{3.8}$$

At this point an approximation is introduced. The coefficient associated to $u_{i-1}$ and $u_{i+1}$ are dropped to simplify the equations. Omission of these terms is the main approximation of the SIMPLE algorithm.

$$\left( \frac{\rho_{i+1/2} u_{i+1/2} - \rho_{i-1/2} u_{i-1/2}}{2} + \frac{\mu_{i+1/2} + \mu_{i-1/2}}{h} \right) u'_{i} = - p'_{i+1/2} + p'_{i-1/2} \tag{3.9a}$$

$$u'_{i} = d_i \left( p'_{i-1/2} - p'_{i+1/2} \right)  \tag{3.9}$$

and substituting Eq. (3.9) in (3.6) gives

$$u_i = u^*_i + d_i \left( p'_{i-1/2} - p'_{i+1/2} \right)  \tag{3.10}$$

### Discretized Continuity Equation

Thus fas we have only considered the momentum equations but the velocity field is also subject to the constraint that it should satisfy continuity equation. The discretized form of the continuity equation applied on a control volume interface is

$$\int_{x_{i}}^{x_{i+1}} \frac{d}{dx} \rho(x) u(x) dx = 0 \tag{3.11a}$$

$$ \rho(x) u(x) \Big|_{x_{i+1}} - \rho(x) u(x) \Big|_{x_{i}} = 0 \tag{3.11b}$$

$$ \rho_{i+1} u_{i+1} - \rho_i u_{i} = 0 \tag{3.11}$$

Substituting the corrected velocity into the discretized continuity equation gives

$$ \rho_{i+1} \left[ u^*_{i+1} + d_{i+1} \left( p'_{i+1/2} -p'_{i+3/2} \right) \right] - \rho_i \left[ u^*_{i} + d_{i} \left( p'_{i-1/2} -p'_{i+1/2} \right) \right] = 0 \tag{3.12}$$

This may be rearranged to give

$$ - \left( \rho_i d_i \right) p'_{i-1/2} + \left( \rho_i d_i + \rho_{i+1} d_{i+1} \right) p'_{i+1/2} + \left( \rho_{i+1} d_{i+1} \right) p'_{i+3/2} = \rho_i u^*_{i} - \rho_{i+1} u^*_{i+1} \tag{3.13}$$

Equation represents the discretized continuity equation as an equation for pressure correction. The source term is the continuity imbalance arising from the incorrect velocity field.

### Summary

The SIMPLE algorithm gives a method of calculating pressure and velocities. The method is iterative, and the sequence of operations is given by:

- Initial guess: $p^*, u^*$

- Solve discretized momentum equations to obtain the predicted velocities: $u^*$

$$\left(\frac{\rho_{i-1/2} u_{i-1/2}}{2} - \frac{\mu_{i-1/2}}{h} \right) u^*_{i-1} + \left( \frac{\rho_{i+1/2} u_{i+1/2} - \rho_{i-1/2} u_{i-1/2}}{2} + \frac{\mu_{i+1/2} + \mu_{i-1/2}}{h} \right) u^*_i + \left( \frac{\rho_{i+1/2} u_{i+1/2}}{2} - \frac{\mu_{i+1/2}}{h} \right) u^*_{i+1}$$
$$ = - p^*_{i+1/2} + p^*_{i-1/2} + h \bar{S}$$

- Solve pressure correction equation: $p'$

$$ - \left( \rho_i d_i \right) p'_{i-1/2} + \left( \rho_i d_i + \rho_{i+1} d_{i+1} \right) p'_{i+1/2} + \left( \rho_{i+1} d_{i+1} \right) p'_{i+3/2} = \rho_i u^*_{i} - \rho_{i+1} u^*_{i+1}$$

- Correct pressure and velocities:

$$p_{i \pm 1/2} = p^*_{i \pm 1/2} + p'_{i \pm 1/2}$$

$$u_i = u^*_i + d_i \left( p'_{i-1/2} - p'_{i+1/2} \right)$$

- Solve all other discretized transport equations:

- Check stop criteria (pressure and velocity). Otherwise update pressure and velocity

$$p^* = p$$

$$u^* = u$$

<br>
