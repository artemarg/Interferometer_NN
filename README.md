# Interferometer_NN

# 0.Experiment

We prepared aqueous suspensions of CDs with fixed concentration (8 mg/L) comprising heavy metal ions Cu<sup>2+</sup>, Ni<sup>2+</sup>, Cr<sup>3+</sup> with concentrations varying from 0 to 4.95 mM with 0.55 mM increment. For that pupose we added Cu(NO<sub>3</sub>)<sub>2</sub> , Ni(NO<sub>3</sub>)<sub>2</sub> , Cr(NO<sub>3</sub>)<sub>3</sub> salts to the CD-suspension in such quantities that Cu<sup>2+</sup>, Ni<sup>2+</sup>, Cr<sup>3+</sup> cations were present in the suspensions in desired concentrations.
Totally, 1000 suspensions were prepared.

We used Shimadzu RF-6000 spectrofluorimeter to register excitation-emission matrices (EEM) of CD's aqueous suspensions in the presence of heavy metal ions. Fluorescensce signal was excited under radiation with wavelengths ranging from 250 to 450 nm with 5 nm increment - that is 41 excitation wavelengths. Each fluorescence spectrum was registered in a range from 250 to 750 nm with 1 nm increment - that is 500 spectral channels.

# 1.Dataset

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
