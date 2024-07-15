# Solid Mechanics Fundamentals

Ottosen N.S., and Peterson H., Introduction to the Finite Element Method. Prentice Hall, 1992

## Stresses

The stress tensor is defined as

$$\bold{S} = 
\begin{bmatrix}
\bold{s_x}^T \\ \bold{s_y}^T \\ \bold{s_z}^T
 \end{bmatrix} = 
\begin{bmatrix}\
\sigma_{xx} & \sigma_{xy} & \sigma_{xz} \\
\sigma_{yx} & \sigma_{yy} & \sigma_{yz} \\
\sigma_{zx} & \sigma_{zy} & \sigma_{zz} 
\end{bmatrix}$$

containing all the `stress components`. The $\sigma_{uu}$ are called `normal stresses`, whereas $\sigma_{uv}$ are referred to as `shear stresses`. From the notation $\sigma_{uv}$, $u = (x, y, z)$ is the normal plane direction, whereas $v = (x, y, z)$ is the component orientation.

In addition, through a moment equilibrium analysis along each direction we can obtain that

$$\sigma_{uv} = \sigma_{vu}$$

Therefore, the matrix $\bold{S}$ is symmetric.

**Note**: Traction is force per unit area

$$\vec{t} = \vec{F} / A$$

<br>

## Stress Equilibrium Equations

The forces acting on a arbitrary body are given by the traction vector $\bold{S\hat{n}}$ along the boundary surface $S$ and the body force $\bold{f}$ in the region $V$. Equilibrium requires that

$$\int_S \bold{S \cdot \hat{n}} dS + \int_V \bold{f} dV = 0$$

Using Gauss' divergence theorem, it is obtained

$$\int_V (\nabla \bold{S} + \bold{f})dV = 0$$

and so, it concluded that 

$$\nabla \bold{S} + \bold{f} = 0$$

which give us to the equilibrium equations:

$$\frac{\partial \sigma_{xx}}{\partial x}  + \frac{\partial \sigma_{xy}}{\partial y} + \frac{\partial \sigma_{xz}}{\partial z}  + f_x  = 0$$


$$\frac{\partial \sigma_{yx}}{\partial x}  + \frac{\partial \sigma_{yy}}{\partial y} + \frac{\partial \sigma_{yz}}{\partial z}  + f_y  = 0$$

$$\frac{\partial \sigma_{zx}}{\partial x}  + \frac{\partial \sigma_{zy}}{\partial y} + \frac{\partial \sigma_{zz}}{\partial z}  + f_z  = 0$$

<br>


## Strain Displacement Relations

The displacements of a point $(x, y, z)$ are given by $\bold{u}(x, y, z)$. For a neighboring point $(x + dx, y + dy, z + dz)$, the displacement become $\bold{u} + \bold{du}$.

The relative elongation or `normal strain` is defined as

$$\epsilon_{xx} = \frac{\partial u_x}{\partial x}, \quad 
\epsilon_{yy} = \frac{\partial u_y}{\partial y}, \quad
\epsilon_{zz} = \frac{\partial u_z}{\partial z}$$

and the `shear strain` is defined as

$$\gamma_{xy} = \frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x}, \quad 
\gamma_{xz} = \frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x}, \quad 
\gamma_{yz} = \frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y} $$

and also, they are symmetric, i.e. $\gamma_{uv} = \gamma_{vu}$. With, the `normal strains` and the `shear strains`, a complete description of the deformation of the body is achieved. As derivatives of the displacements, the strains are independent of rigid-body motions. However, the above equations were derived under the assumption of small displacement gradients, i.e. small strains. In practice, small strains mean strains smaller than 3-5%

<br>


## Linear Elasticity and Hooke's Law

The relation between stresses and strains is called the `constitutive relation` and a variety of such relations has been established. Examples are elasticity, plasticity, viscoelasticity, viscoplasticity, and creep. We shall consider the simplest constitutive theory, namely `linear elasticity`.

In one dimension, linear elasticity is expressed by `Hooke's Law` - Stress is directly proportional to the strain

$$\sigma = E \epsilon$$

where the material constant $E$ is `Young's modulus`. Only Applied within the `Elastic Range` of the material. We note that `loading` and `unloading` follow the same path. This means that the material response is `path independent` or `history independent`, as there exists a one-to-one relation between stress and strain.

These characteristics also hold for linear elasticity with several stress and strain components. In this general case, a direct generalization of Hooke's Law, which maintains the concept of linearity between stresses and strains, is given by

$$\bold{\sigma} = \bold{D \epsilon}$$

$$ \begin{Bmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \sigma_{zz} \\ \sigma_{xy} \\ \sigma_{xz} \\ \sigma_{yz} \end{Bmatrix} = 
\begin{bmatrix}
D_{11} & D_{12} & \cdots & D_{16} \\ 
D_{21} & D_{22} & \cdots & D_{26} \\ 
\vdots & \vdots & \ddots & \vdots \\
D_{61} & D_{62} & \cdots & D_{66} \\ 
\end{bmatrix} 
\begin{Bmatrix} \epsilon_{xx} \\ \epsilon_{yy} \\ \epsilon_{zz} \\ \gamma_{xy} \\ \gamma_{xz} \\ \gamma_{yz} \end{Bmatrix}$$

and $\bold{D}$ is the constitutive matrix. As linearity is required, the $\bold{D}$ is constant. This elasticity, which possesses the properties of linearity and a one-to-one relation between stresses and strains, is also termed `Cauchy elasticity`.

Also, if the `strain energy` for a given strain state only depends on the `strain state` itself and not the manner in which this strain state was obtained, we obtain the so-called `hyperelasticity` or `Green elasticity`. In this case, the constitutive matrix $\bold{D}$ is symmetric, i.e.

$$\bold{D} = \bold{D}^T$$

This symmetry property is used almost universally within linear elasticity and the 36 elasticity coefficients of $\bold{D}$ reduce to 21 independent coefficients.

If the $\bold{D}$-matrix takes the same form irrespective of the coordinate system, we called an `isotropic` material

$$ \bold{D} = \frac{E}{(1+\upsilon)(1-2\upsilon)} \begin{bmatrix}
1 - \upsilon & \upsilon & \upsilon & 0 & 0 & 0 \\ 
\upsilon & 1 - \upsilon & \upsilon & 0 & 0 & 0 \\ 
\upsilon & \upsilon & 1 - \upsilon & 0 & 0 & 0 \\ 
0 & 0 & 0 & \frac{1 - 2\upsilon}{2} & 0 & 0 \\ 
0 & 0 & 0 & 0 & \frac{1 - 2\upsilon}{2} & 0 \\ 
0 & 0 & 0 & 0 & 0 & \frac{1 - 2\upsilon}{2}\\ 
\end{bmatrix}$$

where $E$ is the `Young's modulus`, and $\upsilon$ the `Poisson's ratio`. We recall that an isotropic material has the same properties in all directions. This type of material is the one most often used in engineering applications.

We also define the `shear modulus` $G$, given by

$$G = \frac{E}{2(1 + \upsilon)}$$

and, from $\bold{D}$, we have that

$$\sigma_{xy} = G \gamma_{xy} \quad \sigma_{xz} = G \gamma_{xz} \quad \sigma_{yz} = G \gamma_{yz}$$

where the shear stresses and shear strains are independent of (i.e. uncoupled from) the normal stresses and normal strains.

We finally remark that if $\bold{D}$ dependes on position, i.e. $\bold{D} = \bold{D}(x,y,z)$, then the material is referred to as `inhomogeneous`; otherwise it is termed `homogeneous`.

### Initial strains

From linear elasticity, it appears that zero stresses imply zero strains. However, there exist situations with the presence of non-zero strains for zero stresses, i.e

$$\bold{\epsilon} = \bold{D}^T \bold{\sigma} + \bold{\epsilon_0}$$

that implies

$$\bold{\sigma} = \bold{D}(\bold{\epsilon} - \bold{\epsilon_0})$$

An important example of such initial strains is `thermal strains`, i.e. strains caused by the thermal expansion of the material. When thermal strains are considered in Hooke's law, one speaks of `thermoelasticity`.

Consider a specimen of isotropic material which is free to expand as a result of a change in temperature. As the material is free to expand, $\bold{\sigma} = 0$ holds, and the thermal strains are then given by

$$ \bold{\epsilon_0} = \alpha \Delta T \begin{bmatrix}
1 \\ 
1 \\ 
1 \\ 
0 \\ 
0 \\ 
0 \\ 
\end{bmatrix}$$

where $\alpha$ is the `thermal expansion coefficient` [$1 / \degree C$] and $\Delta T$ is the change in temperature. And,

$$ \bold{D} \bold{\epsilon_0} = \frac{E \alpha \Delta T}{1-2\upsilon} \begin{bmatrix}
1 \\ 
1 \\ 
1 \\ 
0 \\ 
0 \\ 
0 \\ 
\end{bmatrix}$$

<br>

## Equations for solid mechanics

the stresses $\bold{\sigma}$ must fulfil the `differential equations of equilibrium`:

$$\tilde{\nabla} \bold{\sigma} + \bold{f} = 0$$

where $\bold{f}$ is the body force vector. The strains $\bold{\epsilon}$ must fulfil the `kinematic relation`

$$\bold{\epsilon} = \tilde{\nabla} \bold{u}$$

where $\bold{u}$ is the displacement vector. Within our assumption of small strains, these equations hold for arbitrary solid materials which can be considered as continua.

For a specific kind of material, the relation between stresses and strains is given in terms of the `constitutive relation`. Considering linear elasticity or Hooke's generalized law

$$\bold{\sigma} = \bold{D \epsilon} - \bold{D \epsilon_0}$$

These expressions are generally referred to as the `field equations for thermoelasticity`. 

These field equations have to be solved given certain boundary conditions. These boundary conditions may be expressed in terms of prescribed traction vectors $\bold{t}$ or prescribed displacements $\bold{u}$. We note that it is not possible to prescribe the traction vector and the displacement vector at the same position.

## Comparison of the equations of heat flow and solid mechanics

* The variable $T$ or $\bold{u}$ is often termed the `state` variable as it comprises the unknown, i.e. the state itself.

* The distribution of the state variable gives rise to a certain physical quantity called the `flux` vector ($\bold{q}$ in heat flow, $\bold{\sigma}$ in solid mechanics).

* At the boundary, this flux vector is determined by $q_n$ for heat flow and by the traction vector $t$ in solid mechanics.

* It is characteristic that the divergence always enters the balance principle. which takes the form of a `conversation principle` in heat flow and an `equilibrium condition` for solid mechanics.

* In order to relate the state variables $T$ or $\bold{u}$ to the fluxes $\bold{q}$ or $\bold{\sigma}$, a `kinematic` quantity is derived from the state variable. In heat flow, this kinematic quantity is the `temperature gradient` $\nabla T$ whereas in solid mechanics it is the strain $\bold{\epsilon}$.

* The flux and kinematic quantity are related by the `constitutive law` in terms of Fourier's or Hooke's law.

The insertion of the constitutive law into the balance equation gives

$$\nabla \cdot \bold{D} \nabla T + Q = 0$$

for heat flow, whereas for elasticity we obtain

$$\tilde{\nabla}^T \bold{D} \tilde{\nabla} \bold{u} + \bold{f} = 0$$

This last set of equations is termed `Navier's equations` from 1821.

<br>
