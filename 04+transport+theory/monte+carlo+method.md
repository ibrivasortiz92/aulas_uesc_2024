# Monte Carlo Method

Monte Carlo methods are capable of treating very complex three - dimensional configurations. Moreover, the continuous treatment of energy, as well as space and angle, obviates discretization errors. The errors in Monte Carlo calculations take the form of stochastic uncertainties.

In its simplest form, Monte Carlo consists of simulating a finite number, of particle histories through the use of a random number generator. In each particle history random numbers are generated and used to sample appropriate probability distributions for scattering angles, track length distances between collisions, and so on.

The estimate of the expectation or mean value of some quantity $\bar{x}$ take the form of the mean of $N$ samples

$$\hat{x} = \frac{1}{N} \sum_{n=1}^N x_n$$

where $x_n$ is the contribution of the $n$ th history to that quantity. Thus as the Monte Carlo calculation proceeds, we tally the $x_n$ due to each history in order ro calculate the estimated or sample mean $\hat{x}$ at the end of the calculation.

<br>

## 1. Probability Distribution Functions

Let consider a random variable $x$. By random variable we mean a variable that takes on particular values with a frequency that is determined by some underlying probability distribution. We define

$$P \left[ a \leq x \leq b \right] \tag{1.1}$$

as the probability that $x$ will have value between $a$ and $b$.

The `probability density function` $f(x)$ is defined as

$$ f(x) \Delta x =  P \left[x \leq x' \leq x + \Delta x  \right] \tag{1.2}$$

Thus $f(x) \Delta x$ is just the probability that $x'$ will take on a value between $x$ and $x + \Delta x$. Clearly we must have $f(x) \geq 0$ and

$$\int_a^b f(x) dx = P \left[ a \leq x \leq b \right] \tag{1.3}$$

If the values of $x$ are restricted to between $a$ and $b$, we require that the probability density function be normalized by

$$\int_a^b f(x) dx = 1 \tag{1.4}$$

On the other hand, the `cumulative probability distribution function`, defined by

$$F(x) = P \left[ x' \leq x \right] \tag{1.5}$$

is the probability that the random variable $x'$ is less that or equal to $x$. From our definition of $f(x)$ we have for a random variable that can take on only real values

$$F(x) = \int_{-\infty}^x f(x') dx' \tag{1.6}$$

and using Eqs. (1.3) and (1.6), we have

$$P \left[ a \leq x' \leq b \right] = F(b) - F(a) \tag{1.7}$$

### Random Variables Transformation Rule

It is often more convenient to write Eq. (1.6) in the differential form

$$\frac{d F(x)}{dx} = f(x) \tag{1.8}$$

Suppose $y(x)$ is a function of the random variable $x$. If $g(y)dy$ is the probability that $y$ is between $y$ and $y + dy$, and $f(x)dx$ is the probability that $x$ is between $x$ and $x + dx$, the probability density functions $g(y)$ and $f(x)$ must satisfy

$$|g(y) dy| = |f(x) dx| \tag{1.9}$$

or since $g(y) \ge 0$ and $f(x) > 0$,

$$g(y) = f(x)\left|\frac{dx}{dy}\right| \tag{1.10}$$

For one very particular function, where $y = F(x)$ of the random variable $x$, where $F(x)$ is the cumulative probability distribution, we obtain for this particular transformation that

$$g(F) = 1 \quad 0 \leq F \leq 1 \tag{1.11}$$

Since $g(F)$ is just the probability density function of the random variable $F$, Eq. (1.11) states that the probability of $F$ taking on a value between $F$ and $F + dF$ is just equal to $dF$. Thus $F$ is uniformly distributed between zero and one.

This relationship is very important in Monte Carlo calculations because we can use random number generator uniformly distributed (constant value) between zero and one to sample uniformly distributed $F(x)=\xi$ in an unbiased manner (every possible number has an equal probability of being selected). And the distribution of $x$ can be computed through

$$x = F(\xi)^{-1} \tag{1.12}$$

Aside from the straightforward evaluation of probability distributions by inversion there are alternative methods that may prove to be beneficial, particularly if the inverse of $F(x)$ is costly to obtain or if $f(x)$ is given as numerical data: the `rejection technique` and the `numerical evaluation`.

**Example**: Suppose we want to generate a series of random numbers that are distributed according to the number of mean free paths that particles will travel between collisions. Our random variable $x$ is the mean free paths. The probability density functions is

$$f(x) = e^{-x}$$

where we have assumed total cross section equal to 1. The cumulative probability distribution is

$$F(x) = 1 - e^{-x}$$

For this simple relationship we may perform the inversion directly to obtain

$$x = - ln(1 - \xi)$$

Moreover, if $\xi$ is uniformly distributed between 0 and 1 so will be $1 - \xi$, so that we simply write

$$x = -ln(\xi)$$

### Functions of Two Random Variables

Probability distributions may also be defined as a function of more than one random variables. If we have two random variables $x$ and $y$, then we may define a joint probability density function

$$f(x, y) \Delta x \Delta y = P \left[ x \leq x' \leq x + \Delta x, y \leq y' \leq y + \Delta y \right] \tag{1.13}$$

The normalization for the joint probability density function is

$$\int_{- \infty}^\infty dx \int_{- \infty}^\infty dy f(x, y) = 1 \tag{1.14}$$

If we integrate over only one of the variables, we obtain

$$g(x) = \int_{- \infty}^\infty dy f(x,y) \tag{1.15}$$

$$h(y) = \int_{- \infty}^\infty dx f(x,y) \tag{1.16}$$

These quantities are referred to as the `marginal probability densities` of $x$ and $y$, respectively.

In Monte Carlo calculations these distributions normally take one of two limiting forms either with $x$ and $y$ independent of one another or with $x$ conditional on the value of $y$. If the joint probability density function is separable in the form

$$f(x, y) = f_1(x) f_2(y) \tag{1.17}$$

then $x$ and $y$ are said to be independent.


**Example**: Choosing the direction of particles produced or scattered isotropically. The production is proportional to the solid angle $d \Omega$:

$$f(\Omega) d \Omega = C d \Omega$$

where $C$ is a constant. Since $\int d \Omega = 1$, we must have $C = f(\Omega) = 1$. Now, $d \Omega$ may be written in terms of $(\theta, \omega)$, the polar and azimuthal coordinates

$$d \Omega = \frac{d \theta sin(\theta) d \omega}{4 \pi} = \left( \frac{d \mu}{2}\right) \left( \frac{d \omega}{2 \pi} \right)$$

where $\mu = cos(\theta)$. Clearly, this equation is in the form

$$f(\mu, \omega) = f_1(\mu) f_2(\omega)$$

where $f_1(\mu) = 1/2$ and $f_2(\omega) = 1 / (2 \pi)$. Hence $\mu$ and $\omega$ are to be sampled independently. So

$$\mu = 2 \xi_1 - 1 \quad \omega = 2 \pi \xi_2$$


Two random variables $x$ and $y$ may also be related by a conditional probability distribution. Thus

$$f(x|y) \Delta x = P \left[x \leq x' \leq x + \Delta x | y \right] \tag{1.18}$$

is the probability that $x$ will lie between $x$ and $x + \Delta x$ given the condition that a particular value $y$ is taken by the second random variable. The conditional probability density function of $x$, given $y$, is defined in terms of joint and marginal distributions,

$$f(x|y) = \frac{f(x, y)}{h(y)}, \quad h(y) \neq 0 \tag{1.19}$$


**Example**: Consider neutrons emitted at a distance $y$ from the outer surface of a solid. The solid is assumed to be a purely absorbing material. We may calculate the conditional probability $f(x|y)$ that a neutron emitted will travel a distance between $x$ and $x + dx$ in the solid, given that the distance to the surface is $y$. Since the neutron history may be terminated by either of two mechanism, collision or escape, the probability density function will have two contributions.

The probability that the neutron will collide before escaping is just

$$\int_0^y dx f(x|y) = \int_0^y dx \sigma_t e^{-\sigma_t x} = 1 - e^{-\sigma_t y}$$

and hence the escape probability is

$$1 - \int_0^y dx f(x|y) = e^{-\sigma y}$$

These probabilities may be combined through the use of a Dirac delta and Heavyside functions to obtain the conditional probability density function traveling a distance in the solid $x$ given a boundary at distance $y$:

$$f(x|y) = \sigma e^{- \sigma x} H(y - x) + e^{-\sigma y} \delta (x - y), \quad x \geq 0$$

where

$$H(x) = \begin{cases} 0 & x < 0 \\ 1 & x \geq 0  \end{cases}$$

The path lengths to the surface will depend on the space-angle distribution in which neutrons are emitted as well as on the size and shape of the solid. For any path length distribution $h(y)$, which is the marginal density function, we may write

$$f(x, y) = h(y) f(x|y)$$

<br>


## 2. Monte Carlo Sampling

We consider mono-energetic transport in a solid with isotropic scattering

### Tracking Procedure

1 Based on the source distribution, $S(x, y, z)$, three random numbers are generated to compute the starting point in space of the history.

2 Two more random numbers are used in conjunction with
 
$$d \Omega = \frac{d \theta sin(\theta) d \omega}{4 \pi} = \left( \frac{d \mu}{2}\right) \left( \frac{d \omega}{2 \pi} \right)$$

to determine the particle direction.

3 One more random number is used to determine the mean free path traveled before the next collision through

$$x = -ln(\xi)$$

if the particle passes out of the problem domain, it has escaped and the history is terminated.

4 Another random number is used to determine the interaction type:
if 

$$\xi < \sigma_a / \sigma_t$$

the particle is absorbed and the history is terminated; if 

$$\xi \geq \sigma_s / \sigma_t$$ 

the particle is scattered. The foregoing procedure is repeated from step 2. The Monte Carlo simulation consists of repeating the procedure for $N$ independent histories.

### Tallies

Since the histories are random, the property $x$ is also a random variable. It does not in general coincide with the random variables that are sampled in producing the histories:

- the scattering angles

- positions

- distances between collisions

Rather, $x$ most often is related to:

- scalar flux

- current distribution

- escape probability

Our task then is to ask which of the properties that we have available from the simulation of random particle histories should be `tallied` in order to calculate the $x$ property of interest.

**Example**: For scalar flux the two most widely used `tallies` result from the relationship between collision density and scalar flux, and from the definition of the scalar flux in terms of total neutron track length. Suppose that we want to calculate the average scalar flux $\bar{\phi}$ in some volume $V$ where the total cross section is $\sigma_t$. Then since $\sigma \bar{\phi}$ is the collision density, the mean number of collisions in $V$ per unit time is

$$\bar{c} = V \sigma_t \bar{\phi}$$

Hence for the Monte Carlo simulation we may write

$$\bar{\phi} = \frac{1}{V \sigma_t} \bar{c}$$

where $\bar{c}$ is the mean number of collisions, normalized to one source particle. The random variable whose mean we want to calculate is thus $\bar{c}$. We have a sample estimate o $\hat{c}$:

$$\hat{c} = \frac{1}{N} \sum_n c_n$$

where $c_n$ is the number of collisions made in $V$ during the $n$ th history. Our sample estimate of the scalar flux is then

$$\hat{\phi} = \frac{1}{V \sigma} \frac{1}{N} \sum_n c_n$$

The path length estimator for which every particle that passes through $V$ contributes, whether or not a collision occurs. The scalar flux can be defined as the total track length traversed by all particles per unit volume per unit time. Hence

$$\bar{\phi} = \frac{1}{V} \bar{l}$$

where $\bar{l}$ is the mean track length. From our path length estimator we have

$$\hat{\phi} = \frac{1}{V} \frac{1}{N} \sum_n l_n$$

<br>


## 3. Error Estimates

We use a number of random variables to estimate the scalar flux in Monte Carlo calculations. The question now arises as to how much error the sample estimate $\hat{\phi}$ is likely to have in relation to the true values of the mean $\bar{\phi}$. We introduce the concepts of expectation values and variance, and utilize the central limit theorem to arrive at an error estimate.

### Expectation Values

Suppose that $x$ is a random variable, for example, some property of a Monte Carlo history. The expectation value of $x$ is defined as

$$E \left[ x \right] = \bar{x} = \int_{-\infty}^\infty x f(x) dx \tag{3.1}$$

where $f(x)$ is the probability density distribution. Qualitatively, it is the mean value of $x$ that we would expect to achieve if we repeated a Monte Carlo calculation infinitely many times. 

Moreover, the expectation value of any one $x_n$ would  be

$$E \left[ x_n \right] = E \left[ x \right] \tag{3.2}$$

This expression states that the average value of $x_n$ is equal to the expectation or true mean value $\bar{x}$. Thus the expectation value of $\hat{x}$ may also be equal to $\bar{x}$:

$$E \left[ \hat{x} \right] = E \left[ \frac{1}{N} \sum_{n=1}^N x_n \right] = \frac{1}{N} \sum_{n=1}^N E\left[ x \right] = \bar{x} \tag{3.3}$$

This results do no imply that $x_n$ or even $\hat{x}$ will be equal to $\bar{x}$. 

### Variance

What is needed is a measure of the spread in values of $\hat{x}$ about $\bar{x}$. To do this we must first introduce some functions of a random variable.

Suppose that $g(x)$ is a real function of the random variable $x$. The expectation value of $g(x)$ is then defined by

$$E \left[ g(x) \right] = \bar{g} = \int_{-\infty}^\infty g(x) f(x) dx \tag{3.4}$$

Corresponding to Eq. (3.2), if we have $x_1$, $x_2$, ..., $x_n$ independently from $f(x)$, then

$$E \left[ g(x_n) \right] = E \left[ g(x) \right] \tag{3.5}$$

Moreover, we note that if $g$ is a linear combination

$$g(x) = C_1 g_1(x) + C_2 g_2(x) \tag{3.6}$$

then

$$E \left[ g(x_n) \right] = C_1 E \left[ g_1(x) \right] + C_2 E \left[ g_2(x) \right] \tag{3.7}$$

To estimate the spread of values of $x$, and eventually of $\hat{x}$, about $\bar{x}$ we introduce a particular function, the second moment about the mean

$$g(x) = \left(x - \bar{x}\right)^2 \tag{3.8}$$

Then by using Eq. (3.4), the `variance` is defined to be

$$\sigma^2(x) = E \left[ \left(x - \bar{x}\right)^2 \right] = \int_{-\infty}^\infty \left(x - \bar{x}\right)^2 f(x) dx $$

$$= \int_{-\infty}^\infty x^2 f(x) dx - 2 \bar{x} \int_{-\infty}^\infty x f(x) dx + \bar{x}^2 \int_{-\infty}^\infty f(x) dx $$

$$= \bar{x^2} - \bar{x}^2 \tag{3.9}$$

The standard deviation thus

$$\sigma(x) = \left( \bar{x^2} - \bar{x}^2 \right)^{1/2} \tag{3.10}$$

provides a measure of the spread of $x$ about the mean value $\bar{x}$.

We may now express the variance of $\hat{x}$ in terms of the variance of $x$. We define

$$\sigma^2(\hat{x}) = E \left[ \left(\hat{x} - \bar{x}\right)^2 \right] \tag{3.11}$$

Developing the expectation term we obtain

$$\sigma^2(\hat{x}) = \frac{1}{N} \sigma^2(x) \tag{3.12}$$

Demonstration found in Lewis & Miller, 1984 (Chapter 7). And the standard deviation is given by

$$\sigma(\hat{x}) = \frac{\sigma^2(x)}{\sqrt{N}} \tag{3.13}$$

where $\sigma(x)$ is a measure of the spread of individual $x_n$ about $\bar{x}$. If we use $\hat{x}$ constructed from $N$ values of $x_n$ to estimate $\bar{x}$, then the spread of the result of $\hat{x}$ around $\bar{x}$ is proportional to $\sigma(x)$ and falls off as the square root of the number of histories in the sample.

### Sample Variance

In order to estimate the spread in $\hat{x}$. The `sample variance` is defined by

$$S^2 = \frac{1}{N-1} \sum_{n=1}^N \left( x_n - \hat{x} \right)^2 \tag{3.14}$$

that satisfy the relation

$$E \left[ S^2\right] = \sigma^2(x) \tag{3.15}$$

which shown that the sample variance is an unbiased estimator of $\sigma^2(x)$. In practice, it is not calculated directly from Eq. (3.14). Instead, it is used

$$S^2 = \frac{N}{N-1} \left( \hat{x^2} - \hat{x}^2 \right) \tag{3.16}$$

where 

$$\hat{x^2} = \frac{1}{N} \sum_{n=1}^N x_n^2 \tag{3.17}$$

From this the `sample standard deviation` is calculated as

$$S = \left( \frac{N}{N-1} \right)^{1/2} \left[ \frac{1}{N} \sum_{n=1}^N x_n^2 - \hat{x}^2 \right]^{1/2} \tag{3.18}$$

Moreover, when large numbers of histories are involved, $N/(N-1)$ often is set equal to one.

### The Central Limit Theorem

Suppose that Monte Carlo calculations are carried out, each consisting of independent histories, such that the $x_n$ are computed from the same distribution having a finite mean and variance. For any fixed value of $N$ histories per calculation, there is a probability density function, say $f_N(\hat{x})$, which describes the distribution of the $\hat{x}$ that results from repeated Monte Carlo calculations.

The `Central Limit Theorem` states that, as $N$ approaches infinity, there is a specific limiting distribution for the resulting values of $\hat{x}$, and this is the normal distribution.

$$f_N(\hat{x}) \approx \frac{1}{\sqrt{2 \pi} \sigma(\hat{x})} \exp{\left[ \frac{- \left( \hat{x} - \bar{x} \right)^2}{2 \sigma^2(\hat{x})} \right]}, \quad N \to \infty \tag{3.19}$$

Moreover, since we already related $\sigma^2(\hat{x})$ to $\sigma^2(x)$ by Eq. (3.13), we may write

$$f_N(\hat{x}) \approx \sqrt{\frac{N}{2 \pi}} \frac{1}{\sigma(x)} \exp{\left[ \frac{- N \left( \hat{x} - \bar{x} \right)^2}{2 \sigma^2(x)} \right]}, \quad N \to \infty \tag{3.20}$$

While in practice we cannot calculate $\sigma^2(x)$ exactly, we can estimate it from the sample variance $S^2$. From the state of the `central limit theorem`, the probability that $\hat{x}$ is between $\bar{x} - \epsilon$ and $\bar{x} + \epsilon$ can be computed from

$$P \left[ \bar{x} - \epsilon < \hat{x} \leq \bar{x} + \epsilon \right] = \int_{\bar{x} - \epsilon}^{\bar{x} + \epsilon} f_N(\hat{x}) d \hat{x} \tag{3.21}$$

Inserting Eq. (3.20) and changing variables with $\sqrt{2/N} t = \left( \hat{x} - \bar{x} \right) / \sigma(x)$, we have

$$P \left[ \bar{x} - \epsilon < \hat{x} \leq \bar{x} + \epsilon \right] =  \frac{2}{\sqrt{\pi}} \int_{0}^{\sqrt{N/2} \epsilon / \sigma} e^{-t^2} dt \tag{3.22}$$

or using the definition of the error function

$$P \left[ \bar{x} - \epsilon < \hat{x} \leq \bar{x} + \epsilon \right] = erf \left[ \sqrt{N/2} \epsilon / \sigma(x) \right] \tag{3.23}$$

Thus given an $\epsilon$ we need only to evaluate the standard error integral to determine the probability that $\hat{x}$ will fall into the interval $\bar{x} \pm \epsilon$. For example, if we take $\epsilon = 0.674 \sigma(x) / \sqrt{N}$ we have a 50% probability that the value of $x$ will fall into the interval $x \pm 0.6740 \sigma(x)/ \sqrt{N}$.

More frequently when plus or minus errors are tabulated, they correspond to $\epsilon = \sigma(x) / \sqrt{N}$. This mean that $\hat{x}$ is within one standard deviation of $\bar{x}$. Two or three standard deviations may also be used if higher confidence levels are desired. For example

$$P \left[ \bar{x} - \frac{M \sigma(x)}{\sqrt{N}} \leq \hat{x} \leq \bar{x} + \frac{M \sigma(x)}{\sqrt{N}} \right] = \begin{cases} 
0.6826 & \quad M = 1 \\
0.954 & \quad M = 2 \\
0.997 & \quad M = 3 \\
\end{cases} \tag{3.24}$$

When using this error estimates, some cautionary notes are notice:

1. No matter what quantity is being estimated, the value of $N$ must be large enough for the expressions to hold. Not only because the central limit theorem applies only for large $N$, but also because a large number of histories is required for $S$ to give a reliable estimate of $\sigma(x)$.

2. The variance for a probability density function $f(x)$ for some tally does not exist. If the variance does not exist, a finite and fallacious value of the sample variance $S^2$ may be calculated and used to estimate error. Moreover, the central limit theorem is not applicable and, if a limiting distribution can be found for such situation, it generally is not Gaussian.

3. The histories turn out not to be independent. 

<br>


## 4. Monte Carlo Calculation

### Fixed Source Problem

Consider a sphere of pure absorber that is one mean free path in diameter. For convenience we take the cross section as $\sigma_t = 1$ and ask what is the average flux in the sphere due to a uniform isotropic source emitting one neutron per second. We do a Monte Carlo simulation using both collision and track length estimators of $\bar{\phi}$. 

$$V \bar{\phi} = \bar{c} \quad V \bar{\phi} = \bar{l}$$

For pure absorbers the collision estimator becomes binomial, since for each history, $c_n$ is either 0 or 1. The path length estimator $l_n$ is continuous, but it consists of only one contribution per history, the distance to the collision or to the surface.

To choose the radius $r$ from which a particular history originates, we need the spatial probability density function, which is

$$f(r) dr = \frac{dV}{V} = \frac{3 r^2 dr}{R^3}$$

Hence

$$F(r) = \left( \frac{r}{R} \right)^3$$

and the sampling for the initial radius is

$$r = R \xi_1^{1/3}$$

The distance from the neutron point of origin to the surface is

$$y = \left[ R^2 - r^2 sin^2 \theta \right]^{1/2} - r cos \theta$$

or, more simply,

$$y = \left[ R^2 - r^2 \left( 1 - \mu^2 \right) \right]^{1/2} - r \mu$$

where $\theta$ is the polar angle and $\mu = cos \theta$. For isotropic sources $\mu$ is evenly distributed over $-1 < \mu < 1$. Hence for each history another random number is generated for

$$\mu = 2\xi_2 - 1$$

Note that there is no need to sample the azimuthal angle since neither the distance to a collision nor to the surface of the sphere depends on it.

The distance to the first collision is then estimated by another random number

$$s = - ln \xi_3$$

For the collision estimator, $s$ is compared to the distance to the surface to determine whether the neutron collides in the sphere or escapes

$$c_n = \begin{cases} 
1 & \quad \text{if} \quad s \leq y \\ 
0 & \quad \text{if} \quad s > y
\end{cases}$$

For the track length estimator, only the counter is updated with the distance traveled before the first collision

$$l_n = s \quad \text{if} \quad x \leq y$$

The results are given below for the $\hat{c}$ and $\hat{l}$ estimators

|N    |$\hat{c}$          |$\hat{l}$          |
|----:|:------------------|:-----------------:|
|10   |$0.7000 \pm 0.1429$|$0.2063 \pm 0.0419$|
|100  |$0.3800 \pm 0.0455$|$0.2416 \pm 0.0215$|
|1000 |$0.2810 \pm 0.0143$|$0.2847 \pm 0.0066$|
|10000|$0.2942 \pm 0.0046$|$0.2922 \pm 0.0022$|
|Exact|$0.2927$           |$0.2927$           |


### Criticality Calculation

Given a distribution of fission neutrons, we follow them through their lifetime and determine how many fission neutrons rise to in the next generation. The ratio of the number of fission neutrons in the j'th generation $F_j$, to that in the j - 1 generation then gives the multiplication of the system $k_j$ for the j'th generation

$$k_j = \frac{F_j}{F_{j-1}}$$

After a sufficient number of generations the spatial distribution of neutrons from one generation to the next will become stationary except for statistical fluctuations. At this point the so-called `fundamental mode` or eigenfunction has been obtained, and the corresponding eigenvalue will no longer change from generation to generation.

In a Monte Carlo eigenvalue calculation, some finite number of neutron histories, say $N$, is originated by sampling a probability distribution of fission neutrons. This distribution is isotropic and is distributed in energy according to a standard fission spectrum $\chi(E)$. In the first generation the spatial distribution of the fission neutrons is determined either from a guess or as the result of simplified calculation. The source for each succeeding generation is then determined from the results of the preceding generation.

In the j'th generation each history is followed and its contribution, say $X_{n,j}$, to the number of fission neutrons produced in the j + 1 generation is calculated. The mean value

$$\hat{x}_j = \frac{1}{N} \sum_n x_{n,j}$$

may then be used as an estimate for $k_j$

$$k_j = \hat{x}_j$$

since $\hat{x}_j$ is normalized to one neutron in the preceding generation.

In general, each generation of particle proceeds in the same manner as in a fixed source problem with the exception that efficient tallies must be included:

- To specify the spatial fission distribution for the next generation

- To estimate the number of fission neutrons produced in the next generation.

At the time of absorption interaction the particle will produce

$$x_n = \frac{\nu \sigma_f(\vec{r}, E)}{\sigma_a(\vec{r}, E)} \Big|_n$$

neutrons in the next generation. Here $E$ and $\vec{r}$ designate the phase-space point of the particle absorption, where the cross sections are summed over all the nuclides present at $\vec{r}$. The value of $\vec{r}$ is recorded, and $x_n$ particles are produced from an isotropic sampling of the fission spectrum. Since $x_n$ is not ans integer, it is treated as

$$x_n = I_n + R_n$$

where $I_n$ is an integer and $0 < R_n < 1$ is the remainder. One then starts $I_n$ particles at $\vec{r}$. Then a random number $\xi$ is generated and if $\xi < R_n$ and additional particle is generated.

There is another estimator frequently used in criticality calculations based on collision and track length estimators that may be used to estimate the fission source distribution for the next generation. Both estimators use weight functions to compensate for the suppression of absorption.

For absorption estimator the number of particles per generation would decrease since the number of absorptions is smaller than the number of source particles due to the surface leakage. Moreover, if leakage is significant, this reduction would be so rapid it would cause $N$ to become unacceptably small before a fundamental mode distribution is reached.

For the collision estimator, the result will be that with each generation the number of source particles will have very small weight coefficients and after a few generations the number of particles would become exceedingly large.

As a rule, it is desirable to keep the number of particles in each generation about the same. This is done exactly by the absorption and collision estimators if the $x_n$ are divided by the current estimate of $k$ before the estimation of fission particle production.

Track length estimators are not well suited to determining the spatial distribution of fission for the next generation because they are not localized at specific space points. Though, it can provide a second and often almost independent estimate of the number of fission neutrons produced.

#### Error Evaluations

Error estimation in Monte Carlo eigenvalue calculations suffer from:

-  The finite number of histories $N$ per neutron generation

- The finite number of generations before the calculations is terminated.

If a large number of histories per generation is followed, the variance in the estimator is very small. However, the fundamental mode may not be reached in order to compute the multiplication factor. Lowing down the history to track more generations will provide reaching to te fundamental mode but the variance in the estimators will be large. To circumvent this difficulty one invariably averages values of the estimator over a number of generations is used to calculate the multiplication factor.

<br>

