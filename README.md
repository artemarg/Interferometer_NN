# Interferometer_NN

# 1.Introduction

**A programmable N-channel interferometer** is a waveguide structure equipped with tunable phase shifters that adjust the phase values in the device's channels and beam splitters that redistribute optical radiation between the channels.

Using a set of phase shifters **ϕ**, a specific **N×N unitary transformation matrix U(ϕ)** can be programmed and applied to the input vector of the light field's amplitudes, yielding the result of matrix-vector multiplication.

Our goal is to develop a **digital model of the optical chip** on a computer, which will then be used to determine the required phase shifts **ϕ** for programming a given unitary transformation **U(ϕ)**.
![plot](https://github.com/artemarg/Interferometer_NN/blob/main/png_files/msuai1.PNG)
# 2.Physical Model of 1-Layer Universal Robust Interferometer

The physical model of the interferometer is represented as a product of **unitary matrices** describing the individual components of the linear optical scheme: a layer of three phase shifters $P(\theta_{1-3})$ and mixing layers—multichannel beam splitters M₁ and M₂. The unitary matrices depended on trainable physical parameters. In total, the model contained 34 trainable physical parameters.
![plot](https://github.com/artemarg/Interferometer_NN/blob/main/png_files/msuai41.PNG)
# Dataset Description
Go to the link in the Physical_1_Layer folder
## Folder Structure
Calibration_Data_One_Layer_925_nm/
├── channel_1/

│ ├── ch1_H1.txt

│ ├── ch1_H2.txt

│ └── ch1_H3.txt

├── channel_2/

│ ├── ch2_H1.txt

│ ├── ch2_H2.txt

│ └── ch2_H3.txt

├── channel_3/

│ ├── ch3_H1.txt

│ ├── ch3_H2.txt

│ └── ch3_H3.txt

└── channel_4/

├── ch4_H1.txt

├── ch4_H2.txt

└── ch4_H3.txt



## Naming Convention

- **Folder names** `channel_X` indicate the input channel number (1-4) where:
  - `X` = channel number where laser radiation was injected

- **File names** `ch[i]_H[j].txt` represent:
  - `i` = input channel number (matches folder number)
  - `j` = heating element number (1-3)

## Experimental Setup

| Parameter          | Description                          |
|--------------------|--------------------------------------|
| Radiation input    | Directed to channel specified by `i` |
| Current injection  | Applied to heating element `j` with values ranging from **0 to 1300 a.u.** with **10 a.u.** step |
| Output intensities       | Recorded in corresponding text file |

> **Note:** The "a.u." stands for arbitrary units of current applied to heating elements.

R² was used as the metric

Run in Colab

PhysicalModel_1_Layer.ipynb
# 3.Physical Model of 3-Layer Universal Robust Interferometer

The physical model of the interferometer is represented as a product of **unitary matrices** describing the individual components of the linear optical scheme: 3 layers of 3 phase shifters $P_1(\theta_{1-3}),P_2(\theta_{4-6}),P_3(\theta_{7-9})$ and 4 mixing layers—multichannel beam splitters $M_1,M_2,M_3,M_4$. The unitary matrices depended on trainable physical parameters. In total, the model contained 72 trainable physical parameters.
![plot](https://github.com/artemarg/Interferometer_NN/blob/main/png_files/msuai3.PNG)
# Dataset Description
Go to the link in the Physical_3_Layers folder
## Folder Structure
2024_10_16_980_Calibration/
├── input_1/

│ ├── ch1_H1.txt

│ ├── ...

│ └── ch1_H9.txt

├── input_2/

│ ├── ch2_H1.txt

│ ├── ...

│ └── ch2_H9.txt

├── input_3/

│ ├── ch3_H1.txt

│ ├── ...

│ └── ch3_H9.txt

└── input_4/

├── ch4_H1.txt

├── ...

└── ch4_H9.txt



## Naming Convention

- **Folder names** `channel_X` indicate the input channel number (1-4) where:
  - `X` = channel number where laser radiation was injected

- **File names** `ch[i]_H[j].txt` represent:
  - `i` = input channel number (matches folder number)
  - `j` = heating element number (1-9)

## Experimental Setup

| Parameter          | Description                          |
|--------------------|--------------------------------------|
| Radiation input    | Directed to channel specified by `i` |
| Current injection  | Applied to heating element `j` with values ranging from **0 to 1500 a.u.** with **10 a.u.** step |
| Output intensities       | Recorded in corresponding text file |

R² was used as the metric

Run in Colab

PhysicalModel_3_Layers.ipynb

# 4.Neural Network Model of 1-Layer Universal Robust Interferometer

## Dataset Generation
An artificial dataset was first created using the physical model described in Section 2.

### Input Features:
- Channel number
- Random triplets of heating element currents

### Output:
- 4 normalized output intensities

### Evaluation Metric:
Fidelity between the interferometer's transfer matrices

## Experimental Setup

The study compared three distinct neural network approaches:
1. **Baseline Model** - Conventional architecture serving as reference
2. **ResNet** - Residual network with skip connections
3. **Transformer** - Self-attention based model
   
![plot](https://github.com/artemarg/Interferometer_NN/blob/main/png_files/msuai5.PNG)
## Training Results

| Dataset Size | Baseline | Transformer | ResNet |
|-------------|----------|-------------|-----------|
| 500 matrices | 0.920 | 0.950 | 0.947 |
| 2000 matrices | 0.954 | 0.989 | 0.988 |
| 5000 matrices | 0.965 | 0.994 | 0.994 |

*Table: Average fidelity scores across different dataset sizes and models*

Run in Colab

Neural_1_Layer.ipynb
# 5.Reconstruction of 40 Physical Parameters in Clements Chip Using Neural Networks
![plot](https://github.com/artemarg/Interferometer_NN/blob/main/png_files/msuai7.PNG)
## Dataset Generation
We generated an artificial dataset containing:
- 400 unique Clements Chips with different sets of 40 physical parameters $R,\alpha,\phi_0,T_{out}$
- 400 random current configurations

### Physical Model Simulation:
- **Input**: 
  - Random current configuration
  - 40 physical chip parameters
- **Output**: 
  - Transfer matrix

## Neural Network Training
We trained a Transformer network to solve the inverse problem:
- **Input**:
  - Random current configuration
  - Transfer matrix
- **Output**:
  - 40 reconstructed physical chip parameters
  
Run in Colab

Clements_40_parameters.ipynb
## Training Results
![plot](https://github.com/artemarg/Interferometer_NN/blob/main/png_files/msuai6.PNG)
