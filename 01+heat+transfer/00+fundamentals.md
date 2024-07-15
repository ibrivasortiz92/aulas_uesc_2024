# Fundamentals (Heat Transfer)

## 1. Heat Diffusion Equation

The first law of thermodynamics for a closed system takes the form

$$\frac{dU}{dt} = Q - W \tag{1.1}$$

where $dU/dt$ is the rate of change of internal thermal energy. $Q$ is the heat transfer rate into the control volume and $W$ is work transfer rate done by the control volume. They may be expressed in joules per second ($J/s$) or watts. 

Frequently, solids and liquids are approximated as being incompressible (constant volume). In this cases, Eq. (1.1) takes the form

$$\frac{dU}{dt} = Q \tag{1.2}$$

The net heat $Q$ generated or consumed within a control volume is obtained through

$$Q = - \int_S{\mathbf{q} \cdot \mathbf{n} dS} + \int_V{\dot{q}dV} \tag{1.3}$$

where $\mathbf{q}$ is the heat flux ($W/m^2$) obtained from the `Fourier's Law`

$$ \mathbf{q} = - k \nabla T \tag{1.4}$$

and $\dot{q}$ is a volumetric heat generation ($W / m^3$). 

In Eq. (1.5), $k$ is the `thermal conductivity` ($W/m \degree K$). It depends on temperature in the most general case. However for many engineering problems, materials are often considered to posses a constant thermal conductivity. The table below shows the values of thermal conductivities of various engineering materials

|Substance|$k \space (W/m \degree K)$|
|----|----|
|Steel|19.3|
|Water|0.51|
|Air|0.022|

For solids the transport of energy by conduction is due drift of free electrons and lattice vibration waves. the thermal conductivity for most metals (except aluminum and uranium) decreases with increasing temperature. The thermal conductivity in liquids decreases, and, for gases, increases when increases the temperature.

The rate of internal thermal energy is obtained from

$$\frac{dU}{dt} = \int_V{\rho c \frac{\partial T}{\partial t} dV} \tag{1.5}$$

where $\rho$ is the material `density` ($kg / m^3$), and $c$ is the `specific heat capacity` ($J / kg \degree K$). The derivate of $T$ is in partial form because $T$ is a function of both $\mathbf{r}$ and $t$.

Substituting Eqs. (1.3) and (1.5) into (1.2) we obtain that

$$\int_V{\rho c \frac{\partial T}{\partial t} dV} = \int_S{k \nabla T \cdot \mathbf{n} dS} + \int_V{\dot{q}dV} \tag{1.6}$$

From the Gauss theorem, which converts a surface integral into a volume integral we obtain that

$$\int_S{k \nabla T \cdot \mathbf{n} dS} = \int_V{\nabla \cdot k \nabla T dV} \tag{1.7}$$

and so, Eq. (1.6) can be rewritten as

$$\int_V{\left( \nabla \cdot k \nabla T  - \rho c \frac{\partial T}{\partial t} + \dot{q} \right) dV} \tag{1.8}$$

Since the control volume $V$ is arbitrary, the integrand must vanish identically. Therefore, we obtain the `heat diffusion equation`:

$$\nabla \cdot k \nabla T  - \rho c \frac{\partial T}{\partial t} + \dot{q} \tag{1.9}$$

The limitations on this equation are:

- Incompressible medium (no expansion work term was included).

- No convection (the medium cannot undergo any relative motion).

<br>


## 2. Simplifications

A more complete version of the heat conduction equation is obtained if the variation of $k$ with $T$ is small. Then, the thermal conductivity can be considered as a average constant value and 

$$\nabla^2 T + \frac{\dot{q}}{k} = \frac{1}{\alpha} \frac{\partial T}{\partial t}  \tag{2.1}$$

where $\alpha = k / \rho c$ is the `thermal diffusivity` which is a measure of how well a material conduct heat. The term $\nabla^2 T = \nabla \cdot \nabla T$ is called the Laplacian.

<br>


## Extra Notes

Thermodynamic axioma: When two systems are brought into contact through some kind of wall, energy transfer such as `heat` and `work` take place between them.

**0th Law of Thermodynamics**: Two system in thermal equilibrium shares the same temperature.

**1st Law of Thermodynamics**: Energy can neither be created nor destroyed.

**2st Law of Thermodynamics**: Any isolated system spontaneously evolves towards thermal equilibrium - the state of maximum entropy.

**3rd Law of Thermodynamics**: The entropy of a system approaches a constant value as the temperature approaches absolute zero.

**Work**: Transfer of energy to a particle which is evidenced by changes in its position when acted upon by a force.

**Heat**: Energy in the process of being transferred.

**Energy** is what is stored. Work and heat are two ways of transferring energy across the boundaries of a system.

The transfer and conversion of energy from one form to another are governed by the first and second law of thermodynamics.

**Thermodynamic vs Heat Transfer**:

* Thermodynamic: Deals with the relation between heat and other forms of energy. Thermal - equilibrium systems.

* Heat Transfer: Analysis of the rate of heat transfer. Non - equilibrium states.

### Heat Transfer

The knowledge of `temperature distribution` is essential in heat transfer studies because of the fact that the heat flow takes place only wherever there is a temperature gradient.

The energy transfer as heat takes place by three distinct modes: 

* **Conduction**: Heat transfer accomplished via molecular interaction, and kinetic of free electrons. Pure conduction is found only in solids.

* **Convection**: Heat transfer cause by a relative motion within the system. Free or Natural Convection: Fluid motion driven by buoyancy effects (density variation caused by the temperature difference in the fluid). Forced Convection: Fluid motion caused by an external force.

* **Radiation**: Heat transfer via an electromagnetic wave phenomenon. No medium is required for its propagation. Depends only on the temperature and the material optical properties.

### Convection

The Newton's law of cooling states that

$$q = h(T_s-T_\infty)$$

where $T_\infty$ is the mean temperature of a fluid flowing over a surface at $T_s$. The heat transfer coefficient $h$ has units of $W/m^2K$.

|Types of flow| $h \space (W/m^2K)$|
|---|---|
|Free convection, air| 5 - 28|
|Forced convection, air|10 - 500|
|Water| 100 - 17000|
|Boiling water| 2500-57000|
|Condensation of steam| 5000 - 11000|

### Thermal Radiation

The Stefan-Boltzmann law state that the radiation energy emitted by a body is proportional to the fourth power of its absolute temperature

$$Q = \sigma A T^4$$

where $\sigma$ is called the Stefan-Boltzmann constant with the value of $5.6697 \times 10^{-8} W/m^2K^4$, and $T$ is the surface temperature in degree Kelvin.

The gray nature of real surface can be accounted by a factor $\varepsilon$ called `emissivity` which relates radiation between gray and black bodies at the same temperature. The net heat exchange between similar bodies can be formulated as

$$Q = \sigma A \varepsilon F(T_1^4 - T_2^4)$$

where the factor $F$, called view factor, is dependent upon geometry of the two surfaces exchanging radiation.

<br>
