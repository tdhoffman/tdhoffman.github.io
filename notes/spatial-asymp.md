## Asymptotics for modeling areal data

_These notes are a work in progress: I am transferring the jumble of thoughts from paper to a polished version here.
The beginnings of the motivation and the final punchline have been written, mostly because I was communicating these ideas to colleagues and had portions of that text ready to go when I decided to write these notes up._

In classical statistics, asymptotic properties of estimators (our prototype here will be consistency) are relatively straightforward to establish: take $n$, the number of samples, to infinity and study what happens to the statistic in question.
However, in spatial settings, this task is not so straightforward.
If there is only one observation of a variable per spatial unit, then what does it mean to take $n$ to infinity?

Initially, I thought I couldn't find the answer to this in any of my textbooks, but it turns out that was wrong -- I didn't look in the one textbook I should've started with, Cressie (1993). 
Section 5.8 is all about infill asymptotics for continuous domains and Section 7.3.1 is all about increasing-domain asymptotics for areal data.
From his treatment of the two, infill asymptotics feels like a very natural study of asymptotic properties for the estimators, but increasing-domain asymptotics feels quite contrived.
In this sense, the superpopulation is an infinite domain of which we've merely selected a "large enough" subregion; e.g., an analysis on the counties of the US assumes that the US extends infinitely in at least one direction.

It turns out .... **Work in progress**. This section will follow Cressie's section 7.3.1.

Moreover, Cressie says:

_"It is worth reiterating that all of these results are for spatial-dependence parameters; the mean of the process has been assumed known and hence, without loss of generality, assumed to be zero. Often, most of the interest centers on the unknown mean parameters; the spatial-dependence parameters are important, but only in terms of efficient estimation of the mean parameters."_

He continues to discuss a theorem (Mardia and Marshall, 1984) that proves consistency and asymptotic normality of maximum likelihood estimators for the mean and dependence parameters on an index set S, to which Cressie adds two assumptions that make it work in the spatial case.

De Gruijter's model-based approach seems to hint at another way to construct superpopulations, which I'll call "infinite universes". Suppose we're working with county data for all the counties in the US. The infinite universes approach views this sample-population (as the sample equals the population here) as but one realization of some infinite set of maps of the US. Essentially, this is a second-order population on top of the observed sample-population. I might poke around to see if there's more literature in that thread.

Anyway, I have three conclusions to draw from this:
- Asymptotic results for areal statistics are made far easier if we let there be multiple observations per unit.
- Modern asymptotic results for areal statistics are predicated on the increasing domain idea.
- Always, always, always start with Cressie. (I thought I learned this one already!)

However, I'm still left wondering about what practical conditions make these theorems applicable, and how badly the results perform when the conditions aren't satisfied!
I think the next step is some large sample approximations/experiments or digging deeper into the theorem to see how each condition comes into play and what it affects.


### References

Cressie, N. (1993). _Statistics for Spatial Data_. Wiley Series in Probability and Mathematical Statistics.

Ding, P., Li, X., and Miratrix, L.W. (2017). "Bridging finite and super population causal inference." _Journal of Causal Inference_, 5(2):1--8.

De Gruijter, J.J. and ter Braak, C.J.F. (1990). "Model-free estimation from spatial samples: A reappraisal of classical sampling theory." _Mathematical Geology_, 22(4):407--415.

Mardia, K.V. and Marshall, R.J. (1984). "Maximum likelihood estimation of models for residual covariance in spatial regression." _Biometrika_, 71:135--146.

