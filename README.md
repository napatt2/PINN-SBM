# Physics-Informed Neural Networks for Physics of Earthquakes
Rassi et al. [1] introduced a method called Physics-informed Neural Networks (PINNs) for solving forward and inverse partial differential equations. Through automatic differentiation, PINNs enable the imposition of physical laws into the objective function.

![BK](https://github.com/napatt2/PINN-SBM/assets/106395611/79fa0712-9a47-44e4-a56b-39e2e2b38ea8)

We investigate emergent dynamics at earthquake fault motion using slip law formulation of nonlinear rate-and-state friction law attached to Burridge-Knopoff spring-block model. This simple system serves as a foundation to understand and predict the dynamic behavior of physical systems. We proposed approaches for both forward and inverse problems. Our primary objectives are:

1. to predict slip evolution of a single spring-block model coupling with rate-and-state friction law using forward PINN 
2. to estimate a constant frictional parameter via time-independent inverse PINN 
3. to estimate evolution of friction force through time-dependent inverse PINN 
4. to estimate the material properties of fault determining the instability of the fault.
# Installation
All required packages are listed as follows:
```
matplotlib
numpy
scikit-learn
scikit-optimize>=0.9.0
scipy
pandas
deepxde
```
This repository requires the installation of [DeepXDE](https://deepxde.readthedocs.io/en/latest/) [2]. Each problem's code is standalone and can be run individually using Jupyter Notebook.

# Usage
- [Forward_adaptive_loss.ipynb](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/PINN_SBM/Forward_adaptive_loss.ipynb) predicts the slip evolution of a single block using an adaptive time-stepping scheme based on loss. The time step is chosen such that the loss falls below a predefined threshold. This model does not involve any observations.
- [Forward_adaptive_mse.ipynb](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/PINN_SBM/Forward_adaptive_mse.ipynb) predicts the slip evolution of a single block through an adaptive time-stepping approach relying on the mean squared error (MSE) of predictions. Like the previous model, it does not incorporate any observations.
- [Forward_with_data.ipynb](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/PINN_SBM/Forward_with_data.ipynb) predicts the slip evolution of a single block and incorporates observations, which are available [here](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/Dataset/sbm1.csv).
- [Inverse_friction_evolution.ipynb](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/PINN_SBM/Inverse_friction_evolution.ipynb)  estimates the evolution of friction force based on the dataset of slip and slip rate, available [here](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/Dataset/sbm_inv.csv).
- [Inverse_kappa.ipynb](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/PINN_SBM/Inverse_kappa.ipynb) estimates a constant frictional parameter $\kappa$, given the observations of slip, slip rate, and state variable. The dataset can be found [here](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/Dataset/sbm1.csv).
- [Inverse_10_blocks.ipynb](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/PINN_SBM/Inverse_10_blocks.ipynb) estimates the material properties $\epsilon$ of each block in a series of 10 blocks, which determine the stability of the fault to earthquakes. We utilize the observations, available [here](https://github.com/napatt2/PINN-SBM/blob/af88cf450e15d185849296593c39f3a9152d321a/Dataset/sbm10.csv).

# Bibliography
[1] Maziar Raissi, Paris Perdikaris, and George Em Karniadakis. Physics Informed Deep Learning (Part I): Data-driven Solutions of Nonlinear Partial Differential Equations. http://arxiv.org/pdf/1711.10561v1

[2] Lu Lu et al. DeepXDE: A deep learning library for solving differential equations.2019. https://arxiv.org/abs/1907.04502
