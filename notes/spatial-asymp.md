## Asymptotics for modeling areal data

In classical statistics, asymptotic properties of estimators (our prototype here will be consistency) are relatively straightforward to establish: take $n$, the number of samples, to infinity and study what happens to the statistic in question.
However, in spatial settings, this task is not so straightforward.
For a continuous spatial domain (e.g., assessing the performance of a kriging estimator), this limit is well-defined: we can think of the limit n -> infinity as filling in the domain with infinite points and approximating the true surface of a variable.
However, the discrete case was giving me some trouble.
We usually treat areal data as possessing only one observation per unit, in which case the limit $n \rightarrow \infty$ implies either (a) the addition of more areal units or (b) some sort of refinement in the discretization.
(a) is practically nonsensical (there aren't more US counties to add to a countrywide analysis!) and (b) provokes severe MAUP problems. 
If there is only one observation of a variable per spatial unit, then what does it mean to take $n$ to infinity?

As a side note, sometimes spatial statisticians cover the case where areal units have multiple observations per unit.
Say unit $i$ has $n_i$ observations.
Then you could possibly limit $n_i \rightarrow \infty$ to achieve some asymptotic results.
I haven't tried this or seen examples of it in the literature, though.

Another potential way to think of the asymptotics might be to consider superpopulations, which can be thought of as alternate universes.
Suppose we're working with county data for all the counties in the US.
The infinite universes approach views this sample-population (as the sample equals the population here) as but one realization of some infinite set of maps of the US.
Essentially, this is a second-order population on top of the observed sample-population.
In this case, the choice of asymptotics has significant effects on the inference setting: if we interpret sets of spatial observations as coming from this second-order superpopulation, we are effectively doing inference over all possible observations of these variables across the US (de Gruijter and ter Braak, 1990; Ding et al., 2017).

After trawling through my spatial statistics textbooks, I eventually found the answer in Cressie (1993).
(As a side note, it's hard to understate how often this happens -- that I have a spatial stats question and find the answer in Cressie.
It's my handbook on spatial statistical thinking.)
Section 5.8 is all about infill asymptotics for continuous domains and Section 7.3.1 is all about increasing-domain asymptotics for areal data.
From his treatment of the two, infill asymptotics feels like a very natural study of asymptotic properties for the estimators, but increasing-domain asymptotics feels quite contrived.
In this sense, the superpopulation is an infinite domain of which we've merely selected a "large enough" subregion; e.g., an analysis on the counties of the US assumes that the US extends infinitely in at least one direction.

It turns out that the increasing-domain approach is actually how the results are formulated.
Section 7.3.1 of Cressie is very dense, but the result in question boils down to Theorems 2 and 3 of Mardia and Marshall (1984).
He begins by showing increasing-domain asymptotic results for spatial parameters, and then around the midpoint of the section makes a turn by saying: 

_"It is worth reiterating that all of these results are for spatial-dependence parameters; the mean of the process has been assumed known and hence, without loss of generality, assumed to be zero. Often, most of the interest centers on the unknown mean parameters; the spatial-dependence parameters are important, but only in terms of efficient estimation of the mean parameters."_

He continues to discuss a theorem (Mardia and Marshall, 1984) that proves consistency and asymptotic normality of maximum likelihood estimators for the mean and dependence parameters on an index set S, to which Cressie adds two assumptions that make it work in the spatial case.

**Theorem 2.** Consider a Gaussian spatial process $Y \sim N_n(X\beta, \Sigma)$ where $\beta \in \mathbb{R}^p$ are mean parameters and $\gamma \in \mathbb{R}^k$ are spatial parameters.
Let $\Sigma = \Sigma(\gamma)$ with eigenvalues $\lambda_1 \leq \dots \leq \lambda_n$, $\Sigma_i = \frac{\partial \Sigma}{\partial \gamma_i}$ with eigenvalues $|\lambda^i_1| \leq \dots \leq |\lambda^i_n|$, and $\Sigma_{ij} = \frac{\partial^2 \Sigma}{\partial \gamma_i \gamma_j}$ with eigenvalues $|\lambda^{ij}_1| \leq \dots \leq |\lambda^{ij}_n|$.
As $n \rightarrow \infty$, assume the following:
1. $\lambda\_n \rightarrow C < \infty$, $\|\lambda^i\_n\| \rightarrow C\_i < \infty$, and $\|\lambda^{ij}\_n\| \rightarrow C\_{ij} < \infty$ for all $i, j, = 1, \dots, p$.
1. There exists $\delta > 0$ such that $\|\Sigma_i\|_F^{-2} = O\left(n^{-\frac{1}{2} - \delta}\right)$ for each $i$.
1. Define $t_{ij}/2 = \frac{1}{2} \text{tr}(\Sigma^{-1}\Sigma_i\Sigma^{-1}\Sigma_j)$. Then $t_{ij}/(t_{ii}t_{jj})^{1/2} \rightarrow a_{ij}$ where $A = [a_{ij}]$ is a nonsingular matrix.
1. $(X^TX)^{-1} \rightarrow 0$.

Then the maximum likelihood estimators $\hat{\beta}_n$ and $\hat{\gamma}_n$ are weakly consistent and asymptotically Gaussian ($\hat{\eta}_n \sim N(\eta, J^{-1})$ where $\eta = (\beta, \gamma)$ and $J = -\mathbb{E}[L^{(2)}]$ is the expected information matrix).

There's a lot to unpack here, but bear with me for a little while longer. 
Theorem 3 of Mardia and Marshall adds two more assumptions that guarantee full consistency.
Cressie cites this as a corollary, but I think it's the main result here.

**Theorem 3.** Along with assumptions 3 and 4 of Theorem 2, assume the following:
<ol start="5">
<li>Let $D_n$ be the spatial domain with $n$ observations in it. For all $(s, s') \in D_n \times D_n$, $\|s - s'\| \geq a > 0$.</li>
<li>$Y$ is covariance stationary in $\mathbb{R}^d$, where $d$ is the dimension of the spatial domain (usually 2). That is, $C(s, s+h; \gamma) = \sigma^2\rho(h; \gamma)$ with $\rho(0; \gamma) = 1$.</li>
<li>Define $\rho\_i = \partial \rho/\partial \gamma\_i$ and $\rho\_{ij} = \partial^2 \rho / \partial \gamma\_i \partial \gamma\_j$. $\rho$, $\rho\_i$, and $\rho\_{ij}$ must be absolutely summable over $\mathbb{Z}^d$.</li>
</ol>

Then the maximum likelihood estimators of $\beta$ and $\gamma$ are consistent and asymptotically Gaussian.

I forgo presenting proofs here (see Mardia and Marshall, 1984 for that), opting instead to delve into the intuition for what these assumptions mean.
The information matrix for $\eta$ is $$
J = \begin{bmatrix} J_\beta & 0 \\ 0 & J_\gamma \end{bmatrix}
$$ (apologies for the wonky formatting, still figuring out MathJaX in Github Pages)
where $J_\beta = X^T\Sigma^{-1} X$ and $[J_\gamma]\_{ij} = \frac{1}{2}t\_{ij}$.
This contextualizes the role that the $t_{ij}$ play: they are exactly elements of the information matrix for $\gamma$ and hence assumption 3 ensures that $J^{-1}_\gamma$ is nonsingular in the limit.
That is, it guarantees that the elements of $\hat{\gamma}_n$ are "not asymptotically linearly dependent" (Mardia and Marshall, 1984).

Assumption 4 comes from the standard theory of normal linear models.
$\text{Var}(\hat{\beta}_n) = (X^TX)^{-1} \sigma^2$, so the assumption $(X^TX)^{-1} \rightarrow 0$ as $n \rightarrow \infty$ implies that information accumulates about $\beta$ as we gather more data.

Covariance stationarity (assumption 5) is something we practically always assume when doing spatial statistics.
I've yet to see a method that handles the case where the covariance of a spatial process is location-dependent.

Assumption 6 is more of a housekeeping assumption than anything else: it says that every new observation must be some distance away from the current set of observations.
This ensures that the domain truly expands in the limit.

Finally, assumption 7 tells us that the covariances decay properly with distance, essentially corresponding to [Tobler's First Law](https://en.wikipedia.org/wiki/Tobler%27s_first_law_of_geography).
Mardia and Marshall show that this is equivalent to assumption 1, which is good because assumption 7 is far more practical to check.
In conjunction with assumption 5, this says that new locations remain close enough to keep learning about the spatial parameters.
For example, if there's a cutoff in the covariance function beyond which $\rho(h; \gamma) = 0$, we won't learn anything about $\gamma$ if our observations are always spaced further than this cutoff.

Anyway, I have three conclusions to draw from this:
- Asymptotic results for areal statistics might be made far easier if we let there be multiple observations per unit.
- Modern asymptotic and inferential results for areal statistics are predicated on the increasing domain idea.
- Always, always, always start with Cressie. (I thought I learned this one already!)

However, I'm still left wondering about what practical conditions make these theorems applicable, and how badly the results perform when the conditions aren't satisfied!
I think the next step is some large sample approximations/experiments or digging deeper into the theorem to see how each condition comes into play and what it affects.
Moreover, what implications does this have on inference? 
One of these references comes from causal inference, which is why I started thinking about this in the first place.
To me, considering a sample as but one of infinite alternate universes makes far more sense than considering each sample as a subset of an infinite domain that has the same spatial structure in all directions.
I wonder if it's possible to build theory around the former rather than the latter: could we reexpress these results in the sense of a superpopulation of infinite universes and get a better setting for inference?


### References

Cressie, N. (1993). _Statistics for Spatial Data_. Wiley Series in Probability and Mathematical Statistics.

Ding, P., Li, X., and Miratrix, L.W. (2017). "Bridging finite and super population causal inference." _Journal of Causal Inference_, 5(2):1--8.

De Gruijter, J.J. and ter Braak, C.J.F. (1990). "Model-free estimation from spatial samples: A reappraisal of classical sampling theory." _Mathematical Geology_, 22(4):407--415.

Mardia, K.V. and Marshall, R.J. (1984). "Maximum likelihood estimation of models for residual covariance in spatial regression." _Biometrika_, 71:135--146.

