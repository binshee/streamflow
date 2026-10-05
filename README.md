# Streamflow Forecasting Using ANN and LSTM

## 1. Problem Statement

Streamflow forecasting is important for water-resource management, flood prediction, and hydrological planning. This project investigates the use of Artificial Neural Networks (ANN) and Long Short-Term Memory (LSTM) networks to forecast streamflow using historical rainfall and streamflow observations.

The project is based on the methodology of the reference paper, which models current streamflow as a function of previous rainfall and streamflow values.

## 2. Dataset

The dataset contains daily rainfall and streamflow observations for the period 2003–2012.

- Training period: 2003–2007
- Validation period: 2008–2012
- Input variables: Historical rainfall and streamflow
- Rainfall: converted to inches/day
- Streamflow: measured in cubic feet per second (cfs)
- Missing rainfall values were forward-filled.
- Lag features were created using the previous 3 rainfall and 3 streamflow observations.
- The normalization ranges follow the reference methodology.

## 3. Methodology

The project follows these steps:

1. Load and preprocess the rainfall and streamflow data.
2. Split the data into training (2003–2007) and validation (2008–2012).
3. Normalize the input and target values.
4. Generate lag-based features from historical rainfall and streamflow.
5. Train an ANN model.
6. Train an LSTM model using sequential lagged inputs.
7. Generate streamflow predictions for the validation period.
8. Compare the models using RMSE, MAE, and R².
9. Perform peak and non-peak streamflow analysis.
10. Study ANN hyperparameters such as hidden-layer size and learning rate.

## 4. Models

### Artificial Neural Network

The ANN consists of:

- Input layer
- Dense hidden layer with ReLU activation
- Output layer with linear activation
- Adam optimizer
- Learning rate: 0.001
- Hidden units: 32
- Epochs: 30
- Batch size: 32

### LSTM

The LSTM receives the lagged rainfall and streamflow observations as sequential input and uses an LSTM layer followed by a linear output layer for streamflow prediction.

## 5. Evaluation

The models were evaluated using:

- RMSE – Root Mean Squared Error
- MAE – Mean Absolute Error
- R² – Coefficient of Determination

Peak and non-peak performance was also evaluated using a streamflow threshold of 1500 cfs.

## 6. Results

### Overall Performance

| Model | RMSE (cfs) | MAE (cfs) | R² |
|---|---:|---:|---:|
| ANN | 539.84 | 307.43 | 0.9076 |
| LSTM | 636.51 | 260.39 | 0.8715 |

The ANN achieved a lower RMSE and higher R² than the LSTM in the overall validation evaluation.

### Peak and Non-Peak Performance

| Model | Region | RMSE (cfs) | MAE (cfs) |
|---|---|---:|---:|
| ANN | Peak | 1343.03 | 913.64 |
| ANN | Non-peak | 280.41 | 222.12 |
| LSTM | Peak | 1711.36 | 1117.45 |
| LSTM | Non-peak | 223.69 | 139.79 |

The models perform better during non-peak periods, while prediction errors increase significantly during peak streamflow events.

## 7. Hyperparameter Study

Four ANN configurations were evaluated by varying hidden-layer size and learning rate.

| Hidden Units | Learning Rate | RMSE (cfs) |
|---:|---:|---:|
| 32 | 0.001 | 513.83 |
| 16 | 0.001 | 537.06 |
| 32 | 0.005 | 565.00 |
| 16 | 0.005 | 573.44 |

The best observed hyperparameter experiment used 32 hidden units and a learning rate of 0.001.

## 8. Project Structure

```text
streamflow/
│
├── streamflow.ipynb
├── model_results.csv
├── peak_results.csv
├── ann_hyperparameter_results.csv
├── hydrograph_comparison.png
├── hydrograph_zoomed_2008.png
└── README.md# streamflow
