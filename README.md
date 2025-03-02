# Accelerating MCMC with Optimal Transport and Invertible Neural Networks


This repository stems from my recent research on accelerating **Markov Chain Monte Carlo (MCMC) sampling** using transport-map proposals. The method leverages **Optimal Transport Theory** to train an **Invertible Neural Network** that learns a mapping between a complex target distribution and a simpler reference distribution, such as a multivariate standard  Gaussian (see Fig. 1). At each Markov chain step, samples are drawn in the reference space, mapped back onto the target space via the inverse transport map, and accepted or rejected based on a modified Metropolis-Hastings criterion. Preliminary results indicate that this approach is robust and enables **more efficient proposals** compared to baseline MCMC methods.

> **Note:** A paper detailing this work is in preparation, and the Python codes associated with this repository will be made public upon submission.

![Bayesian MCMC with Transport Maps](figures/banner.png)
*Figure 1: The transport map T transforms points from the complex target distribution π(θ) to the simpler reference distribution ρ(r).*

---

# Abstract submitted to EGU General Assembly 2025

### Transport-map proposals for efficient MCMC sampling

**Fabrizio Magrini¹** and **Malcolm Sambridge¹**  

¹ Australian National University, Research School of Earth Sciences, ACT, Australia  
  
Knowledge of the Earth's interior relies on indirect information collected at or near the surface. Typically, data do not uniquely constrain the subsurface properties and are contaminated by noise, and therefore the solution of ill-posed inverse problems is required. Geophysicists have traditionally addressed such problems through deterministic approaches, seeking a single 'best-fitting' model defined by optimality criteria that reflect our understanding of the problem at hand. In recent decades, Bayesian approaches have become increasingly common, as they characterise the posterior probability distribution of the model conditioned on the observations, thereby quantifying uncertainty.

In this context, Markov chain Monte Carlo (MCMC) methods have emerged as a crucial tool as they allow sampling from posterior distributions of arbitrary complexity. At the core of many MCMC algorithms lies the Metropolis-Hastings scheme. This combines a proposal distribution with a probabilistic acceptance criterion to construct a Markov chain that has the desired target distribution as its stationary distribution. The algorithm is versatile as it rests on mild technical conditions on the proposal, and is thus widely adopted across a broad range of geoscientific inference problems. Yet when the parameter space is large or the forward models are computationally expensive---both common scenarios in geophysical applications---it can become inefficient, resulting in poor chain mixing and slow convergence to the target (posterior) distribution. These challenges underscore the importance of effective proposal mechanisms.

In this presentation, we introduce a novel approach to designing Metropolis-Hastings proposals based on adaptive transport maps. The framework is inspired by recent developments from the field of Applied Mathematics linking Bayesian inference with Optimal Transport theory. The idea is to find a monotone, nonlinear transformation to recast a (complex) target probability distribution into a (simpler) reference distribution that is more amenable to standard MCMC steps. Our key contribution is to parameterise these transformations using invertible neural networks, ensuring monotonicity while gaining the flexibility and expressiveness that neural architectures afford.

The proposed method progresses iteratively. We begin with a standard sampling strategy (e.g., a random-walk Metropolis) to obtain initial draws from the target distribution. These samples inform the training of an invertible neural network that learns to map from the target to a simpler reference distribution, specifically a standard (multivariate) Gaussian. Subsequent proposals are then generated in the reference space, either as global independence moves or local perturbations, and are accepted or rejected following a suitably modified Metropolis-Hastings criterion. As more samples accumulate, the network's parameters are updated, improving overall sampling efficiency. Ultimately, the approach yields not only an ensemble of samples representative of the desired target distribution---just as in standard MCMC---but also a compact, learned representation of it in the network's weights.

We illustrate the proposed paradigm both theoretically and through examples. Preliminary results indicate that transport-map-enhanced MCMC has the potential to significantly accelerate Bayesian sampling across a range of applications.


----

# Gallery

![Bayesian MCMC with Transport Maps](figures/local_proposals.png)
*Figure 2: Simple proposal distributions in the reference space (left) and their transformed counterparts in the target space (right) under the transport map. The resulting distributions enable efficient MCMC sampling.*

![Bayesian MCMC with Transport Maps](figures/tmap_samples_udpates.png)
*Figure 3: Iterative MCMC sampling. A transport map T₁ is first derived from 50 samples obtained via baseline MCMC (a). This map is then used to propose new MCMC samples in the reference space (see Fig. 2), with the transformed samples shown in (b). The transport map is updated iteratively, leading to improved sampling efficiency (panels c–f). Notably, MCMC acceptance rate increases sharply from ~33% to ~67% when reference proposals are introduced (see statistics in panels a and b).*

![Bayesian MCMC with Transport Maps](figures/tmap_pullback_udpates.png)*Figure 4: Evolution of the pullback density 𝜋̃ₖ induced by the transport map Tₖ over successive updates (corresponding to those in Fig. 3). Note how 𝜋̃ₖ progressively approaches the true target density 𝜋, leading to increasingly efficient proposals.*



![Bayesian MCMC with Transport Maps](figures/tmap_pullback_vs_true_posterior.png)*Figure 5: Comparison between the true posterior 𝜋 (center), the pullback density 𝜋̃₆ (left) induced by the transport map T₆ from Fig. 4f, and their pointwise difference (right).*


