# QuakeNN
Rassi et al. [1] introduced a method called Physics-informed Neural Networks (PINNs) for solving forward and inverse partial differential equations. Through automatic differentiation, PINNs enable the imposition of physical laws into the objective function.

![BK](https://github.com/napatt2/PINN-SBM/assets/106395611/79fa0712-9a47-44e4-a56b-39e2e2b38ea8)

We investigate emergent dynamics at earthquake fault motion using slip law formulation of nonlinear rate-and-state friction law attached to Burridge-Knopoff spring-block model. This simple system serves as a foundation to understand and predict the dynamic behavior of physical systems. We proposed approaches for both forward and inverse problems. Our primary objectives are:

1. to predict slip evolution of a single spring-block model coupling with rate-and-state friction law using forward PINN 
2. to estimate a constant frictional parameter via time-independent inverse PINN 
3. to estimate evolution of friction force through time-dependent inverse PINN 
4. to estimate the material properties of fault determining the instability of the fault.

We also investigate the forward and inverse problems of the acoustic and vector wave equations in 2D. The primary goals are as follows:
1. to predict the solution of the acoustic wave equation in 2D space
2. to estimate the wave speed of the acoustic 2D wave equation, given the solution of the wave equation
3. to predict the solution of the vector wave equation
4. to estimate the material properties in the vector wave equation, given the measurements of displacement

# Getting Started
This software tool uses Python language. All required packages are listed as follows:
```
matplotlib
numpy
scikit-learn
scikit-optimize>=0.9.0
scipy
pandas
deepxde
```
This repository requires the installation of [DeepXDE](https://deepxde.readthedocs.io/en/latest/) [2]. Each problem's code is standalone and can be run individually using Jupyter Notebook. The line ```!pip install deepxde``` in the code is intended for Google Colab, users shall comment it out if using other platforms. Please ensure that the dataset path is correctly specified and that the data file is available at that location. If you are using Google Colab, you may need to upload the dataset manually and adjust the file path accordingly.

# Running QuakeNN
The user can execute the entire code from start to finish. It combines all steps, including data preprocessing, model training, and making predictions, all within a single code. The equation used in each model is written in the code. This code takes approximately 5-10 minutes to run using GPU A100. However, it can take hours for the forward adaptive time-stepping scheme. Here are the description of each code:
- [Forward_adaptive_loss.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Fault%20Friction/Forward_adaptive_loss.ipynb) predicts the slip evolution of a single block in spring block model using an adaptive time-stepping scheme based on loss. The time step is chosen such that the loss falls below a predefined threshold. This model does not involve any observations. The outputs from the model are $v$, $A$, and $\theta$. The flow chart of this scheme is shown in the figure below.
  ![loss_flowchart](https://github.com/napatt2/PINN-SBM/assets/106395611/79ca5baa-aebc-4bba-bbc1-e973bf0da49c)
- [Forward_adaptive_mse.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Fault%20Friction/Forward_adaptive_mse.ipynb) predicts the slip evolution of a single block through an adaptive time-stepping approach relying on the mean squared error (MSE) of predictions. Like the previous model, it does not incorporate any observations. The outputs from the model are $v$, $A$, and $\theta$. The flow chart of this scheme is shown in the figure below.
  ![mse_flowchart](https://github.com/napatt2/PINN-SBM/assets/106395611/ab0b8ec4-6fd4-45db-b242-0a67abb53e0f)
- [Forward_with_data.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Fault%20Friction/Forward_with_data.ipynb) predicts the slip evolution of a single block and incorporates observations, which are available [here](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Dataset/sbm1.csv). The outputs from the model are $\tilde{u}$, $\tilde{v}$, and $\tilde{\theta}$.
- [Inverse_friction_evolution.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Fault%20Friction/Inverse_friction_evolution.ipynb)  estimates the evolution of friction force of a single block based on the dataset of slip and slip rate, available [here](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Dataset/sbm_inv.csv). The predictions from neural networks consists of $\tilde{u}$, $\tilde{v}$, and $\tau$.
- [Inverse_kappa.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Fault%20Friction/Inverse_kappa.ipynb) estimates an elastic property $\kappa$, given the observations of slip, slip rate, and state variable of a single block in a spring block model. The dataset can be found [here](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Dataset/sbm1.csv). The estimation of $\kappa$ can be found in file ```variables.dat``` which is generated during the training. The outputs from neural networks are $\tilde{u}$, $\tilde{v}$, and $\tilde{\theta}$.
- [Inverse_10_blocks.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Fault%20Friction/Inverse_10_blocks.ipynb) estimates the material properties $\epsilon$ of each block in a series of 10 blocks, which determine the stability of the fault to earthquakes. We utilize the observations, available [here](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Dataset/sbm10.csv). The predicted parameter $\epsilon$ is in file ```variables.dat```. Moreover, the model also outputs $\tilde{u}$, $\tilde{v}$, and $\tilde{\theta}$ of each block.
- [Forward_acoustic_wave.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Wave%20Equation/Forward_acoustic_wave.ipynb) predicts the solution of acoustic wave equation in 2D without any observational data.
- [Forward_vector_wave.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Wave%20Equation/Forward_vector_wave.ipynb) predicts the solution of vector wave equation in elastic 2D. We do not apply any measurements here.
- [Inverse_acoustic_wave.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Wave%20Equation/Inverse_acoustic_wave.ipynb) identifies the wave speed of acoustic wave equation using the dataset of the solution of acoustic wave equation [here](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Dataset/acoustic_c3.mat). The estimation of wave speed can be found in file ```variables.dat``` which is generated during the training.
- [Inverse_vector_wave.ipynb](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Wave%20Equation/Inverse_vector_wave.ipynb) estimates material properties, given the dataset of vector wave solution [here](https://github.com/napatt2/QuakeNN/blob/7761597689de67dacf46145a42632e403d8a34f4/Dataset/vector_2nd.mat). The estimation of material properties can be found in file ```variables.dat``` which is generated during the training.
# References
[1] Maziar Raissi, Paris Perdikaris, and George Em Karniadakis. Physics Informed Deep Learning (Part I): Data-driven Solutions of Nonlinear Partial Differential Equations. http://arxiv.org/pdf/1711.10561v1

[2] Lu Lu et al. DeepXDE: A deep learning library for solving differential equations.2019. https://arxiv.org/abs/1907.04502

[3] Wang Sifan, Hanwen Wang, and Paris Perdikaris. On the eigenvector bias of Fourier feature networks: From regression to solving multi-scale PDEs with physics-informed neural networks. https://doi.org/10.1016/j.cma.2021.113938
