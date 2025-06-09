# Interferometer_NN

# 1.Introduction

**A programmable N-channel interferometer** is a waveguide structure equipped with tunable phase shifters that adjust the phase values in the device's channels and beam splitters that redistribute optical radiation between the channels.

Using a set of phase shifters **ϕ**, a specific **N×N unitary transformation matrix U(ϕ)** can be programmed and applied to the input vector of the light field's amplitudes, yielding the result of matrix-vector multiplication.

Our goal is to develop a **digital model of the optical chip** on a computer, which will then be used to determine the required phase shifts **ϕ** for programming a given unitary transformation **U(ϕ)**.

# 2.Physical Model of 1-Layer Universal Robust Interferometer

We registered 1000 EEMs corresponding to CD's aqueous suspensions with one, two and three cation types Cu<sup>2+</sup>, Ni<sup>2+</sup>, Cr<sup>3+</sup>.
![plot](https://github.com/oesarmanova/CD_HM_sensor/blob/main/sample_1.png)
![plot](https://github.com/oesarmanova/CD_HM_sensor/blob/main/sample_3_comp.png)

The Figure above shows EEM. Up: CD suspension without cations. Down: CD suspension with three cations.

Each row in the matrix represents a fluorescence spectra at particular excitation wavlengths and comprises 500 spectral channels. Each column in the matrix represents excitation spectra registered in a particular spectral channel and comprises 41 channels. Thus, initial data represents 2D arrays of (41x500) size.

The dataset comprises 27 single-component suspensions (i.e. suspensions, containing 1 cation type), 240 double-component suspensions (containing 2 cation types), and 732 triple-component suspensions. One sample corresponds to the case when all the cations are not present in the suspension.

The dataset is present here https://github.com/oesarmanova/CD_HM_sensor/tree/main/CD_HM_dataset.

# 2.Training Approaches

Multilayer Perceptrons (MLP)

| Approach  | Wavelength of FL Excitation | Sample size |
| --- | --- | --- |
| MLP_1W  | 350 nm  | (1x500) |
| MLP_3W  | 250, 350, 450 nm  | (1x1500) |
| MLP_41W  | 41 wavelengths in range 250 – 450 nm with 5 nm increment | (1x20500) |

Convolutional neural networks (CNN)

| Approach  | Number of channels | Sample size |
| --- | --- | --- |
| CNN_1D  | 41  | (41x1x500) |
| CNN_2D  | 1  | (1x41x500) |

# 3.Code files

Run in Colab

CD_HM_2D_CNN.ipnb - use to train 2D CNN

CD_HM_1D_CNN.ipnb - use to train 1D CNN

CD_HM_MLP.ipnb - use to train MLPs (MLP_1W, MLP_3W, MLP_41W)

Get_statistics.ipnb - use to get statistics of the model performance
