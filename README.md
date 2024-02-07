# Physics-Informed Neural Networks for Physics of Earthquakes
Rassi et al. [1] introduced a method called Physics-informed Neural Networks (PINNs) for solving forward and inverse partial differential equations. Through automatic differentiation, PINNs enable the imposition of physical laws into the objective function.
We investigate emergent dynamics at earthquake fault motion using slip law formulation of nonlinear rate-and-state friction law attached to Burridge-Knopoff spring-block model. This simple system serves as a foundation to understand and predict the dynamic behavior of physical systems. We proposed approaches for both forward and inverse problems. Our primary objectives are:
(1) to predict slip evolution of a single spring-block model coupling with rate-and-state friction law using forward PINN 
(2) to estimate a constant frictional parameter via time-independent inverse PINN 
(3) to estimate evolution of friction force through time-dependent inverse PINN 
(4) to estimate the material properties of fault determining the instability of the fault.
# Installation

# Bibliography
[1] Maziar Raissi, Paris Perdikaris, and George Em Karniadakis. Physics Informed Deep Learning (Part I): Data-driven Solutions of Nonlinear Partial Differential Equations. http://arxiv.org/pdf/1711.10561v1
[3] Lu Lu et al. DeepXDE: A deep learning library for solving differential equations.2019. https://arxiv.org/abs/1907.04502
