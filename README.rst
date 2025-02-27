===============================
Accelerating MCMC with Optimal Transport and Invertible Neural Networks
===============================

This repository stems from my recent research on accelerating Markov Chain Monte Carlo (MCMC) sampling using transport-map proposals. The method leverages **Optimal Transport Theory** to train an **Invertible Neural Network (INN)** that learns a mapping between a complex target distribution and a simpler reference distribution, such as a multivariate standard Gaussian. By drawing samples in the reference space and mapping them back onto the target space, the approach enables more efficient proposals in a **Metropolis-Hastings algorithm**.

**Note:** A paper detailing this work is in preparation, and the Python codes associated with this repository will be made public upon submission.


The following abstract was submitted to **EGU General Assembly 2025**:


=========================================================
Transport-map proposals for efficient MCMC sampling
=========================================================

**Fabrizio Magrini** :sup:`1` and **Malcolm Sambridge** :sup:`1`  

:sup:`1` Australian National University, Research School of Earth Sciences, ACT, Australia

----

**Abstract**  
Knowledge of the Earth's interior relies on indirect information collected at or near the surface. Typically, data do not uniquely constrain the subsurface properties and are contaminated by noise, and therefore the solution of ill-posed inverse problems is required. Geophysicists have traditionally addressed such problems through deterministic approaches, seeking a single 'best-fitting' model defined by optimality criteria that reflect our understanding of the problem at hand. In recent decades, Bayesian approaches have become increasingly common, as they characterise the posterior probability distribution of the model conditioned on the observations, thereby quantifying uncertainty.

In this context, Markov chain Monte Carlo (MCMC) methods have emerged as a crucial tool as they allow sampling from posterior distributions of arbitrary complexity. At the core of many MCMC algorithms lies the Metropolis-Hastings scheme. This combines a proposal distribution with a probabilistic acceptance criterion to construct a Markov chain that has the desired target distribution as its stationary distribution. The algorithm is versatile as it rests on mild technical conditions on the proposal, and is thus widely adopted across a broad range of geoscientific inference problems. Yet when the parameter space is large or the forward models are computationally expensive---both common scenarios in geophysical applications---it can become inefficient, resulting in poor chain mixing and slow convergence to the target (posterior) distribution. These challenges underscore the importance of effective proposal mechanisms.

In this presentation, we introduce a novel approach to designing Metropolis-Hastings proposals based on adaptive transport maps. The framework is inspired by recent developments from the field of Applied Mathematics linking Bayesian inference with Optimal Transport theory. The idea is to find a monotone, nonlinear transformation to recast a (complex) target probability distribution into a (simpler) reference distribution that is more amenable to standard MCMC steps. Our key contribution is to parameterise these transformations using invertible neural networks, ensuring monotonicity while gaining the flexibility and expressiveness that neural architectures afford.

The proposed method progresses iteratively. We begin with a standard sampling strategy (e.g., a random-walk Metropolis) to obtain initial draws from the target distribution. These samples inform the training of an invertible neural network that learns to map from the target to a simpler reference distribution, specifically a standard (multivariate) Gaussian. Subsequent proposals are then generated in the reference space, either as global independence moves or local perturbations, and are accepted or rejected following a suitably modified Metropolis-Hastings criterion. As more samples accumulate, the network's parameters are updated, improving overall sampling efficiency. Ultimately, the approach yields not only an ensemble of samples representative of the desired target distribution---just as in standard MCMC---but also a compact, learned representation of it in the network's weights.

We illustrate the proposed paradigm both theoretically and through examples. Preliminary results indicate that transport-map-enhanced MCMC has the potential to significantly accelerate Bayesian sampling across a range of applications.

We illustrate the proposed paradigm both theoretically and through examples. Preliminary results indicate that transport-map-enhanced MCMC has the potential to significantly accelerate Bayesian sampling across a range of applications.
